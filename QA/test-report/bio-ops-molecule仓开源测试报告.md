# bio-ops-molecule仓FlashAttention算子测试报告

## 1. 概述

本报告为 bio-ops-molecule 仓 `prediction/flash_attention` 算子的 910B 平台验证测试报告。测试基于 CANN 9.0.0，覆盖算子的编译出包、安装、aclnn 直调与 PyTorch 端到端精度验证。该仓由 ops-transformer（`8e9babb`，配套 CANN 9.0.0）剥离并适配 dPse 功能而来

本仓面向 FlashAttention 注意力计算负载，按算子名对外提供 aclnn 接口（经安装包 `op_api` 暴露），PyTorch 侧经 torch_npu 调用。

### 新增特性清单

| 序号 | 特性名称 | 特性描述 |
| --- | --- | --- |
| 1 | flash_attention_score | FlashAttention 前向：`(q, k, v, pse) → attention`，pse 注意力偏置（含 1NSS 布局）与 scale 缩放，支持 `bf16` / `f16` / `f32` |
| 2 | flash_attention_score_grad | FlashAttention 反向：由 `dx` 与前向中间量计算 `dq / dk / dv / dPse` 四路梯度；**dPse 输出为本仓在开源 ops-transformer 基础上的适配功能**，支持 `bf16` / `f16` / `f32` |

### 解决问题列表

不涉及（首个开源测试版本，无历史问题清单）。

### 测试活动

本次测试活动包括：测试环境确认（硬件/驱动/CANN 布局/SoC 识别）、一键编译出包、算子包安装落盘、aclnn 直调精度验证（bf16/f16/f32）、PyTorch 端到端精度验证（含 1024 长序列）。

## 2. 版本测试信息

本节描述被测对象的版本信息和测试时间，包括依赖环境与测试源码仓。

**硬件和版本要求**

产品型号：Atlas A2 / Ascend 910B2（单卡，HBM 64GB）

操作系统：覆盖以下测试因子组合

| | 因子名称 | 因子取值 |
| --- | --- | --- |
| 1 | OS | Ubuntu 22.04.5 LTS |
| 2 | CPU 架构 | ARM64（Kunpeng-920） |
| 3 | 形态 | docker / host+device |

CANN 版本：CANN 9.0.0（**开源组合包布局**：`/usr/local/Ascend/cann-9.0.0`，`ascend-toolkit/latest` 为符号链接）

驱动版本：npu-smi 25.2.1

Python 版本：Python 3.11.15

PyTorch 版本：2.6.0+cpu（配套 torch_npu 2.6.0，PyTorch 用例验证组合）

测试源码仓：https://gitcode.com/cann/bio-ops-molecule.git（`50a88d1`，基于 `f0cdca8 切换 CANN 版本至 9.0.0`；原测试用个人 fork 仓已删除，上述 commit 均已合入官方仓，溯源以官方仓为准）

测试用例仓：https://gitcode.com/Ascend-SACT/FAG-dpse-ops-test.git（dPse 专项反向用例）

测试日期：2026-09-28

## 3. 测试结论

给出明确的版本发布结论。

flash_attention 算子（前向 + 反向含 dPse）基于 CANN 9.0.0 完成 910B 平台全链路验证，共计执行 14 组测试用例，发现 0 个问题，其中有效问题 0 个。**910B 支持验证通过；剥离仓 build.sh 完整打包链路正常；本机 CANN 为组合包布局。**

| 评估维度 | 评估结果 |
| --- | --- |
| 测试用例总数 | 14 组（环境/构建/安装 3 组 + 精度 6 组 + 可靠性 2 组 + 兼容性 3 组） |
| 测试执行通过率 | 100%（14/14） |
| 测试结论 | 通过 |

## 4. 特性质量评估

特性的验证结果清单如下。aclnn 直调用例以 C++ main 经 `libcust_opapi.so` 调用算子，PyTorch 用例经 torch_npu 端到端调用；两者均以测试仓生成的 golden 数据对拍。

| 序号 | 特性 | 测试结论 | 功能 | 精度 | 兼容性 |
| --- | --- | --- | --- | --- | --- |
| 1 | flash_attention_score | 通过 | Pass | Pass | Pass |
| 2 | flash_attention_score_grad（含 dPse） | 通过 | Pass | Pass | Pass |

特性级用例（所有精度用例均校验反向 `dq / dk / dv / dPse` 四路输出与 golden 的一致性；verify_result.py 采用 atol + rtol 双判据，超差样本比例超过 LOSS 阈值判失败）：

| 序号 | 测试用例 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 1 | 测试环境确认 | npu-smi 硬件/驱动识别、CANN 9.0.0 版本与布局确认、`acl.get_soc_name()`=Ascend910B2、`/dev/davinci` 设备存在性 | PASS |
| 2 | 编译出包 | `bash build.sh --pkg --soc=ascend910b --ops=flash_attention_score,flash_attention_score_grad -j20`：6/6 内核批次（前向/反向 × 3 dtype 签名，含全部 tiling 变体）、CPack + makeself 出包 `cann-ops-transformer-custom_linux-aarch64.run` | PASS |
| 3 | 安装落盘 | source 环境后执行 `.run`：SHA256 校验 OK、0 条 WARNING、落盘 `$ASCEND_TOOLKIT_HOME/opp/vendors/custom_transformer/`（382 MB，含 6 内核签名 `.o/.json`、libcust_opapi.so、tiling 库、aclnn 头文件） | PASS |
| 4 | aclnn 直调 bf16 精度 | shape `B2,N2,S1=4,S2=4,D128`，bfloat16，LOSS=10e-3，dq/dk/dv/dPse 四路对拍 | PASS |
| 5 | aclnn 直调 f16 精度 | shape `B2,N2,S1=4,S2=4,D128`，float16，LOSS=10e-3，四路对拍 | PASS |
| 6 | aclnn 直调 f32 精度 | shape `B2,N1,S1=4,S2=4,D128`，float32，LOSS=10e-3，四路对拍 | PASS |
| 7 | PyTorch bf16 精度（默认） | shape `B1,N4,S1=4,S2=4,D16`，random mask，bfloat16，LOSS=15e-3，四路对拍 | PASS |
| 8 | PyTorch bf16 精度（长序列） | shape `B1,N4,S1=1024,S2=1024,D16`，random mask，bfloat16，LOSS=15e-3，四路对拍 | PASS |
| 9 | PyTorch f32 精度 | shape `B1,N4,S1=4,S2=4,D16`，random mask，float32，LOSS=2.44e-4，四路对拍 | PASS |

全部精度用例日志输出 `INFO: you have passed the Precision!`，汇总 6/6 PASS、0 FAIL。

## 5. DFX 专项质量评估

### 5.1 安全测试

版本整体安全测试结论：安装包完整性校验通过；安全扫描类活动未纳入本轮范围（本轮为 910B 平台功能验证，不涉及版本发布安全门禁）。

| 序号 | 测试项 | 测试结论 | 遗留风险 |
| --- | --- | --- | --- |
| 1 | 安装包完整性（makeself SHA256 自校验） | 通过 | 无 |
| 2 | SCA / antipoison 扫描 | 不涉及（未纳入本轮范围） | 无 |

### 5.2 可靠性测试

可靠性指标的验证达成情况如下（均基于本轮既有测试活动，未追加专项用例）。

| 序号 | 可靠性特性 | 测试结论 | 遗留风险 |
| --- | --- | --- | --- |
| 1 | 构建可重复性 | 通过：全量内核重编（约 100 分钟，20 核）一次成功，无随机失败 | 无 |
| 2 | 同输入重复执行结果一致 | 通过：每组 PyTorch 用例含 2 次 NPU 执行，输出与 golden 标杆脚本均一致 | 无 |

### 5.3 兼容性测试

兼容性评估：通过。

| 序号 | 兼容性场景 | 验证结果 | 遗留风险 |
| --- | --- | --- | --- |
| 1 | 驱动 npu-smi 25.2.1 | pass：acl 初始化、6/6 内核运行、全部精度用例通过 | 建议正式交付环境使用 CANN 9.0.0 配套驱动版本 |
| 2 | CANN 9.0.0 开源组合包布局（`cann-9.0.0`，`ascend-toolkit/latest` 符号链接） | pass：构建、安装、运行全链路正常 | 无 |
| 3 | Python 3.11.15 + PyTorch 2.6.0+cpu + torch_npu 2.6.0 | pass：bf16（含 1024 长序列）、f32 端到端用例通过 | 无 |

## 6. 测试执行评估

### 6.1 测试覆盖

特性以及关键测试活动的测试覆盖情况如下。

| 测试活动 | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| --- | --- | --- | --- | --- |
| 特性测试（精度） | pass | 6 | 100% | 100% |
| 构建与安装 | pass | 3 | 100% | 100% |
| 可靠性测试 | pass | 2 | 100% | 100% |
| 兼容性测试 | pass | 3 | 100% | 100% |
| 性能测试 | 不涉及 | 0 | — | — |
| 继承特性测试 | 不涉及 | 0 | — | — |

说明：特性测试覆盖已交付的 2 个算子在 bf16/f16/f32 三种 dtype 下的反向四路输出（含 dPse），aclnn 直调与 PyTorch 端到端两条调用路径；

## 7. 遗留问题和关键风险

不涉及本仓功能缺陷。

### 7.1 遗留问题统计

| | 问题总数 | 严重 | 主要 | 次要 | 不重要 | 已取消 |
| --- | --- | --- | --- | --- | --- | --- |
| 数目 | 0 | 0 | 0 | 0 | 0 | 0 |
| 百分比 | 100% | 0% | 0% | 0% | 0% | 0% |

### 7.2 遗留问题列表

| 问题单(issue链接) | 问题描述 | 问题级别 | 问题影响和规避措施 | 当前状态 |
| --- | --- | --- | --- | --- |
| 不涉及 | 不涉及 | — | — | — |

## 8. 附件
不涉及
# mfg-ops-vision仓开源测试报告

## 1. 概述

本报告为 mfg-ops-vision 仓测试报告。测试基于 CANN 9.1.0 开源包，覆盖仓内已交付算子的文档、编译出包、安装卸载、功能、精度与性能，以及配套环境兼容性。测试过程中对已纳入范围的特性执行覆盖率为 100%。

本仓面向制造业视觉场景，按算子名对外提供 aclnn 接口，不绑定单一上层模型。

### 新增特性清单

| 序号 | 特性名称 | 特性描述 |
|---|---|---|
| 1 | vision_attention | 视觉注意力；fp32 / bf16，多种 head 与 scale 组合 |
| 2 | conv_transpose 2D | 二维转置卷积；fp32 / bf16 共 24 条 |
| 3 | conv_transpose 3D | 三维转置卷积；fp32 / bf16 共 24 条 |
| 4 | sinusoidal_embedding | 正弦位置编码；dim{128,256,512} × N{1,4,16} × {fp32,int64(pos)} |
| 5 | joint_attention | 联合注意力；多 contract 变体 |
| 6 | pixel_shuffle | 像素重排；4 形状 × 2 dtype |
| 7 | pixel_unshuffle | 像素逆重排；4 形状 × 2 dtype |
| 8 | causal_rope_3d | 三维因果旋转位置编码；8 形状 × fp32/bf16 |

---

### 解决问题列表

不涉及（首个开源测试版本，无历史问题清单）。

### 测试活动

本次测试活动包括：Readme 与算子文档评估、一键编译出包、算子包与 Python 包安装卸载、按算子的功能/精度/性能验证、可靠性与兼容性验证。

## 2. 版本测试信息

本节描述被测对象的版本信息和测试时间，包括依赖环境与测试源码仓。

**硬件和版本要求**

产品型号：Atlas 300I DUO

操作系统：覆盖以下测试因子组合

| | 因子名称 | 因子取值 |
| --- | --- | --- |
| 1 | OS | OpenEular 22.03 |
| 2 | CPU 架构 | ARM64（Kunpeng-920） |
| 3 | 形态 | docker / host+device |

CANN 版本：CANN 9.1.0（**开源组合包布局**：`/usr/local/Ascend/cann-9.1.0`，`ascend-toolkit/latest` 为符号链接）

驱动版本：Ascend HDK 26.1.1

测试源码仓：https://gitcode.com/cann/mfg-ops-vision

测试日期：2026-10-29

## 3. 测试结论

mfg-ops-vision 仓 8 算子精度验收实测完成，共计执行 **121 条用例**，发现 0 个不达标项，**全部 PASS**，发现 0 个问题，其中有效问题 0 个。整体质量良好，满足出口质量标准。**建议发布。**

| 算子 | 平台 | 用例数 | 通过 |  结论 |
|---|---|---|---|---|
| vision_attention | Atlas 300I DUO | 14 | 14/14 | ✅ 达标 |
| conv_transpose 2D | Atlas 300I DUO | 24 | 24/24 | ✅ 达标 |
| conv_transpose 3D | Atlas 300I DUO | 24 | 24/24 | ✅ 达标 |
| sinusoidal_embedding | Atlas 300I DUO | 18 | 18/18 | ✅ 达标 |
| joint_attention | Atlas 300I DUO | 9 | 9/9 | ✅ 达标 |
| pixel_shuffle | Atlas 300I DUO | 8 | 8/8 | ✅ 达标 |
| pixel_unshuffle | Atlas 300I DUO | 8 | 8/8 | ✅ 达标 |
| causal_rope_3d | Atlas 300I DUO | 16 | 16/16 | ✅ 达标 |
| **合计** | — | **121** | **121/121** | **✅ 达标** |

---

## 4. 特性质量评估

各特性的验证结果清单如下。

| 序号 | 特性 | 用例数 | 测试结论 | 功能 | 精度 |
|---|---|---|---|---|---|
| 1 | vision_attention | 14 | 通过 | Pass | Pass |
| 2 | conv_transpose 2D | 24 | 通过 | Pass | Pass |
| 3 | conv_transpose 3D | 24 | 通过 | Pass | Pass |
| 4 | sinusoidal_embedding | 18 | 通过 | Pass | Pass |
| 5 | joint_attention | 9 | 通过 | Pass | Pass |
| 6 | pixel_shuffle | 8 | 通过 | Pass | Pass |
| 7 | pixel_unshuffle | 8 | 通过 | Pass | Pass |
| 8 | causal_rope_3d | 16 | 通过 | Pass | Pass |

---

#### 文档测试

检查下列交付文档文件存在，并核对应关键词/章节，确保与对外接口、构建入口一致。

| 序号 | 文档 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 1 | `README.md`（项目入口） | 仓名与两类后端交付物；三种构建入口；测试入口 `-u` | PASS |
| 2 | `LICENSE`（许可证） | Apache License 2.0 全文 | PASS |
| 3 | `SECURITY.md`（安全声明） | 运行/构建安全建议；公网地址声明表 | PASS |
| 4 | `CONTRIBUTING.md`（贡献指南） | 贡献流程、提交前自检与 PR/CI 要求 | PASS |
| 5 | `docs/README.md`（文档导航） | 入门/使用/开发/社区文档索引可跳转 | PASS |
| 6 | `docs/QUICKSTART.md`（快速入门） | 环境前置、三种构建入口、最短调用路径 | PASS |
| 7 | `docs/zh/context/dir_structure.md`（目录结构） | 仓库各目录职责与 `build.sh` 入口说明 | PASS |
| 8 | `docs/zh/op_list.md`（算子列表） | 8 个已交付算子的数学定义、输入输出与约束 | PASS |
| 9 | `docs/zh/api_list.md`（接口列表） | Python 公开接口与 aclnn 两段式入口、环境变量 | PASS |

## 5. DFX 专项质量评估

### 5.1 安全测试

版本整体安全测试结论：满足开源发布对安全声明与许可证的要求。

仓内提供 `SECURITY.md`、Apache 2.0 `LICENSE`；构建入口对非法参数拦截并提示。CI流水线中SCA和antipoison扫描通过。

| 序号 | 测试项 | 测试结论 | 遗留风险 |
| --- | --- | --- | --- |
| 1 | 安全声明与许可证 | 通过 | 无 |
| 2 | 构建参数校验 | 通过 | 无 |
| 3 | SCA扫描 | 通过 | 无 |
| 4 | Antipoison | 通过 | 无 |

### 5.2 可靠性测试

可靠性指标的验证达成情况如下。

| 序号 | 可靠性特性 | 测试结论 | 遗留风险 |
| --- | --- | --- | --- |
| 1 | 非法或退化输入被拒绝或收缩为合法切分 | 通过 | 无 |
| 2 | 融合算子原地写回（输出与输入共享 device 指针） | 通过 | 无 |
| 3 | 同 shape 重复调用精度稳定（含不同缓冲、融合注意力链路） | 通过 | 无 |

### 5.3 兼容性测试

兼容性评估：通过。

| 序号 | 兼容性场景 | 验证结果 | 遗留风险 |
| --- | --- | --- | --- |
| 1 | 驱动 Ascend HDK 26.1.1 | pass：acl 初始化、全部精度用例通过 | 无 |
| 2 | CANN 9.1.0  | pass：构建、安装、运行全链路正常 | 无 |


### 5.4 兼容性

| 序号 | 兼容性场景 | 验证结果 | 遗留风险 |
| --- | --- | --- | --- |
| 1 | CANN 9.1.0 配套 | pass | 无 |
| 2 | docker 与 host+device 形态下编译、安装、跑通算子 | pass | 无 |

## 6. 测试执行评估

本次 121 条用例采用真机实测 + 同源判据双轨取证：

| 平台 | 判据取证方式 | 用例数 | 结果 |
|---|---|---|---|
| Atlas 300I DUO | 交付包 C++ 契约测试 + ATK 等价 numpy 判据 | 121 | 121/121 PASS |

说明：特性测试覆盖已交付的 8 个算子在 Atlas 300I DUO 平台下通过 aclnn 直调运行测试用例


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
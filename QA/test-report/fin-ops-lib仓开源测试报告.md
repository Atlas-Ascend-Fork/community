# fin-ops-lib仓开源测试报告

## 1. 概述

本报告为 fin-ops-lib（金融行业算子仓）首个开源版本的测试报告。报告覆盖 fused_loss 算子、Python 包、单元测试、文档及合规检查。

当前 master `0d0840b` 的测试计划共 39 个功能用例，39 个通过；本轮完整 NPU UT 为 4/4 通过，DSpark ST 为 1/1 通过。CodeCheck、Fossbot、病毒扫描已完成，seninfo 由 GitCode 平台保障，蓝区开发无需 ENPC。

### 新增特性清单

| 序号 | 特性名称 | 特性描述 |
|---|---|---|
| 1 | fused_loss 融合投机解码损失算子族 | 7 个损失接口（kl_div / reverse_kl / jsd / ce / tv / nla / lk_hybrid），fused Triton kernel 与 eager 参考实现双路径；前向反向一对 kernel，不物化 `[T, V]` fp32 中间张量 |
| 2 | Python 包安装 | src-layout + pyproject.toml，支持 editable 安装和 wheel 构建，extras 提供 npu/cuda/dev 三组可选依赖 |
| 3 | 多后端支持 | CUDA（triton >= 3.0）、昇腾 NPU（triton-ascend 3.2.2 + torch-npu 2.10.0，UB 上限 4096 保护）、无加速器 CPU eager 回退 |
| 4 | 懒加载 Triton | 模块导入不依赖 Triton，无 Triton 主机可正常使用 eager 参考实现 |

### 解决问题列表

- PR #12、#13 已完成开源清单、安全文档和中英文文档整改并合入。
- PR #15 已将 triton-ascend 升级为 3.2.2、torch-npu 调整为 2.10.0并合入。
- PR #19 已补齐 CMakeLists.txt 的 Apache 许可头并合入。
- PR #20 已合入，完成测试集调整，当前 master 为 `0d0840b`。

## 2. 版本测试信息

### 2.1 被测版本与本次验证

- 报告同步日期：2026-11-23。
- 测试源码仓：https://gitcode.com/cann/fin-ops-lib 。
- 当前 master：`0d0840b8ad0ec749a9779546fce4ffff522aa15a`，包含 PR #12、#13、#15、#19、#20。
- 先前 `fc2f28a` 的 CPU 验证环境：Windows x86_64，Python 3.10.1，PyTorch 2.11.0+cpu，pytest 9.0.3，无可用加速器。
- PR #20 分支的 CPU 实测结果：`3 passed, 1 skipped, 6 subtests passed`；跳过项为需要 Triton 和加速器的测试。
- 先前 `fc2f28a` 的 `bash build.sh --help` 正常；`uv build --wheel` 成功，wheel 中 `fused_loss` 导入成功。

上述 CPU/构建结果作为历史证据保留，本轮新增验证为 §2.2 的当前 master NPU UT/ST。当前测试计划按 39 个功能用例统计，NPU 顶层测试单独报告，不与子用例重复累加。

### 2.2 特性测试环境（当前 master NPU 实测）

- 实测日期：2026-11-23；被测提交与 §2.1 相同，为 `0d0840b8ad0ec749a9779546fce4ffff522aa15a`。
- 产品型号：Ascend 910B3；UT 使用物理卡 0，ST 使用物理卡 1。
- 操作系统：Ubuntu 22.04.5 LTS，aarch64。
- CANN toolkit：9.1.0，inner version `V100R001C11SPC001B243`；安装路径 `/usr/local/Ascend/cann-9.1.0`。
- NPU 驱动：25.5.2；固件：7.7.0.3.220。
- Python：3.12.13；pytest：8.3.2。
- PyTorch：`2.10.0+cpu`（`__version__`，通过 torch_npu 执行 NPU）；torch-npu：`2.10.0.post6`。
- Triton：实际导入模块 `3.2.0`；安装元数据为 `triton 3.5.0`、`triton-ascend 3.2.2`，分别记录，不混写。
- 调用方案：当前 master 的 `fused_* -> _FusedLoss.apply -> Triton`，不包含 `torch.ops` 注册层。

| 本轮 NPU 项目 | 实际结果 | 范围说明 |
|---|---|---|
| 完整 UT（不过滤） | **4 passed**，662.29 秒 | 当前仓内全部测试；覆盖 39 个子用例，无 deselect、skip、xfail 或失败 |
| DSpark ST | **PASS** | 仓内示例经默认设备注入使用 NPU；`fused path: True`，输出 `[2, 512]` fp32，loss 和 gradient 均与 eager 对齐 |

本轮 UT 命令未使用 `-k`、`--ignore` 或其他排除参数。当前计划数与通过率仅覆盖仓内现有测试。原始日志与环境明细见 [fork 证据分支](https://gitcode.com/dongzihaotajiu/community/tree/docs/fin-ops-lib-test-report-assets/QA/test-report/assets/fin-ops-lib)。

### 2.3 门禁环境（归档）

GitCode CI，x86 无卡静态检查，取自 run #13 Test_image 日志：

- precommit 镜像：ubuntu20.04.05_x86:alpha113。
- codecheck 镜像：ubuntu24.04_x86:lv1_v1.1032。
- staticcheck 镜像：ubuntu24.04.03:v1.0。

## 3. 测试结论

功能测试结论：**通过**。当前测试计划共计 39 个功能测试用例，39 个通过，用例通过率 100%。PR #20 分支的 CPU 验证为 3 passed、1 skipped、6 subtests passed；当前 `0d0840b` 的完整 NPU UT 为 4 passed，DSpark ST 为 1/1 通过。当前 master 的 UT/ST 通过率均为 100%。

版本发布结论：**测试与扫描项已通过，可提交开源发布评审（QA-SIG 预审及 PMC 批准按社区流程执行）**。PR #15、#19、#20 已合入；CodeCheck、Fossbot、病毒扫描已完成，seninfo 由 GitCode 平台保障，蓝区开发无需 ENPC。

## 4. 特性质量评估

N/A 表示该评估维度不适用。性能结果沿用归档记录；CPU 安装、导入和构建入口结果来自 `fc2f28a`，当前 `0d0840b` 的 NPU 普通路径功能、精度已重新验证。

| 序号 | 特性 | 测试结论 | 功能 | 精度 | 性能 | 可靠性 | 兼容性 |
|---|---|---|---|---|---|---|---|
| 1 | fused_loss 融合投机解码损失算子族 | 通过（当前 master NPU 普通路径） | Pass（本轮 NPU） | Pass（本轮 NPU） | Pass（归档） | Pass（普通路径） | Pass（NPU 普通路径） |
| 2 | Python 包安装 | 通过 | Pass | N/A | N/A | Pass | Pass |
| 3 | 多后端支持 | 通过（NPU 普通路径；CUDA 归档） | Pass | Pass | N/A | Pass | Pass（NPU 普通路径） |
| 4 | 懒加载 Triton | 通过 | Pass | N/A | N/A | Pass | Pass |

## 5. DFX专项质量评估

### 5.1 安全测试

- 门禁流水线中的 Antipoison、SCA、OAT 检查已通过；三方依赖已登记 `Third_Party_Open_Source_Software_List.yaml`，并在 `Third_Party_Open_Source_Software_Notice` 声明。
- 漏洞反馈渠道、公网地址声明及文件权限参考表见 `SECURITY.md` / `SECURITY_en.md`。
- CodeCheck、Fossbot、病毒扫描已完成，seninfo 由 GitCode 平台保障，蓝区开发无需 ENPC。

| 检查项 | 当前状态 | 结论 |
|---|---|---|
| CodeCheck 静态检查 | 已完成 | 通过 |
| Fossbot 来源风险扫描 | 已完成 | 通过 |
| 病毒扫描（Antipoison） | 已完成 | 通过 |
| SCA 开源组件扫描 | 已完成 | 通过 |
| OAT 开源合规检查 | 已完成 | 通过 |
| seninfo 敏感词检查 | GitCode 平台保障 | 满足平台保障要求 |
| ENPC 外来非公开信息扫描 | 蓝区开发不适用 | 无需执行 |

### 5.2 可靠性测试

| 序号 | 可靠性特性 | 测试结论 | 遗留风险 |
|---|---|---|---|
| 1 | 无 Triton/加速器时模块可导入、eager 路径可用 | 通过 | 暂无 |
| 2 | masked lane 的 inf/nan 不进入累加器；零梯度行 early-out 返回精确零 | 通过（当前 master NPU 实测） | 暂无 |

### 5.3 性能测试

| 场景 | 模型 | 特性 | 性能指标 | 测试环境 | 测试结果 | 遗留风险 |
|---|---|---|---|---|---|---|
| 训练 | DSpark 草稿蒸馏（Qwen3-4B） | fused TV loss | step 3.30s（eager 4.84s，-32%）；吞吐 24.2 samples/s（+47%） | Ascend 910B3，CANN 9.1.0，NPU 驱动 25.5.2 | Pass（归档） | 当前 master 未重新测量 |

### 5.4 兼容性测试

兼容性评估：**通过（归档及当前 master NPU 普通路径实测）**。

| 序号 | 兼容性场景 | 验证结果 | 遗留风险 |
|---|---|---|---|
| 1 | torch >= 2.1，triton >= 3.0 或 triton-ascend 3.2.2 + torch-npu 2.10.0，extras 分组 | Pass（当前 master NPU 普通路径） | 本轮为已有运行环境源码验证，不替代干净环境依赖安装矩阵 |
| 2 | Ubuntu/Euler，x86_64/aarch64，官方 Release wheel 按 Python 版本和架构选择 | Pass（Ubuntu aarch64 本轮实测；其余归档） | 其他 OS/架构未在本轮重新执行 |
| 3 | CUDA、昇腾 NPU 精度测试，无加速器环境使用 eager | Pass（NPU 普通路径本轮实测；CUDA 归档） | 其他后端和平台组合未在本轮重新执行 |
| 4 | 昇腾 A2/A3 既有验证；本轮为 Ascend 910B3；上游 H20 CUDA 实测 | Pass（归档） | A3 未在本轮重新执行 |

## 6. 测试执行评估

### 6.1 测试覆盖

用例覆盖率按“实际执行数/计划执行数”统计。当前特性测试计划为 39 个子用例，其余活动为验证项或场景数，不与 39 个子用例重复累加。本轮对当前仓内全部 NPU UT 不做过滤，共执行 4 个顶层测试，覆盖 39 个子用例，全部通过。seninfo 由 GitCode 平台保障，ENPC 按蓝区开发不适用处理。

| 测试活动 | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
|---|---|---|---|---|
| 特性测试 | Pass | 39 | 100%（39/39） | 100%（39/39） |
| 当前 master NPU UT（完整、不过滤） | Pass | 4 个顶层测试（39 个子用例） | 100%（4/4） | 100%（4/4） |
| 当前 master NPU ST | Pass | 1 个 DSpark 场景 | 100%（1/1） | 100%（1/1） |
| 性能测试 | Pass（归档） | 1 组 | 100%（1/1） | 100%（1/1） |
| 可靠性测试 | Pass | 2 项 | 100%（2/2） | 100%（2/2） |
| 继承特性测试 | N/A | 不涉及 | N/A | N/A |
| 兼容性测试 | Pass（归档及配套实测） | 4 项 | 100%（4/4） | 100%（4/4） |
| 安全测试 | Pass | 7 项（5 项执行通过、1 项平台保障、1 项不适用） | 执行项 100%（5/5）；seninfo 平台保障；ENPC N/A | 执行项 100%（5/5）；其余按平台保障或不适用处理 |

### 6.2 Readme内容评估

Readme内容评估：**通过**（PR #12、#13 已合入）。

| 验证项 | 验证内容 |
|---|---|
| 文档内容完整性 | 提供仓定位、目录结构、快速入门、算子接口、源码下载、贡献指南、安全声明、许可证、SIG 和问题反馈入口；中英文文档及切换链接齐全 |
| 文档内容正确性 | 7 个损失接口与代码一致；README 导航、文档链接和中英文切换已复核；安装与测试命令经实际验证 |

### 6.3 安装包功能验证

安装包功能评估：**通过**。

| 验证项 | 验证内容 |
|---|---|
| 算子包安装 | editable 安装及 NPU/CUDA/dev extras 安装方式见仓内文档；`fc2f28a` 的 wheel 构建和导入已验证 |
| 打包完整性 | `packages.find` 发现 src/ 下算子包；`fc2f28a` 的 wheel 包含 `fused_loss/__init__.py` 和 `fused_loss/core.py` |
| 卸载功能 | `pip uninstall fin-ops-lib` 正常卸载（归档） |
| 无依赖导入 | `fc2f28a` 的无 Triton 环境可从 wheel 导入 `fused_loss`；仅调用 fused 接口时才要求 Triton |

### 6.4 算子UT功能验证

测试功能评估：**通过**。当前测试计划共 39 个测试用例（含参数化子用例）。PR #20 分支的 CPU 实测为 `3 passed, 1 skipped, 6 subtests passed`；当前 `0d0840b` 的完整 NPU UT 不做过滤，实测为 `4 passed`，覆盖 39 个子用例，无跳过或失败。

实际执行命令（未使用 `-k`、`--ignore` 或其他排除参数）：

```bash
PYTHONDONTWRITEBYTECODE=1 PYTHONPATH=src \
ASCEND_RT_VISIBLE_DEVICES=0 \
TRITON_CACHE_DIR=/data/fin-scan-work/npu-st-ut/pr20-refresh/fin-ops-lib/ut-triton-cache \
python3 -m pytest -p no:cacheprovider -v -rs tests/
```

#### 6.4.1 融合/参考一致性（精度）测试（7 损失 × 3 档 = 21 用例，需加速器）

每损失接口在三种失效模式档下比对 fused 与 eager 的 loss 值与 logits 梯度（loss：atol=1e-4/rtol=1e-3；梯度：atol=1e-3/rtol=1e-2；ce 的 bf16 档按 eager 自身精度放宽）。

| 序号 | 测试用例名称 | 档位 | 测试内容 | 结果 |
|---|---|---|---|---|
| 1-7 | test_fused_matches_eager[kl_div/rkl/jsd/ce/tv/nla/lk_hybrid] | fp32 饱和点质量行 | 极端分布下梯度公式与 log 空间下溢处理 | PASS（当前 master NPU 实测） |
| 8-14 | 同上 | bf16（训练 dtype） | 半精度下 fused/eager 一致性 | PASS（当前 master NPU 实测） |
| 15-21 | 同上 | 151936 宽词表 | 多 block 流式 + 非 2 幂尾块；NPU 触发 4096 block 上限 | PASS（当前 master NPU 实测） |

#### 6.4.2 设备 block 上限测试（11 用例，CPU 可跑）

| 序号 | 测试用例名称 | 测试内容 | 结果 |
|---|---|---|---|
| 1-6 | NPU 档（vocab 512/4096/8192/32768/131072/151936） | block 上限 4096（UB 保护）边界正确 | PASS |
| 7-11 | CUDA 档（vocab 512/4096/8192/131072/151936） | block 上限 131072 边界正确 | PASS |

#### 6.4.3 eager 参考实现测试（7 用例，CPU 可跑）

| 序号 | 测试用例名称 | 测试内容 | 结果 |
|---|---|---|---|
| 1-6 | test_eager_implementation_supports_differentiable_targets[6 损失] | eager 路径目标梯度可导 | PASS |
| 7 | test_eager_losses_self_consistent | eager 实现间恒等式自洽（nla/tv、hybrid 混合权重、ce 与 cross_entropy 等价） | PASS |

### 6.5 系统测试（当前 master NPU ST）

执行仓内 `examples/dspark_fused_tv_example.py` 的 DSpark TV loss 调用、L1/acceptance 组合及反向传播。示例默认创建 CPU 张量，本轮仅通过 `torch.set_default_device("npu")` 注入默认设备，未修改示例源码。

| 验证项 | 实际结果 |
|---|---|
| 真实融合路径 | PASS；日志为 `fused path: True`，不是 CPU fallback |
| 输出 | TV shape `[2, 512]`，dtype `torch.float32`；acceptance 范围 `[0.0035, 0.1316]` |
| 前向/反向精度 | PASS；`torch.testing.assert_close` 验证 fused loss 和 logits gradient 与 eager 一致 |
| 范围限制 | 小张量功能 ST；不替代完整模型训练、金融数据验证或性能测试 |

实际运行方式：

```bash
PYTHONDONTWRITEBYTECODE=1 PYTHONPATH=src \
ASCEND_RT_VISIBLE_DEVICES=1 \
TRITON_CACHE_DIR=/data/fin-scan-work/npu-st-ut/pr20-refresh/fin-ops-lib/st-triton-cache \
python3 -c 'import runpy, torch, torch_npu; torch.set_default_device("npu"); runpy.run_path("examples/dspark_fused_tv_example.py", run_name="__main__")'
```

## 7. 遗留问题和关键风险

### 7.1 遗留问题统计

|  | 问题总数 | 严重 | 主要 | 次要 | 不重要 | 已取消 |
|---|---|---|---|---|---|---|
| 数目 | 0 | 0 | 0 | 0 | 0 | 0 |
| 百分比 | 100% | 0% | 0% | 0% | 0% | 0% |

### 7.2 遗留问题列表

| 问题单（跟踪链接） | 问题描述 | 问题级别 | 问题影响和规避措施 | 当前状态 |
|---|---|---|---|---|
| 不涉及 | 无遗留问题 | — | — | — |

## 8. 附件

- 当前 master：https://gitcode.com/cann/fin-ops-lib/commit/0d0840b8ad0ec749a9779546fce4ffff522aa15a
- 首个特性 PR：https://gitcode.com/cann/fin-ops-lib/pull/10
- 开源清单对齐 PR：https://gitcode.com/cann/fin-ops-lib/pull/12
- 英文文档 PR：https://gitcode.com/cann/fin-ops-lib/pull/13
- triton-ascend 3.2.2 升级 PR：https://gitcode.com/cann/fin-ops-lib/pull/15
- CMakeLists 许可头 PR：https://gitcode.com/cann/fin-ops-lib/pull/19
- 测试集调整 PR：https://gitcode.com/cann/fin-ops-lib/pull/20
- triton-ascend 官方 v3.2.2 Release：https://github.com/triton-lang/triton-ascend/releases/tag/v3.2.2
- 门禁流水线记录：https://gitcode.com/cann/fin-ops-lib/actions
- 当前 master NPU 实测环境：[npu-environment-pr20.json](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-ops-lib-test-report-assets/QA/test-report/assets/fin-ops-lib/npu-environment-pr20.json)
- 当前 master 完整 UT 日志（不过滤）：[npu-ut-pr20.log](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-ops-lib-test-report-assets/QA/test-report/assets/fin-ops-lib/npu-ut-pr20.log)
- 当前 master NPU DSpark ST 日志：[npu-st-pr20.log](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-ops-lib-test-report-assets/QA/test-report/assets/fin-ops-lib/npu-st-pr20.log)
- 证据校验和：[SHA256SUMS](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-ops-lib-test-report-assets/QA/test-report/assets/fin-ops-lib/SHA256SUMS)

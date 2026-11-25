# fin-recipes仓开源测试报告

## 1. 概述

本报告为 fin-recipes（金融行业模型与应用仓）首个开源版本的测试报告。报告覆盖配方胶水层、安装器、单元测试、离线 NPU 系统测试、文档及合规检查。

当前 master的测试计划共 8 个仓内 UT 用例，8 个通过；真实 `run.sh` 离线 ST 为 **3/3 场景通过**；可靠性和兼容性在限定范围内均为 **Pass（最小范围）**。CodeCheck、Fossbot、病毒扫描已完成，seninfo 由 GitCode 平台保障，蓝区开发无需 ENPC。

### 新增特性清单

| 序号 | 特性名称 | 特性描述 |
|---|---|---|
| 1 | src/spec_decoding/draft_distill 草稿模型蒸馏配方 | SpecForge 引擎 + 可选 fin-ops-lib fused_loss，仓内包含配置派生说明、脚本、薄胶水和文档 |
| 2 | install_engine.sh 安装器 | 读取 REQUIRED_ENGINE.txt，下载固定源码、应用仓内离线依赖补丁并安装钉定引擎和运行时 |
| 3 | wire_fused_loss 胶水层 | 加速可用时注入 7 个融合损失；不可用时跳过注入并显式选择 SpecForge eager |
| 4 | 一键启动脚本 | run.sh 串联只告警预检、条件加速选择和引擎 CLI 委托，不再强制 fused 开关 |
| 5 | src 目录统一 | 配方迁移至 `src/spec_decoding/`，同步打包、测试和中英文文档路径 |

### 解决问题列表

- PR #11、#12、#17 已完成开源合规文件、中英文文档、目录迁移和金融多模态分类。
- MR #18 修复了缺 fin-ops-lib 时预检阻断、训练入口无条件注入及强制 fused 开关问题。
- MR #18 将 fin-ops-lib pin 更新为 `0d0840b`，并以仓内补丁明确 CANN 9.1 离线依赖组合，不再混用声明版本与实测版本。
- MR #18 修正了配置文档中的上游配置文件名，补充 eager 回退、安装器及环境边界测试。

## 2. 版本测试信息

### 2.1 被测版本

- 报告同步日期：2026-11-23。
- 源码仓：https://gitcode.com/cann/fin-recipes 。
- 当前 master：`d6064d79b5f74273dc1e27c6afa85c1c93de2356`。
- 代码评审：https://gitcode.com/cann/fin-recipes/merge_requests/18 。
- 调用方式：当前 master的 `_FusedLoss.apply` 路径；未使用 `torch.ops` 分支或 full graph 测试。

### 2.2 当前 master实测环境与依赖

| 项目 | 实测版本或范围 |
|---|---|
| SpecForge | `6c357224f446a16c6530c4fc94f6b1f5913a7e1e` + 仓内 `specforge-cann91-offline.patch` |
| fin-ops-lib | `0d0840b8ad0ec749a9779546fce4ffff522aa15a`；安装后的 `direct_url.json` 已核对 commit |
| 操作系统 / 架构 | Ubuntu 22.04.5 LTS / aarch64 |
| 芯片 | Ascend 910B3；物理卡 1，进程内 `npu:0` |
| CANN | toolkit 9.1.0，`V100R001C11SPC001B243`；**未升级或降级** |
| 驱动 / 固件 | 25.5.2 / 7.7.0.3.220 |
| Python / pytest | 3.12.13 / 8.3.2 |
| PyTorch / torch-npu | `2.10.0+cpu` / `2.10.0.post6` |
| Triton | triton-ascend `3.2.2`；triton 分发包 `3.5.0`；实际 `triton.__version__` 为 `3.2.0` |
| transformers / accelerate | `5.12.1` / `1.16.0` |
| SGLang | 未安装；离线训练不需要，在线捕获及服务不在本轮范围 |
| 检查工具 | Ruff `0.14.14`、codespell `2.4.1`；OAT 按仓内脚本安装 `oat-py>=1.0.1` |

新建 venv 不启用系统 site-packages，初始仅有 pip。安装及训练不继承既有源码环境的 `PYTHONPATH`，ST 仅额外加载归档的观测脚本；`fused_loss`、`specforge`、`torch`、`torch_npu`、`triton`、`triton.language` 和 `transformers` 均从该 venv 导入。SpecForge 安装元数据已确认选择 `torch==2.10.0` 且不包含 SGLang。

由于远程 obsfs 源码目录不支持本仓 setuptools 所需的目录时间戳更新，真实构建在本机临时 venv 和源码副本中执行。源码副本与修改工作树逐文件 SHA-256 一致，未屏蔽构建错误，也未使用既有 SpecForge 源码树或预装 Python 包拼接运行环境。该文件系统限制不是产品依赖冲突。

### 2.3 历史基线结果（保留，不替代本轮）

历史基线 `b8bd447` 原有 3 个 CPU stub UT 在 Windows 和 NPU 主机均为 3/3 通过；原有两步源码方式 DSpark ST 也通过。该历史 ST 使用 fin-ops-lib `05e99781`、transformers `5.19.0` 和既有源码环境，不是本轮干净安装及回退验证的依据。原始日志继续保留于 `https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/` 根目录。

### 2.4 门禁与本地检查

- PR #17 的 CI 记录沿用历史归档；PR #18 的评审流程不改变本轮实测结论。
- 当前 master本地执行：Ruff check、Ruff format `--check`、变更文件 codespell 均通过。
- OAT 对 14 个变更文件检查通过：Invalid File Type 为 0，License Header Invalid 为 0。
- 全仓 codespell 另有 master 既有 README 中两处 `thirdparty` 提示，本次未修改这些文件；变更文件检查无告警。
- Fossbot、seninfo、ENPC 均已独立完成扫描验证并通过，按本报告口径计入安全测试结果。

## 3. 测试结论

- **当前 master仓内 UT：Pass，8/8。** 这些是胶水层和安装契约测试，不冒充 NPU kernel UT。
- **当前 master离线 ST：Pass，3/3 场景。** NPU fused、无 Triton/加速器 eager、未安装 fin-ops-lib eager 均通过真实 `run.sh` 完成两步训练。
- **可靠性：Pass（最小范围）。** 两种不可用场景均不阻断 eager， fused 调用次数为 0。
- **兼容性：Pass（最小范围）。** 干净安装、`pip check`、声明的单一平台矩阵、两种后端路径和真实入口均有证据。
- **测试基线：当前 master。** 本报告按该版本的实测结果给出结论。
- **版本发布结论：测试与扫描项已通过，可提交开源发布评审（QA-SIG 预审及 PMC 批准按社区流程执行）。** 最小可靠性和兼容性 Pass 不扩展为全平台发布通过。

## 4. 特性质量评估

N/A 表示该维度不适用；“Pass（承接）”表示数值或性能证据由 fin-ops-lib 与 SpecForge 承接，不是本仓独立全量实测。

| 序号 | 特性 | 测试结论 | 功能 | 精度 | 性能 | 可靠性 | 兼容性 |
|---|---|---|---|---|---|---|---|
| 1 | draft_distill 草稿模型蒸馏配方 | Pass（当前 master、限定离线范围） | Pass | Pass（承接） | Pass（承接） | Pass（最小范围） | Pass（最小范围） |
| 2 | install_engine.sh 安装器 | Pass（本机干净环境） | Pass | N/A | N/A | Pass | Pass（限定矩阵） |
| 3 | wire_fused_loss 胶水层 | Pass（条件注入与回退实测） | Pass | Pass（承接） | N/A | Pass（最小范围） | Pass（限定矩阵） |
| 4 | 一键启动脚本 | Pass（真实 CLI 三场景） | Pass | N/A | N/A | Pass（最小范围） | N/A |
| 5 | src 目录统一与金融多模态分类 | Pass | Pass | N/A | N/A | Pass | Pass（本机打包安装） |

## 5. DFX专项质量评估

### 5.1 安全测试

- 本仓不分发模型权重与金融数据，不捆绑三方件二进制；三方件清单、版权声明、CONTRIBUTING 和 SECURITY 已提供。
- 本次 OAT 14 个变更文件检查通过；CodeCheck、Fossbot、病毒扫描已完成，seninfo 由 GitCode 平台保障，蓝区开发无需 ENPC。

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

可靠性评估：**Pass（最小范围）**。

| 序号 | 可靠性场景 | 测试结论 | 实测证据 |
|---|---|---|---|
| 1 | 已安装 fin-ops-lib，但无 Triton/加速器 | Pass | 预检和训练入口均告警并选择 eager；真实 run.sh 完成 2 步，loss、梯度及参数有限，7 个 fused 函数调用均为 0 |
| 2 | 未安装 fin-ops-lib | Pass | 预检仅警告、不注入、不阻断；真实 run.sh 完成 2 步 eager，loss、梯度及参数有限，fused 调用为 0 |

两个场景均使用同一干净 venv，通过卸载对应测试包构造，未更改 CANN 或系统 Python。完成后已恢复 fin-ops-lib、triton、triton-ascend 和 torch-npu，恢复后的 `pip check`、导入检查及 fused 预检均通过。

### 5.3 性能测试

配方自身无独立性能指标，算子性能数据承接 fin-ops-lib 开源测试报告。本轮两步小模型 ST 不用于性能结论。

| 场景 | 特性 | 测试环境 | 测试结果 | 遗留风险 |
|---|---|---|---|---|
| DSpark 草稿蒸馏 | 配方胶水层无独立指标，承接 fused TV loss 结果 | Ascend 910B3，CANN 9.1.0 | Pass（承接） | 非本仓独立性能实测；本轮未测吞吐、时延或显存收益 |

### 5.4 兼容性测试

兼容性评估：**Pass（最小范围）**。声明多少验证多少，未验证平台不写成 Pass。

| 序号 | 兼容性场景 | 验证结果 | 范围说明 |
|---|---|---|---|
| 1 | 固定依赖与真实安装 | Pass | SpecForge、fin-ops-lib commit 和运行时版本已核对；本仓安装成功，`pip check` 无冲突，无 SGLang 混入 |
| 2 | Ubuntu 22.04 + aarch64 + Ascend 910B3 + Python 3.12 | Pass | 本轮唯一声明通过的 OS/架构/芯片/Python 组合 |
| 3 | NPU fused 与 CPU eager 后端配套 | Pass | 同一主机完成 fused 及两种 eager 实测；不扩展为 CUDA 或其他后端通过 |
| 4 | 固定 SpecForge 引擎与真实 run.sh | Pass | 单卡离线 DSpark 两步训练通过；在线捕获、Mooncake、SGLang 服务不在范围 |

Euler、x86_64、A3、CUDA、其他 OS 和芯片均为**未验证/不在本轮范围**。仓内补丁明确本轮选择的依赖组合，不代表 SpecForge 官方对所有 PyTorch 版本的兼容承诺。

## 6. 测试执行评估

### 6.1 测试覆盖

| 测试活动 | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
|---|---|---|---|---|
| 仓内 UT | Pass | 8 | 100%（8/8） | 100%（8/8） |
| 真实 run.sh 离线 ST | Pass | 3 个场景，每个 2 步 | 100%（3/3） | 100%（3/3） |
| 可靠性测试 | Pass（最小范围） | 2 | 100%（2/2） | 100%（2/2） |
| 兼容性测试 | Pass（最小范围） | 4 | 100%（4/4） | 100%（4/4）；仅限声明矩阵 |
| 性能测试 | Pass（承接） | 1 组（承接） | 100%（承接） | 100%（承接） |
| 安全测试 | Pass | 7 项（5 项执行通过、1 项平台保障、1 项不适用） | 执行项 100%（5/5）；seninfo 平台保障；ENPC N/A | 执行项 100%（5/5）；其余按平台保障或不适用处理 |

### 6.2 Readme内容评估

当前 master说明文档在本轮限定范围内为 **Pass**：

- 安装命令、实际 pin、CANN 9.1 离线依赖组合及 eager 回退行为与代码一致。
- 配置示例名已修正为上游实际存在的 `qwen3-4b-dspark-offline.yaml` 和 `qwen3-4b-dspark-disaggregated.yaml`。
- 已明确在线捕获、SGLang 及其他平台未验证，不以文档声明替代实测。
- 根目录 docs/examples 的占位内容和后续场景规划仍需持续完善，不写成已交付教程或全场景覆盖。

### 6.3 配方安装与静态检查

实际安装使用固定官方源码地址和以下命令；GitCode 凭据仅用于读取受限仓，不写入报告或证据：

```bash
python -m venv --copies /tmp/fin-recipes-compat-venv
unset PYTHONPATH
TMPDIR=/tmp/fin-recipes-compat-tmp \
PYTHON_BIN=/tmp/fin-recipes-compat-venv/bin/python \
PIP_NO_COMPILE=1 PYTHONDONTWRITEBYTECODE=1 \
./install_engine.sh --recipe src/spec_decoding/draft_distill

# 在 SHA-256 已核对一致的本机源码副本中
python -m pip install --no-build-isolation '.[dev]'
python -m pip check
python -m pytest -p no:cacheprovider -q tests/
```

`pip check` 实际输出 `No broken requirements found.`。恢复测试环境后再次检查，结果相同。完整依赖清单、安装日志、包来源、导入路径、补丁 SHA-256 和源码副本比对均见附件。

### 6.4 配方 UT 功能验证

全量结果：**8 passed，14 warnings，9.14s**。警告为 PyTorch 对 `torch.jit.script_method` 的弃用提示，无失败或 ERROR。UT 是 CPU 可运行的胶水层测试；NPU kernel 的实际调用由 §6.5 ST 证明。

| 序号 | 测试用例 | 结果 |
|---|---|---|
| 1 | 7 个融合损失全部替换且重复注入幂等 | PASS |
| 2 | 缺 Triton 时可用性探测返回 False | PASS |
| 3 | 加速可用时注入并设置 fused=1 | PASS |
| 4 | 缺 Triton 时不注入并设置 fused=0 | PASS |
| 5 | 缺 fin-ops-lib 时预检仅告警并返回 0 | PASS |
| 6 | 缺 fin-ops-lib 时跳过注入并选择 eager | PASS |
| 7 | 训练入口委托 SpecForge 并透传退出码 | PASS |
| 8 | 安装干跑展示固定引擎、补丁、算子和 NPU 运行时 | PASS |

### 6.5 真实 run.sh 系统测试

三组测试均执行仓内真实入口 `run.sh <config>`，不是旧的自定义编程式训练脚本。测试观测层只统计调用并在 `TrainerCore.train_step` 返回后记录指标，不修改产品训练逻辑。所有通过日志均无 `ERROR` 和 `Traceback`。

| 场景 | 训练结果 | loss / grad_norm | 融合调用 | checkpoint |
|---|---|---|---|---|
| NPU fused | 2 步完成，`DSparkTrainStrategy`，fused=1 | 第 1 步 `1.485413 / 5.768185`；第 2 步 `1.159476 / 2.286787`，均有限 | fused TV 共 4 次，输入设备 `npu:0`，其余 6 个 fused 函数为 0 | 2 个 checkpoint，每个 18 个参数张量均有限 |
| 无 Triton/加速器 eager | 2 步完成，fused=0 | 第 1 步 `1.476688 / 5.901380`；第 2 步 `1.214264 / 3.137635`，均有限 | 7 个 fused 函数均为 0 | 2 个 checkpoint，参数均有限 |
| 未安装 fin-ops-lib eager | 2 步完成，预检只警告，fused=0 | 第 1 步 `1.476688 / 5.901380`；第 2 步 `1.214264 / 3.137635`，均有限 | 7 个 fused 函数均为 0 | 2 个 checkpoint，参数均有限 |

范围仍为小模型、合成特征、单卡两步离线训练。完整金融语料、真实生产模型、在线捕获与服务、性能、多卡和分布式平台矩阵未覆盖。

## 7. 遗留问题和关键风险

### 7.1 遗留问题统计

| 问题总数 | 严重 | 主要 | 次要 | 不重要 | 已取消 |
|---|---|---|---|---|---|
| 2 | 0 | 0 | 2 | 0 | 0 |

### 7.2 遗留问题列表

| 跟踪链接 | 问题描述 | 级别 | 影响与措施 | 当前状态 |
|---|---|---|---|---|
| 无（范围与 Roadmap） | 完整金融语料、在线服务、性能、其他平台及 docs/examples 内容未闭环 | 次要 | 本轮已收窄声明，未验证项不写 Pass；后续按 Roadmap 补充 | 范围外/持续跟踪 |
| 根目录 README / README_en | master 既有两处 `thirdparty` codespell 提示 | 次要 | 非本次变更引入；变更文件检查通过，基线提示另行处理，不宣称全仓拼写零告警 | 待单独处理 |

## 8. 附件

- 当前 master：https://gitcode.com/cann/fin-recipes/commit/d6064d79b5f74273dc1e27c6afa85c1c93de2356
- 代码评审：[fin-recipes MR #18](https://gitcode.com/cann/fin-recipes/merge_requests/18)
- 报告评审：[community MR #1069](https://gitcode.com/cann/community/merge_requests/1069)
- 本轮结果汇总：[summary.json](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/summary.json)
- 实测环境与版本：[environment.json](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/environment.json)
- 完整安装日志：[install-utf8.log](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/install-utf8.log)（原始字节日志为同目录 `install.log`）
- 依赖检查：[pip-check.log](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/pip-check.log)、[restored-pip-check.log](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/restored-pip-check.log)
- 依赖清单：[pip-freeze.txt](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/pip-freeze.txt)
- 仓内 UT：[unit-tests.log](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/unit-tests.log)
- NPU fused ST：[validation.json](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/fused/validation.json)、[run.log](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/fused/run.log)
- 无加速器 eager ST：[validation.json](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/eager-no-accelerator/validation.json)、[run.log](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/eager-no-accelerator/run.log)
- 未安装 fin-ops-lib eager ST：[validation.json](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/eager-missing-fin-ops/validation.json)、[run.log](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/eager-missing-fin-ops/run.log)
- 复现与校验脚本：[scripts/](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/scripts/)
- 含尾随空格的 `pip show` 等原始输出按字节保存为 `.log.gz`；解压后的原始 SHA-256 见 [compressed-log-sha256.json](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/compressed-log-sha256.json)，未为格式检查改写原始证据。
- OAT 结果：[oat-result.txt](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/compatibility/oat-result.txt)
- 算子质量证据：[fin-ops-lib仓开源测试报告](https://gitcode.com/cann/community/pull/1068)
- 全部证据校验和：[SHA256SUMS](https://gitcode.com/dongzihaotajiu/community/blob/docs/fin-recipes-test-report-assets/QA/test-report/assets/fin-recipes/SHA256SUMS)

复现脚本保留实际工作目录；在其他环境执行时需替换路径并准备有权限的 GitCode 凭据，不得替换已声明的依赖 commit 或把未验证平台写成通过。

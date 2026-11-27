# its-trip-samples 仓开源测试报告

## 1. 概述

本报告为 its-trip-samples 仓开源测试报告。its-trip-samples 是 CANN 社区 Intelligent Transportation System（ITS）SIG 的行业应用验证仓，按“五个工程域 + 跨域样例”组织，当前处于目录结构与开源治理骨架阶段，尚无可直接运行的端到端样例。ITS SIG 组评审已确认通过，本报告用于 QA-SIG 评审。

本次测试覆盖仓内已交付的仓库骨架、开源治理文件、文档体系、samples 模板、仓库级自动化测试、GitCode workflow 配置，以及日常流水线 CI 安全扫描结果。测试对象为 `dev` 分支 HEAD，不包含端到端功能、模型精度、性能、运行态可靠性与兼容性测试。

### 新增特性清单

| 序号 | 特性名称 | 特性描述 |
| --- | --- | --- |
| 1 | 五工程域目录骨架 | `its-infra`、`its-model`、`its-data`、`its-agent`、`its-knowledge` 五个工程域，共 14 个二级子目录 |
| 2 | samples 跨域样例模板 | `samples/_template/`，含 README、requirements、data/README、src/configs/scripts/tests 占位 |
| 3 | 文档体系 | 项目 README、文档导航、架构设计、开发规范、样例规范、贡献指南、治理规范 |
| 4 | 开源治理与合规文件 | LICENSE、CONTRIBUTING、SECURITY、CHANGELOG、AGENTS、OAT.xml、pyproject.toml、requirements.txt 等 |
| 5 | 仓库级测试与检查脚本 | `tests/test_smoke.py` 共 12 个测试函数、33 个参数化用例；`scripts/check.sh`、`scripts/oat_check.sh` |
| 6 | PR 流水线配置 | `.gitcode/workflows/PR-pipeline_its-trip-samples.yml`，含 PreBuild + CodeCheck 两个 stage |
| 7 | QA 评审材料 | `docs/its-trip-samples-qa-评审.pptx`，评审演示材料，不参与代码执行 |

### 测试活动

本次测试活动包括：README 与文档评估、仓库骨架与工程域检查、samples 模板检查、根级开源文件检查、许可证/合规/版权头检查、Markdown 文档质量检查、GitCode workflow YAML 检查、ruff/black 静态检查、日常流水线 CI 安全扫描结果确认，以及连续 3 次 pytest 可靠性复跑。

## 2. 版本测试信息

**硬件和版本要求**

| 项 | 说明 |
| --- | --- |
| 产品型号 | 不涉及（本期无 NPU 运行时测试） |
| 操作系统 | Windows 11 10.0.26200（x86_64） |
| CANN 版本 | 不涉及（仓库级测试不依赖 CANN） |
| Python 版本 | 3.12.10 |
| pytest 版本 | 9.1.1 |
| ruff / black 版本 | ruff 0.17.0 / black 26.10.1 |
| 依赖环境 | 使用已安装 pytest、ruff、black、PyYAML 的 Python 环境；未在全新 venv 中验证 `pip install -r requirements.txt` |
| 安全扫描 | 日常流水线 CI 已扫描并标记通过（本报告未附具体扫描明细） |

测试源码仓：https://gitcode.com/cann/its-trip-samples


## 3. 测试结论

its-trip-samples 完成本期开源测试，共计执行 33 个仓库级测试用例，全部通过；ruff 静态检查与 black 格式检查通过；连续 3 次 pytest 复跑均通过。本期测试范围内 0 缺陷，整体满足仓库骨架、治理与文档范围的开源要求。**建议 QA-SIG 审议通过本期骨架开源发布。**

| 评估维度 | 评估结果 |
| --- | --- |
| 测试用例总数 | 33 个 |
| 测试执行通过率 | 100%（33/33） |
| 测试结论 | 通过（仅限仓库骨架、治理、文档范围） |
| 缺陷数 | 0（本期测试范围内） |
| 可靠性复跑 | 连续 3 次执行，均 33/33 通过 |
| 静态检查 | ruff：All checks passed；black：2 files unchanged |
| 安全扫描 | PASS（日常流水线 CI 已扫描并标记通过） |
| 不适用范围 | 端到端功能、模型精度、性能、运行态可靠性、兼容性 |

## 4. 特性质量评估

| 序号 | 特性 | 测试结论 | 结构 | 模板 | 合规 | 文档 | 测试 | CI |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 五工程域目录骨架 | 通过 | Pass | — | — | Pass | Pass | — |
| 2 | samples 模板与规范 | 通过 | — | Pass | — | Pass | Pass | — |
| 3 | 开源治理与合规文件 | 通过 | — | — | Pass | Pass | Pass | — |
| 4 | 文档体系与链接 | 通过 | — | — | — | Pass | Pass | — |
| 5 | 仓库级测试与检查脚本 | 通过 | — | — | — | — | Pass | — |
| 6 | PR 流水线配置 | 部分通过 | — | — | — | — | Pass（YAML） | Pass |

## 5. 测试用例与结果

### 5.1 仓库骨架与工程域

| 序号 | 测试用例 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 1 | its-infra 工程域 | 目录存在；`AGENTS.md`、`README.md` 存在；`ops/`、`tools/` 子目录存在 | PASS |
| 2 | its-model 工程域 | 目录存在；`AGENTS.md`、`README.md` 存在；`inference/`、`sft/`、`rl/`、`eval/` 子目录存在 | PASS |
| 3 | its-data 工程域 | 目录存在；`AGENTS.md`、`README.md` 存在；`datasets/`、`scripts/` 子目录存在 | PASS |
| 4 | its-agent 工程域 | 目录存在；`AGENTS.md`、`README.md` 存在；`workflow/`、`skills/`、`algorithms/` 子目录存在 | PASS |
| 5 | its-knowledge 工程域 | 目录存在；`AGENTS.md`、`README.md` 存在；`ontology/`、`corpus/`、`retrieval/` 子目录存在 | PASS |

### 5.2 samples 模板

| 序号 | 测试用例 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 6 | 模板 README | `samples/_template/README.md` 存在 | PASS |
| 7 | 模板依赖清单 | `samples/_template/requirements.txt` 存在 | PASS |
| 8 | 模板数据说明 | `samples/_template/data/README.md` 存在 | PASS |
| 9 | 模板源码目录 | `samples/_template/src/.gitkeep` 存在 | PASS |
| 10 | 模板配置目录 | `samples/_template/configs/.gitkeep` 存在 | PASS |
| 11 | 模板脚本目录 | `samples/_template/scripts/.gitkeep` 存在 | PASS |
| 12 | 模板测试目录 | `samples/_template/tests/.gitkeep` 存在 | PASS |

### 5.3 根级开源必备文件

| 序号 | 测试用例 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 13 | LICENSE | 根目录 `LICENSE` 存在 | PASS |
| 14 | README.md | 根目录 `README.md` 存在 | PASS |
| 15 | CONTRIBUTING.md | 根目录 `CONTRIBUTING.md` 存在 | PASS |
| 16 | SECURITY.md | 根目录 `SECURITY.md` 存在 | PASS |
| 17 | CHANGELOG.md | 根目录 `CHANGELOG.md` 存在 | PASS |
| 18 | AGENTS.md | 根目录 `AGENTS.md` 存在 | PASS |
| 19 | .gitignore | 根目录 `.gitignore` 存在 | PASS |
| 20 | .gitattributes | 根目录 `.gitattributes` 存在 | PASS |
| 21 | OAT.xml | 根目录 `OAT.xml` 存在 | PASS |
| 22 | pyproject.toml | 根目录 `pyproject.toml` 存在 | PASS |
| 23 | requirements.txt | 根目录 `requirements.txt` 存在 | PASS |
| 24 | .pre-commit-config.yaml | 根目录 `.pre-commit-config.yaml` 存在 | PASS |

### 5.4 许可证与合规

| 序号 | 测试用例 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 25 | License 文本 | `LICENSE` 包含 CANN Open Software License Agreement Version 2.0 | PASS |
| 26 | OAT.xml 可解析 | 使用 XML 解析器加载 `OAT.xml`，无语法错误 | PASS |
| 27 | pyproject 许可证声明 | 许可证指向 `LICENSE` 文件，未残留 Apache-2.0 声明 | PASS |
| 28 | 源文件版权头 | 所有 `.py` / `.sh` 文件均包含 Copyright 声明 | PASS |

### 5.5 文档质量

| 序号 | 测试用例 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 29 | samples 文档存在 | `samples/README.md`、`docs/STANDARDS-sample.md` 存在 | PASS |
| 30 | README 仓库名 | README 使用 `its-trip-samples`，未残留 `its-trip-app`、`its-dimak` | PASS |
| 31 | Markdown 标题规范 | 31 个 Markdown 文件无手工标题序号 | PASS |
| 32 | Markdown 相对链接 | 31 个 Markdown 文件的相对链接均可解析 | PASS |

### 5.6 CI 配置

| 序号 | 测试用例 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 33 | GitCode workflow YAML | `.gitcode/workflows/PR-pipeline_its-trip-samples.yml` 可被 YAML 解析器加载 | PASS（仅验证 YAML 可加载；PreBuild / CodeCheck 运行日志未获取） |

### 5.7 静态检查与可靠性复跑

| 检查项 | 命令 | 结果 |
| --- | --- | --- |
| Python lint | `python -m ruff check .` | PASS（All checks passed） |
| Python format | `python -m black --check .` | PASS（2 files unchanged） |
| 可靠性复跑第 1 次 | `python -m pytest tests/ -q` | PASS（33 passed，0.33s） |
| 可靠性复跑第 2 次 | `python -m pytest tests/ -q` | PASS（33 passed，0.37s） |
| 可靠性复跑第 3 次 | `python -m pytest tests/ -q` | PASS（33 passed，0.32s） |

### 5.8 构建产物

不涉及。本期为 Python 仓库骨架，无可执行构建产物；`docs/its-trip-samples-qa-评审.pptx` 为评审演示文档，不计入构建产物。

## 6. DFX 专项质量评估

### 6.1 安全测试

| 序号 | 安全测试项 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| S1 | 敏感信息检查 | 对 tracked 文本文件扫描私钥、AK、API Key、口令赋值、Windows/Linux 绝对路径 | PASS（0 命中） |
| S2 | License 与版权头检查 | LICENSE、pyproject 许可证声明、`.py` / `.sh` 版权头 | PASS |
| S3 | 病毒扫描 | 日常流水线 CI 扫描并标记通过 | PASS（日常流水线 CI） |
| S4 | 漏洞扫描 | 日常流水线 CI 扫描并标记通过 | PASS（日常流水线 CI） |
| S5 | 开源片段引用扫描 | 日常流水线 CI 扫描并标记通过 | PASS（日常流水线 CI） |
| S6 | 开源组件扫描 | 日常流水线 CI 扫描并标记通过 | PASS（日常流水线 CI） |
| S7 | 安全编译选项扫描 | Python 仓，无编译产物 | 不适用 |

> 说明：S3–S6 由日常流水线 CI 扫描并标记通过；本报告未附具体扫描报告编号/链接，归档时以 CI 记录为准。

### 6.2 可靠性测试

| 序号 | 可靠性测试项 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| R1 | 重复执行稳定性 | 连续 3 次执行 `python -m pytest tests/ -q`，每次均为 33/33 通过，0 failed / 0 skipped | PASS |

> 本期无运行态服务、构建产物或端到端样例，重复构建、导出、推理稳定性不适用。

### 6.3 兼容性测试

| 序号 | 兼容性测试项 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| C1 | OS 兼容性 | Windows 11 本地执行；社区 CI 配置为 Ubuntu 20.04 容器；Linux 本地未执行 | 部分通过 / 未完全验证 |
| C2 | Python 版本兼容性 | Python 3.12.10 执行；README 要求 Python >= 3.10；3.10 / 3.11 未执行 | 部分通过 |
| C3 | 昇腾 / CANN 兼容性 | 本期无 NPU 运行时用例 | 不适用 / 未验证 |

### 6.4 文档测试

| 序号 | 文档测试项 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| D1 | README 完整性 | 项目概述、源码下载、环境准备、运行测试、目录结构、模块说明、文档导航、贡献指南、安全声明、问题反馈、变更日志、许可证齐全 | PASS |
| D2 | 链接有效性 | 31 个 Markdown 文件的相对链接可解析 | PASS |
| D3 | 标题规范 | 31 个 Markdown 文件无手工标题序号 | PASS |
| D4 | 命令可执行性 | `python -m pytest tests/ -q` 可执行；`pip install -r requirements.txt` 未在全新环境验证 | 部分通过 |
| D5 | 文档一致性 | README“关键特性”中“样例可直接运行并复现”属于目标态表述，与当前骨架阶段存在语义张力 | 建议优化（非阻塞） |

## 7. 测试执行评估

| 测试活动 | 测试结论 | 用例数 | 用例通过率 |
| --- | --- | --- | --- |
| 仓库骨架与工程域 | PASS | 5 | 100% |
| samples 模板 | PASS | 7 | 100% |
| 根级开源文件 | PASS | 12 | 100% |
| 许可证与合规 | PASS | 4 | 100% |
| 文档质量 | PASS | 4 | 100% |
| CI 配置 | PASS（仅 YAML） | 1 | 100% |
| 仓库级测试合计 | PASS | 33 | 100% |
| 静态检查（ruff / black） | PASS | 2 项 | 100% |
| 可靠性复跑 | PASS | 3 次 | 100% |
| 安全测试（本地敏感信息 / License） | PASS | 2 项 | 100% |
| 安全扫描（日常流水线 CI） | PASS | 4 项 | 100% |
| 端到端 / 性能 / 兼容性 | 不适用 / 未验证 | 0 | NA |

## 8. 遗留问题和关键风险

### 8.1 遗留问题统计

| | 问题总数 | 严重 | 主要 | 次要 | 不重要 |
| --- | --- | --- | --- | --- | --- |
| 数目 | 0 | 0 | 0 | 0 | 0 |
| 百分比 | — | — | — | — | — |

### 8.2 遗留问题列表

无。

### 8.3 已知环境差异与测试边界（非本仓缺陷）

- 本期无可执行端到端样例，功能、模型精度、性能、运行态可靠性、兼容性未验证。
- 本地测试环境为 Windows 11；社区 CI 配置为 Ubuntu 20.04 容器，Linux 本地未执行。
- 安全扫描由日常流水线 CI 标记通过；本报告未附具体扫描报告编号/链接，归档时需补充 CI 记录。

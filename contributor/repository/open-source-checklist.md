# 仓库开源条件与目录结构指引

> 本指引描述"开源前仓库本身须具备什么"（条件、目录结构、自查清单）。开源审批流程（QA-SIG/PMC 评审、基础设施审视等时间线与操作步骤）请参阅[新建仓与仓开放操作指引](new-repo-operation-guide.md)。两份文档配合使用：本指引为"验收项"，操作指引为"流程"。

---

## 一、推荐流程（最小必要集）

以下为**所有类型仓库**开源前必须满足的最小条件，无论仓库是 C++ 算子库、纯 Python 包还是文档/配置仓，均需具备：

| 序号 | 条件 | 说明 |
|------|------|------|
| 1 | `LICENSE` | 许可证文件（CANN 2.0 或业界开源友好许可证如 Apache 2.0/MIT/BSD 3-Clause） |
| 2 | `README.md` | 项目入口，须含：概述、源码下载、目录结构、贡献指南链接、安全声明链接、许可证链接、所属SIG链接、问题反馈 |
| 3 | `CONTRIBUTING.md` | 贡献指南，含 Issue/PR 规范 |
| 4 | `SECURITY.md` | 安全声明，含公网地址声明表、文件权限参考 |
| 5 | `.gitignore` | Git 忽略规则 |
| 6 | `OAT.xml` | 开源合规扫描配置 |
| 7 | 安全扫描通过 | 病毒扫描、漏洞扫描、开源片段引用扫描、License 合规检查通过（由 CI 流水线执行，详见[安全检查项](#21-安全合规文件有三方件依赖时必须)） |
| 8 | 权限配置 | `org-info.yaml` 和 `sig-info.yaml` 已配置，贡献者已签署 CLA |
| 9 | 测试报告 | 按[测试报告模板](../testing/test-templates/测试报告模板.md)完成，QA-SIG 评审通过 |

> 以上 9 项是**进入 QA-SIG 评审的门槛**，缺一不可。

---

## 二、完整流程（按仓库类型补充）

在最小必要集的基础上，不同类型的仓库需要额外满足以下条件：

### 2.1 安全合规文件（有三方件依赖时必须）

引入了第三方开源软件的仓库，须额外配置：

| 文件 | 说明 |
|------|------|
| `Third_Party_Open_Source_Software_List.yaml` | 三方件清单（含 url/version/license） |
| `Third_Party_Open_Source_Software_Notice` | 三方件版权与许可证声明文本 |

> 纯文档仓或无三方依赖的仓库不需要配置。三方件引入流程详见[开源三方件维护指南](../third_party/third_party_maintenance.md)。

[版本发布网络安全质量要求](../coding-standards/SecureRelease.md)规定了版本发布网络安全质量要求，开源前须通过 6 项安全检查：

| 检查项 | 通过标准 | 适用范围 | 检查方 |
|--------|---------|---------|--------|
| 病毒扫描 | 无疑似病毒提示，有则需清理或澄清为误报 | 所有仓 | [安全SIG](../../CANN/sigs/security/README.md) |
| 漏洞扫描 | 所有漏洞已修复或已备案（含业界无解决方案的 CVE） | 所有仓 | [安全SIG](../../CANN/sigs/security/README.md) |
| 安全编译选项扫描 | "要求类"编译选项全部实施，不适用的需评审备案 | 有编译产物的仓 | [安全SIG](../../CANN/sigs/security/README.md) |
| 开源片段引用扫描 | 无开源片段引用问题 | 所有仓 | [安全SIG](../../CANN/sigs/security/README.md) |
| 开源软件 License 合规检查 | 自身 License 正确，引入的 License 无冲突 | 所有仓 | [安全SIG](../../CANN/sigs/security/README.md) |
| 开源组件扫描 | 引入的开源组件为上游社区长期维护的稳定版本 | 有三方依赖的仓 | [安全SIG](../../CANN/sigs/security/README.md) |

> **工具与证据链**：上述安全检查项由社区 CI 流水线（门禁/每日构建）自动执行，开发者可通过流水线日志获取扫描结果。如需人工复核或工具支持，请在 [安全SIG](../../CANN/sigs/security/README.md) 例会申报议题沟通。

`Third_Party_Open_Source_Software_List.yaml` 配置示例（来自[开源三方件维护指南](../third_party/third_party_maintenance.md)）：

```yaml
observability:          # 顶层公共节点
    eigen:              # 软件包名称
        url: https://gitlab.com/libeigen/eigen.git   # 官方获取地址
        version: 3.4.0  # 版本号
        license: Mozilla Public License Version 2.0  # 许可证信息
```

`Third_Party_Open_Source_Software_Notice` 声明示例：

```
Copyright Notice and License Texts
Software: protobuf v3.13.0
Copyright notice:
Copyright 2008 Google Inc.
....
License: BSD 3-Clause License
Copyright (c) All rights reserved.
...
```

> **三方件引入流程**：详见[开源三方件维护指南](../third_party/third_party_maintenance.md)与[三方件建仓及分支命名指导](../third_party/third-party-repo-branch-guide.md)，以及[新建仓与仓开放操作指引](new-repo-operation-guide.md)常见问题 Q4。

### 2.2 编译构建（C++/混合仓必须，纯 Python 仓不适用）

有 C/C++ 编译产物的仓库（如算子库、运行时库）须额外具备：

| 文件/目录 | 说明 |
|----------|------|
| `build.sh` | 编译入口脚本，支持 `--help` 查看选项 |
| `CMakeLists.txt` | 顶层 CMake 构建文件 |
| `cmake/` | CMake 模块与三方件引用配置 |
| `version.cmake` | 版本定义 |

> 纯 Python 仓（如 PyPTO 算子、gauss-splat）使用 `setup.py` / `pyproject.toml` + `requirements.txt` 替代 CMake 构建体系，不需要上述文件。

### 2.3 测试（有可执行逻辑的仓必须）

| 文件/目录 | 说明 |
|----------|------|
| `tests/` | UT 测试目录，**全量 UT 必须通过且日志无 ERROR** |

> 纯文档仓或配置仓（如 community）不涉及可执行逻辑，不需要 tests/ 目录。

### 2.4 文档（有使用门槛的仓推荐）

| 文件/目录 | 说明 |
|----------|------|
| `docs/` | 文档目录（含 QUICKSTART、目录结构说明、API 列表等） |

### 2.5 CI 流水线（有编译或测试的仓必须）

仓库须在 `.gitcode/workflows/` 目录下配置 GitCode Action 工作流，至少包含门禁流水线（PR 触发：编译 + UT），每日构建流水线按需配置。可参考 [runtime](https://gitcode.com/cann/runtime/tree/master/.gitcode/workflows) 仓的流水线配置（含编译、LLT、代码检查、安全扫描等）。配置流程详见[门禁与版本集成流程指南](ci-guide.md)及[新建仓与仓开放操作指引](new-repo-operation-guide.md)第4.3节。

> 纯文档仓不需要编译和UT配置，但是需要安全合规的扫描。

### 2.6 测试报告要求

须按[测试报告模板](../testing/test-templates/测试报告模板.md)完成报告，覆盖特性质量评估（功能/精度/性能/可靠性/兼容性）、DFX 专项（安全/可靠性/性能/兼容性）、测试覆盖（用例数、通过率 100%）。遗留问题要求：严重/主要问题必须闭环，次要问题需有规避措施和 Roadmap。

> **测试报告归档要求**（见 [QA/test-report/README.md](../../QA/test-report/README.md)）：须在 QA-SIG 会议评审前 2 天通过 PR 提交至 `QA/test-report/`，由 Maintainer/Committer 检视，会议前完成检视问题闭环。评审流程详见[新建仓与仓开放操作指引](new-repo-operation-guide.md)第三节。

### 2.7 权限与组织配置

须在本仓（community）中完成 `org-info.yaml`（仓库归属 SIG）和 `sig-info.yaml`（maintainer/committer）配置，所有贡献者已签署 CLA。配置流程详见[新建仓与仓开放操作指引](new-repo-operation-guide.md)第4.4节及[org-info.yaml文件指导说明](../../CANN/org-info-guidance.md)、[sig-info.yaml文件指导说明](../../CANN/sig-info-guidance.md)。

### 2.8 README 内容正确性要求

QA-SIG 评审会对照开源测试报告"Readme 内容评估"逐项检查：
- 仓中介绍内容与代码实际实现一致（接口、数据类型、芯片支持范围）
- 目录排版合理，逻辑清晰，总览和各子模块映射易获取，跳转准确
- 编译命令、安装命令、测试命令经实际验证可正确执行

---

## 三、推荐目录结构

基于 [ops-math](https://gitcode.com/cann/ops-math)（C++ 算子仓）和 [ops-multimodal-fusion](https://gitcode.com/cann/ops-multimodal-fusion)（纯 Python 仓）等标杆仓的实际结构，推荐目录如下。标注 **[通用]** 的适用于所有仓库，标注 **[C++]** 的仅适用于有 C/C++ 编译产物的仓库，标注 **[Python]** 的仅适用于纯 Python 仓：

```
your-repo/
├── LICENSE                                       # [通用] 许可证（CANN 2.0 或 Apache 2.0/MIT/BSD 3-Clause）
├── README.md                                     # [通用] 项目入口文档
├── CONTRIBUTING.md                               # [通用] 贡献指南
├── SECURITY.md                                   # [通用] 安全声明（含公网地址声明表）
├── .gitignore                                    # [通用] Git 忽略规则
├── OAT.xml                                       # [通用] 开源合规扫描配置
├── Third_Party_Open_Source_Software_List.yaml    # [通用·有依赖时] 三方件清单
├── Third_Party_Open_Source_Software_Notice       # [通用·有依赖时] 三方件版权声明
├── .gitcode/                                     # [通用·有CI时] GitCode Action 流水线配置
│   └── workflows/                                #   工作流定义（门禁编译、UT、安全扫描等）
├── build.sh                                      # [C++] 编译入口脚本
├── CMakeLists.txt                                # [C++] 顶层 CMake
├── cmake/                                        # [C++] CMake 模块与三方件引用
│   └── third_party/
├── version.cmake                                 # [C++] 版本定义
├── .clang-format                                 # [C++·推荐] C++ 代码格式
├── requirements.txt                              # [Python] Python 依赖声明
├── setup.py / pyproject.toml                     # [Python] 打包配置
├── .pre-commit-config.yaml                       # [通用·推荐] 提交前检查钩子
├── CHANGELOG.md                                  # [通用·推荐] 变更记录
├── tests/                                        # [通用·有逻辑时] UT 测试
├── docs/                                         # [通用·推荐] 文档目录
│   ├── QUICKSTART.md                             # 快速入门
│   └── zh/                                       # 中文文档
├── examples/                                     # [通用·推荐] 示例代码
├── scripts/                                      # [通用·推荐] 辅助脚本
├── experimental/                                 # [算子仓·推荐] 实验性特性归档目录
└── <your-ops-categories>/                        # 按业务分类的目录
```

### 各目录说明

**通用必须（所有仓库）**：

| 目录/文件 | 说明 |
|----------|------|
| `LICENSE` | 许可证文件，CANN 仓使用 CANN 2.0，或业界开源友好许可证如 Apache 2.0/MIT/BSD 3-Clause 等 |
| `README.md` | 项目入口，需含完整导航链接 |
| `CONTRIBUTING.md` | 贡献指南，含 Issue/PR 规范 |
| `SECURITY.md` | 安全声明，含公网地址声明表和权限参考 |
| `.gitignore` | Git 忽略规则 |
| `OAT.xml` | 开源合规扫描配置 |

**条件必须（按仓库特征）**：

| 目录/文件 | 说明 | 适用条件 |
|----------|------|---------|
| `Third_Party_Open_Source_Software_List.yaml` | 三方件清单 | 有三方依赖时 |
| `Third_Party_Open_Source_Software_Notice` | 三方件版权声明 | 有三方依赖时 |
| `build.sh` | 编译入口 | C++/混合仓 |
| `CMakeLists.txt` | 顶层 CMake | C++/混合仓 |
| `cmake/` | CMake 模块 | C++/混合仓 |
| `version.cmake` | 版本定义 | C++/混合仓 |
| `requirements.txt` | Python 依赖声明 | Python 仓 |
| `setup.py` / `pyproject.toml` | Python 打包配置 | Python 仓 |
| `tests/` | UT 测试目录 | 有可执行逻辑时 |
| `docs/` | 文档目录 | 有使用门槛时 |
| `.gitcode/workflows/` | GitCode Action 流水线配置（门禁编译、UT、安全扫描等） | 有编译或测试时 |

**推荐（非强制）**：

| 目录/文件 | 说明 |
|----------|------|
| `CHANGELOG.md` | 变更记录 |
| `.clang-format` | C++ 代码格式 |
| `.pre-commit-config.yaml` | 提交前检查 |
| `examples/` | 示例代码 |
| `scripts/` | 辅助脚本 |
| `experimental/` | 实验性特性归档目录（算子仓） |
| `common/` | 公共代码 |
| `install_deps.sh` | 依赖安装脚本 |
| `classify_rule.yaml` | 分类规则 |

---

## 四、开源自查清单

开源提交评审前，请逐项对照以下清单确认：

### 4.1 最小必要集（所有仓库必须）

- [ ] 仓库已经 TSC 评审批准创建（有评审纪要）
- [ ] 已在 community 仓 `org-info.yaml` 中配置仓库归属 SIG
- [ ] 对应 SIG 的 `sig-info.yaml` 已配置 maintainer/committer
- [ ] 所有贡献者已签署 CLA
- [ ] `LICENSE` 文件存在且许可证正确（CANN 2.0 或业界开源友好许可证）
- [ ] `README.md` 内容完整（概述、源码下载、目录结构、贡献指南、安全声明、许可证、所属SIG、问题反馈）
- [ ] `README.md` 中描述与代码实际实现一致
- [ ] `CONTRIBUTING.md` 存在且含完整贡献流程
- [ ] `SECURITY.md` 存在且含公网地址声明表、文件权限参考表
- [ ] `.gitignore` 配置正确
- [ ] `OAT.xml` 已配置
- [ ] 病毒扫描通过
- [ ] 漏洞扫描通过（所有漏洞已修复或已备案）
- [ ] 开源片段引用扫描通过
- [ ] License 合规检查通过
- [ ] 按[测试报告模板](../testing/test-templates/测试报告模板.md)完成报告
- [ ] 在 QA-SIG 会议前 2 天通过 PR 提交至 `QA/test-report/`
- [ ] Maintainer/Committer 检视意见已闭环
- [ ] 测试用例通过率 100%
- [ ] 遗留问题已闭环或有规避措施 + Roadmap

### 4.2 完整集（按仓库类型补充）

**有三方件依赖时**：
- [ ] `Third_Party_Open_Source_Software_List.yaml` 已配置所有三方件
- [ ] `Third_Party_Open_Source_Software_Notice` 已声明所有三方件版权
- [ ] 开源组件扫描通过（引入组件为上游社区长期维护的稳定版本）

**C++/混合仓（有编译产物）**：
- [ ] `build.sh` 编译入口可用，支持 `--help`
- [ ] `CMakeLists.txt` + `cmake/` 构建系统完整
- [ ] `version.cmake` 版本定义存在
- [ ] 安全编译选项扫描通过（"要求类"编译选项全部实施）
- [ ] 门禁流水线（PR 触发）配置完成：编译 + UT
- [ ] 已向 infrastructure 提交编译命令、UT 运行命令

**Python 仓**：
- [ ] `requirements.txt` 依赖声明完整
- [ ] `setup.py` / `pyproject.toml` 打包配置存在

**有可执行逻辑的仓**：
- [ ] `tests/` UT 测试目录存在
- [ ] 全量 UT 通过且日志无 ERROR
- [ ] 特性质量评估覆盖（功能/精度/性能/可靠性/兼容性）
- [ ] DFX 专项覆盖（安全/可靠性/性能/兼容性）

### 4.3 推荐项（非强制，提升仓库质量）

- [ ] `CHANGELOG.md` 存在并维护
- [ ] `.clang-format` / `.pre-commit-config.yaml` 已配置
- [ ] `docs/` 文档目录存在（含 QUICKSTART 等）
- [ ] `examples/` 示例代码
- [ ] `scripts/` 辅助脚本
- [ ] 每日构建流水线配置完成（按需）

---

## 五、参考示例

| 仓库 | 参考价值 |
|------|---------|
| [ops-math](https://gitcode.com/cann/ops-math) | 算子仓标杆，目录结构、文档、合规文件齐全 |
| [runtime](https://gitcode.com/cann/runtime) | 已完成 CI 迁移的标杆仓，`.gitcode/workflows/` 可参考 |
| [ops-nn](https://gitcode.com/cann/ops-nn) | 已完成 CI 迁移的标杆仓 |

| 开源测试报告 | 参考价值 |
|-------------|---------|
| [Gauss-splat仓开源测试报告](../../QA/test-report/Gauss-splat仓开源测试报告.md) | 完整的算子仓开源测试报告范例 |
| [ops-multimodal-fusion仓开源测试报告](../../QA/test-report/ops-multimodal-fusion仓开源测试报告.md) | 含详细 UT 用例和兼容性验证 |
| [ops-solver仓开源测试报告](../../QA/test-report/ops-solver仓开源测试报告.md) | 简化版测试报告范例 |
| [cann-simulator仓开源测试报告](../../QA/test-report/cann-simulator仓开源测试报告.md) | 工具类仓开源测试报告范例 |

---

**相关文档**
- [新建仓与仓开放操作指引](new-repo-operation-guide.md) — 建仓和开源审批流程
- [门禁与版本集成流程指南](ci-guide.md) — CI 流水线配置
- [版本发布网络安全质量要求](../coding-standards/SecureRelease.md) — 安全发布检查标准
- [开源三方件维护指南](../third_party/third_party_maintenance.md) — 三方件全生命周期管理
- [三方件建仓及分支命名指导](../third_party/third-party-repo-branch-guide.md) — 三方件仓库命名与分支规范
- [测试报告模板](../testing/test-templates/测试报告模板.md) — 开源测试报告模板

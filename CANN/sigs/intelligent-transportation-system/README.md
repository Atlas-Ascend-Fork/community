# Intelligent Transportation System SIG

## Welcome

欢迎来到 **Intelligent Transportation System SIG**。

Intelligent Transportation System SIG 是 CANN 社区面向智能交通系统领域的特别兴趣小组，聚焦交通网络优化计算、大模型训练稳定性、交通垂域大模型和交通行业智能应用，推动智能交通系统场景在 CANN / Ascend 生态中的建设、验证与落地。

## 导航

| 模块 | 你可以做什么 |
| --- | --- |
| [了解 (Learn)](#了解-learn) | 了解 SIG 简介、项目目标、技术架构和仓库分工 |
| [交流 (Community)](#交流-community) | 加入例会、邮件列表和社区讨论 |
| [贡献 (Contribute)](#贡献-contribute) | 提交 Issue、Pull Request、文档、样例和测试 |
| [未来规划 (Roadmap)](#未来规划-roadmap) | 了解 SIG 基础建设、场景落地、生态深化三个阶段 |

## 了解 (Learn)

### SIG 简介

本 SIG 旨在联合交通行业企业、高校、科研机构和开发者，围绕智能交通系统中的高性能计算、交通仿真、大模型训练稳定性、交通智能体决策闭环等关键问题，沉淀可复用的开源代码仓、接口规范、样例任务和基础测试流程。

SIG主要面向以下参与者：

- 智能交通、车路协同、交通管控、交通仿真方向的开发者和研究者；
- 希望将交通模型、算法或应用迁移到 CANN / Ascend 生态的工程师；
- 关注大模型稳定训练、推理优化和行业智能体落地的开发者；
- 希望贡献文档、样例、测试、Benchmark 或真实场景验证案例的社区成员。

### 愿景与使命

**愿景：** 建设开放、易用、可复现、可扩展的 CANN 智能交通应用生态，形成智能交通系统领域的算子、工具、模型与应用样例参考体系。

**使命：** 降低交通领域开发者使用 CANN / Ascend 进行模型开发、性能优化、稳定性分析和行业应用验证的门槛，帮助开发者从“运行样例”逐步成长为“贡献代码、共建方案”的社区参与者。

### 技术逻辑

Intelligent Transportation System SIG 由四个方向组成，整体按照“基础计算优化 -> 训练稳定性保障 -> 交通大模型能力 -> 行业应用闭环”的逻辑展开。

| 层次 | 仓库 | 定位 | 关系 |
| --- | --- | --- | --- |
| 1. 矩阵计算基础 | [its-matrix-computation](https://gitcode.com/cann/its-matrix-computation) | 面向昇腾平台的矩阵计算与 GEMM 分块策略优化 | 为交通仿真、模型训练和推理提供高性能计算基础 |
| 2. 大模型稳定性 | [its-stable-llm](https://gitcode.com/cann/its-stable-llm) | 面向大模型训练的 micro-batch 稳定性分析 | 帮助交通大模型训练过程更可观测、更稳定 |
| 3. 交通大模型与决策 | [its-trip](https://gitcode.com/cann/its-trip) | 面向交通事件理解、风险研判、方案生成和仿真验证的核心能力 | 承接计算与稳定性能力，形成交通智能决策引擎 |
| 4. 行业应用验证 | [its-trip-samples](https://gitcode.com/cann/its-trip-samples) | 面向交通行业场景的端到端应用参考实现 | 将模型、算法和工具组织为可运行、可复现、可扩展的应用 |


## 交流 (Community)

### 会议组织

- 会议白板：[Intelligent Transportation System SIG 会议白板](https://etherpad-cann.meeting.osinfra.cn/p/sig-intelligent-transportation-system)
- 公开会议时间：北京时间，两周一次例会，单周周五下午 14:00-14:30，节假日顺延或跳过；
- 议题申报：建议在会前至少 1 天通过会议白板、Issue 或邮件列表提交；
- 会议纪要：会议议题、结论、任务负责人和下一步计划将在 SIG 会议白板中持续维护。

### 邮件列表

- SIG 邮件列表：[intelligent-transportation-system@cann.osinfra.cn](mailto:intelligent-transportation-system@cann.osinfra.cn) 邮件列表用于发布会议通知、议程、会议纪要、版本计划、重要讨论和社区协作事项。

### Discussion

欢迎通过以下方式参与讨论：
- 在相关仓库提交 Issue，描述问题、需求、建议或场景；
- 在 Pull Request 中讨论代码实现、接口设计、测试结果和文档更新；
- 在 SIG 例会中同步任务进展、提出技术问题或认领 Roadmap 任务；
- 通过邮件列表发起跨仓库、跨组织或跨 SIG 的协作讨论。

## 贡献 (Contribute)

### 贡献指南

欢迎交通行业企业、高校、科研机构和个人开发者围绕以下内容参与共建：

- 提交 Issue，反馈问题、需求、场景或改进建议；
- 提交 Pull Request，贡献代码、文档、样例、测试和性能报告；
- 参与 SIG 例会，讨论技术路线、任务进展和阶段成果；
- 贡献可复用的数据处理、计算优化、模型稳定性分析和智能体决策流程示例；
- 提供真实交通场景验证案例、评测指标和业务适配方案。

### Issue

提交 Issue 时建议包含：

- 问题类型：Bug、Feature、Documentation、Question、Good First Issue 等；
- 相关仓库、分支、提交版本和运行环境；
- CANN / Ascend 版本、硬件信息和依赖版本；
- 可复现步骤、最小示例、日志、截图或性能数据；
- 期望结果与实际结果；
- 你希望社区协助的具体问题。

### Pull Request

提交 Pull Request 前建议完成：

- 已关联对应 Issue 或说明变更背景；
- 已在本地完成必要测试，并在 PR 中说明测试结果；
- 已更新 README等文档；
- 代码、配置、数据和文档不包含敏感信息；
- 变更范围尽量聚焦，便于 Review 和合入。

### Code Style

各子仓库应在仓内维护具体代码风格和测试要求。通用建议如下：

- 保持目录结构清晰，示例、源码、测试和文档分层明确；
- 为核心接口、配置项和脚本入口提供必要说明；
- 新增功能应尽量包含测试、示例或结果校验方式；
- 日志与异常信息应便于开发者定位问题；
- 涉及第三方模型、数据集或组件时，应遵循对应许可证要求。

### Review Process

Pull Request 通常按以下流程处理：

1. 贡献者提交 PR，并说明变更背景、测试方式和影响范围。
2. Committer / Maintainer 进行代码、文档、测试和许可证检查。
3. 如需修改，贡献者根据 Review 意见更新 PR。
4. Review 通过后由 Maintainer 或具备权限的 Committer 合入。
5. 对重要变更，在 SIG 例会或邮件列表中同步结论和后续任务。


## 成员

### Maintainer 列表

- 王丽健 [@wanglijian_zjec](https://gitcode.com/wanglijian_zjec), *wanglijian_zjec@126.com*
- 刘志远 [@zhiyuanliu](https://gitcode.com/zhiyuanliu), *zhiyuanl@seu.edu.cn*
- 刘少韦华 [@liushaoweihua1225](https://gitcode.com/liushaoweihua1225), *shaoweihualiu@seu.edu.com*

### Committer 列表

#### its-matrix-computation

- 刘洋 [@ly_evtech](https://gitcode.com/ly_evtech), *thu_ets_ly@tsinghua.edu.cn*
- 王正礼 [@wzlnju](https://gitcode.com/wzlnju), *zhlwang@nju.edu.cn*
- 顾子渊 [@ZG_SEU](https://gitcode.com/ZG_SEU), *gzysqy@163.com*
- 张宏刚 [@Zhang_Honggang](https://gitcode.com/Zhang_Honggang), *zhgang1994@163.com*
- 辛云鹏 [@yx_xlqy](https://gitcode.com/yx_xlqy), *yunpengxin@seu.edu.cn*

#### its-stable-llm

- 安琨 [@Candice_Kun_An](https://gitcode.com/Candice_Kun_An), *kunan@tongji.edu.cn*
- 黄迪 [@dihuangseu](https://gitcode.com/dihuangseu), *dihuang@seu.edu.cn*
- 陈垚 [@chenyao0303](https://gitcode.com/chenyao0303), *chenyao1@bjtu.edu.cn*
- 李宏 [@HongriJiujiu](https://gitcode.com/HongriJiujiu), *213222359@seu.edu.cn*

#### its-trip

- 张玉杰 [@seventeenzhang17z](https://gitcode.com/seventeenzhang17z), *yj_zhang@tongji.edu.cn*
- 孙虎成 [@hucheng0222](https://gitcode.com/hucheng0222), *52381101@qq.com*
- 黄凯 [@huangkai0410](https://gitcode.com/huangkai0410), *kaihuang@seu.edu.cn*
- 徐占东 [@ZhandongXu](https://gitcode.com/ZhandongXu), *zhandong.xu@swjtu.edu.cn*
- 周臻 [@zhenz2020](https://gitcode.com/zhenz2020), *zzhou602@seu.edu.cn*

#### its-trip-samples

- 史云阳 [@JNSYY](https://gitcode.com/JNSYY), *JNSYY@noreply.gitcode.com*
- 周臻 [@zhenz2020](https://gitcode.com/zhenz2020), *zzhou602@seu.edu.cn*
- 张晨洋 [@sunnyzcyyy](https://gitcode.com/sunnyzcyyy), *Sunny_zhang@seu.edu.cn*
- 李沐泽 [@Luz7818](https://gitcode.com/Luz7818), *213230392@seu.seu.cn*



## 未来规划 (Roadmap)

Intelligent Transportation System SIG 将按照 **基础建设、场景落地、生态深化** 三阶段推进。

### 基础建设阶段

- 完成 `its-matrix-computation`、`its-stable-llm`、`its-trip` 三个核心仓库的规范化建设；
- 建立统一工程目录、接口规范、输入输出格式和基础测试流程；
- 梳理 GEMM 分块优化、微批次稳定性分析、交通智能体编排等核心能力；
- 完成与 CANN 社区的初步适配，形成可运行样例、README 文档和基础测试说明。

### 场景落地阶段

- 围绕高速路网在线推演、交通管控决策、交通智能体应用等场景开展验证；
- 打通交通大模型“感知—研判—仿真—下发”闭环流程；
- 推动智能交通系统领域算法、工具链和示例应用在 CANN 生态中的落地。

### 生态深化阶段

- 完善算子库高级功能，包括自动参数搜索、模型压缩、稳定性诊断、智能体流程编排等；
- 建立课程牵引和社区协作相结合的开发者贡献机制；
- 联合交通企业、科研机构和 CANN 社区开发者，形成持续迭代的代码共建机制；
- 发布智能交通系统领域 SIG 年度成果包，包括代码仓、样例任务、技术文档和场景验证报告。






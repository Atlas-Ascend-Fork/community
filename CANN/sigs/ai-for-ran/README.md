# AI for RAN SIG

## 概述

AI for RAN SIG（`ai-for-ran`）是 CANN 社区面向 6G 无线接入网（RAN）智能化的特别兴趣小组，聚焦人工智能与无线接入网的深度融合。本 SIG 面向 6G RAN 物理层与网络协作中的专用 AI 模型，在昇腾硬件平台与适配环境下，构建可运行、可复现、可贡献的开源样例与通信指标复现实验。

本 SIG 面向 6G 通信 AI 研究者与高校实验室、昇腾开发者与 CANN 算子/模型适配开发者，以及 RAN 行业生态伙伴，解决通信专用 AI 模型在昇腾平台上缺乏公开适配案例、缺乏基于国产算力的可复现实验等问题。

本 SIG 主要沉淀面向 6G AI RAN 的典型任务样例，覆盖时变信道表征与建模、信道估计、端到端无反馈 MIMO 预编码与多流传输、跨场景智能定位与多基站协作传输等方向，并可进一步拓展至基站智慧节能、移动性管理等 AI for RAN 应用。底层算子、驱动及系统能力依托 CANN 社区现有项目和相关 SIG 共同建设。

## 工作目标 (Goals)

- 建设面向 6G AI RAN 的开源代码仓，沉淀可运行、可复现、可贡献的种子样例与中文文档；
- 围绕信道表征与生成、信道估计、无反馈 MIMO、多基站协作与智能定位等方向，形成 CANN 社区首批通信专用 AI 典型任务集合；
- 围绕昇腾 NPU + CANN 适配形成端到端运行示范，兼容社区现有工具链；
- 以 NMSE、吞吐量、频谱效率等通信 KPI 闭环验证样例效果，形成可量化评估的社区贡献；
- 维护 SIG 相关仓库、成员信息、会议入口、邮件列表和社区协作流程；
- 联合高校、科研机构、产业单位和社区开发者，共同推进昇腾 AI 6G 生态建设。

## 工作愿景 (Vision)

面向 6G 无线接入网智能化场景，建设开放易用、可复现、可贡献的 CANN 通信 AI 应用生态；使能开发者基于 CANN 与昇腾适配环境完成 6G AI RAN 模型样例运行、指标复现与持续贡献，填补通用 AI 算力栈与无线通信算法应用之间的衔接空白，降低通信专用 AI 研究与工程落地成本。

## 职责与范围

AI for RAN SIG 的统一代码仓已创建，仓内计划按研究方向组织子目录。

### 规划目录结构


| 子目录                                  | 职责范围                |
| ------------------------------------ | ------------------- |
| `channel-representation-generation/` | 时变信道表征与扩散式生成        |
| `channel-estimation/`                | 信道估计                |
| `feedback-free-mimo/`                | 无反馈 MIMO 预编码与多流传输   |
| `multi-bs-cooperation/`              | 多基站协作传输             |
| `intelligent-localization/`          | 跨场景智能定位             |
| `docs/`                              | 环境配置、运行说明、技术原理与 FAQ |


## 协作边界

- 本 SIG 聚焦 6G RAN 物理层与网络协作中的通信专用 AI 模型、昇腾适配样例、指标复现与社区协作；
- 底层算子、驱动、编译、运行时及基础系统能力依托 CANN 社区现有项目和相关 SIG；
- 本次 SIG 创建阶段不向 CANN 主仓引入三方件；样例运行所需的 Python / PyTorch 昇腾适配环境等仅在文档中说明。

## 成员

### Maintainer 列表

- 周海波 [@gcw_u7SnCGH7](https://gitcode.com/gcw_u7SnCGH7), *[haibozhou@nju.edu.cn](mailto:haibozhou@nju.edu.cn)*
- 张朝阳 [@zuzy-2012](https://gitcode.com/zuzy-2012), *[diccenter@zju.edu.cn](mailto:diccenter@zju.edu.cn)*
- 陈嘉成 [@chenjch](https://gitcode.com/chenjch), *[jiacheng1989@gmail.com](mailto:jiacheng1989@gmail.com)*

### Committer 列表

- 柳景博 [@JLiu](https://gitcode.com/JLiu), *[jingboliu@nju.edu.cn](mailto:jingboliu@nju.edu.cn)*
- 石宇航 [@Yuhang_Shi](https://gitcode.com/Yuhang_Shi), *[yuhangshi@smail.nju.edu.cn](mailto:yuhangshi@smail.nju.edu.cn)*
- 孙泽宇 [@weixin_46675887](https://gitcode.com/weixin_46675887), *[zeyusun@smail.nju.edu.cn](mailto:zeyusun@smail.nju.edu.cn)*
- 周伟杰 [@qq_56352737](https://gitcode.com/qq_56352737), *[wj_zhou@zju.edu.cn](mailto:wj_zhou@zju.edu.cn)*
- 安通 [@AnnBurger](https://gitcode.com/AnnBurger), *[antoon@zju.edu.cn](mailto:antoon@zju.edu.cn)*
- 刘宗熙 [@weixin_44863193](https://gitcode.com/weixin_44863193), *[1754627980@qq.com](mailto:1754627980@qq.com)*
- 王宁 [@WNNWLL](https://gitcode.com/WNNWLL), *[ning22668800@gmail.com](mailto:ning22668800@gmail.com)*

## 仓库清单

- 统一代码仓：[ai-for-ran](https://gitcode.com/cann/ai-for-ran)。

## 社区运作

### 会议组织

- 会议白板：[AI for RAN SIG 会议白板](https://etherpad-cann.meeting.osinfra.cn/p/sig-ai-for-ran)
- 公开会议频率：北京时间，每月一次线上例会，具体时间以会议白板通知为准
- [CANN 社区会议平台](https://meeting.osinfra.cn/cann/)

### 邮件列表

- 计划邮件列表：[ai-for-ran@cann.osinfra.cn](mailto:ai-for-ran@cann.osinfra.cn)

邮件列表申请完成后，将在本页面补充正式订阅说明。

## 贡献指南

欢迎高校、科研机构、产业单位和个人开发者参与 AI for RAN SIG 共建。

社区成员可以通过以下方式参与：

- 在相关仓库提交 Issue，反馈问题、需求或改进建议；
- 提交 Pull Request，贡献代码、文档、模型样例和测试用例；
- 参与 SIG 例会，讨论技术路线、样例适配和项目进展；
- 贡献通信 KPI 复现实验、昇腾适配经验和技术文档；
- 参与昇腾平台上的模型迁移、性能分析和优化工作。

## 未来规划

AI for RAN SIG 围绕信道表征与估计、无反馈 MIMO 预编码与多流传输、跨场景智能定位与多基站协作三个主题，按层次推进样例建设。

### 信道表征与估计

- 完成统一代码仓 `ai-for-ran` 中信道相关子目录与文档框架建设；
- 沉淀时变信道表征、扩散式生成与信道估计种子样例；
- 提供昇腾环境配置、运行脚本、最小测试数据和 NMSE 等指标复现说明。

### 无反馈 MIMO 预编码与多流传输

- 在信道侧样例基础上，构建无反馈 MIMO 预编码与多流传输种子样例；
- 打通复值神经网络与强化学习决策在昇腾适配环境下的运行链路；
- 形成吞吐量等通信 KPI 的复现实验与使用文档。

### 跨场景智能定位与多基站协作

- 完成跨场景智能定位与多基站协作传输样例构建；
- 串联前述信道与传输能力，形成可运行、可复现的首批样例集合；
- 根据社区反馈持续完善文档与易用性，并向 TSC 汇报建设进展。

## License

SIG 仓库采用 Apache License 2.0 开源
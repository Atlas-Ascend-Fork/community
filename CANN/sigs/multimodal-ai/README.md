# Multimodal-AI SIG

## 概述

Multimodal-AI SIG 是 CANN 社区面向多模态智能计算领域的特别兴趣小组。SIG 以多模态算子为核心，从典型多模态模型的实际计算需求出发，开展模型计算图与关键计算链路拆解，识别具有共性、高性能需求或国产化适配价值的多模态算子，推动算子的抽象、实现、融合与优化。

在算子建设基础上，SIG 使用新算子重构典型多模态模型 Sample，验证算子在真实模型计算链路中的功能与性能收益；同时建设统一的 Benchmark，对多模态算子及重构后的多模态模型进行功能、精度、性能、回归和跨平台对比评测，形成“模型需求拆解—算子建设—模型重构—评测反馈—算子迭代”的协同闭环。

## 愿景与使命

### 愿景

面向多模态模型在昇腾平台上的高效运行需求，建设以高性能多模态算子为核心、模型 Sample 与 Benchmark 协同支撑的开放技术生态。

### 使命

从真实多模态模型中持续识别关键算子需求，沉淀可复用的高性能算子，形成基于新算子的模型重构 Sample 和统一评测基线，降低多模态模型在昇腾平台上的算子开发、模型重构与性能验证成本。

## 工作目标

* 分析典型多模态模型的计算图、关键算子、异构数据流和性能瓶颈，形成面向多模态场景的算子需求；
* 抽象多模态模型中的共性计算模式，建设编码、融合、几何处理和扩散计算等可复用算子；
* 开展多模态算子的生成、改写、融合与性能优化，持续提升算力利用率和数据搬运效率；
* 使用新算子重构典型多模态模型，沉淀可运行、可复现的模型 Sample；
* 建设统一的多模态 Benchmark，评测算子及重构后模型的功能、精度和性能；
* 通过 Benchmark 反馈算子缺陷与性能瓶颈，推动算子和模型 Sample 持续迭代；
* 建立清晰的仓库边界、贡献规范、维护机制和版本演进路线。

## 技术闭环

Multimodal-AI SIG 围绕以下技术闭环开展建设：

1. 从典型多模态模型和应用场景出发，拆解模型计算图、关键算子、异构数据流及性能瓶颈；
2. 将模型中的共性计算模式抽象为可复用的多模态算子，开展实现、融合与性能优化；
3. 使用新算子重构典型多模态模型 Sample，验证算子在真实模型链路中的适用性与收益；
4. 对多模态算子和重构后的多模态模型进行统一 Benchmark 评测；
5. 根据功能、精度和性能评测结果，持续反馈并优化算子实现与模型重构方案。

## 仓库与职责范围

SIG 以 `multimodal-ops` 算子仓为核心：从典型多模态模型中提炼关键计算模式，抽象并实现面向昇腾的高性能多模态算子；在此基础上，`multimodal-samples` 使用这些新算子重构典型多模态模型，验证算子在真实模型链路中的功能与性能收益；而 `multimodal-benchmark` 则贯穿整个过程，提供算子提炼、实现优化、功能精度与性能评测所需的工具链和基准数据，将评测结果反馈给算子和模型的持续迭代。

| 仓库                                                                | 定位            | 职责范围                                                         |
| ----------------------------------------------------------------- | ------------- | ------------------------------------------------------------ |
| [multimodal-ops](https://gitcode.com/cann/multimodal-ops)         | 多模态算子核心仓      | 沉淀从多模态模型中抽象出的关键算子和融合算子，开展算子实现、生成、改写、融合及性能优化                  |
| [multimodal-samples](https://gitcode.com/cann/multimodal-samples) | 模型重构 Sample 仓 | 使用 `multimodal-ops` 中的新算子重构典型多模态模型，提供可运行、可复现的模型 Sample 和使用示例 |
| [multimodal-benchmark](https://gitcode.com/cann/multimodal-benchmark)     | 多模态拆解与评测仓     | 拆解典型多模态模型中的算子需求，沉淀测试工具、数据、规则与评测基线，统一评测多模态算子及重构后模型的功能、精度和性能   |

### multimodal-ops

`multimodal-ops` 是 SIG 的核心仓库，主要包括：

* 多模态模型关键计算模式的算子抽象；
* 编码、融合、几何处理和扩散计算等多模态算子；
* 面向 Ascend C、Triton-Ascend 等技术路线的算子实现；
* 算子生成、改写、融合和性能优化；
* 算子接口、语义、输入输出和适用范围说明；
* 算子功能、精度和性能测试所需的基础用例。

### multimodal-samples

`multimodal-samples` 不作为通用模型仓库，主要用于展示和验证新算子在真实多模态模型中的应用，包括：

* 基于 `multimodal-ops` 新算子重构的典型多模态模型 Sample；
* 新旧计算链路的替换方式和模型重构方案；
* 模型运行、配置、部署和复现实例；
* 新算子接入前后的功能、精度与性能结果；
* 面向开发者的算子使用示例和模型重构最佳实践。

### multimodal-benchmark

`multimodal-benchmark` 统一承载多模态模型拆解、测试工具、评测规则和评测资产，主要包括：

* 典型多模态模型计算图和关键计算链路拆解；
* 多模态算子需求识别、分类和优先级分析；
* 多模态算子的功能、精度、性能和回归评测；
* 重构后多模态模型的端到端功能、精度和性能评测；
* 统一测试数据、测试协议、指标体系和评测基线；
* 跨实现、跨版本和跨平台对比；
* 评测结果分析及面向算子优化的反馈。

## 协作边界

* 本 SIG 聚焦多模态模型中的关键计算模式、算子建设、模型重构 Sample 和统一评测；
* `multimodal-ops` 负责算子资产，`multimodal-samples` 负责基于新算子的模型重构示例，`multimodal-benchmark` 负责需求拆解和统一评测；
* 通用模型工程、完整模型产品和与算子无关的应用功能不纳入本 SIG 的主要范围；
* CANN 底层编译、运行时、驱动及通用基础能力依托社区现有项目和相关 SIG 协同建设；
* 已有模型、算子及评测资产的迁移和归属，按照 CANN 社区治理流程及相关项目协作结果推进。

## 成员

### Maintainer 列表

* 陈振宇 [@gcw_9tG1ncgm](https://gitcode.com/gcw_9tG1ncgm)，*[zychen@nju.edu.cn](mailto:zychen@nju.edu.cn)*
* 王伟 [@willtongji](https://gitcode.com/willtongji)，*[wwang@dase.ecnu.edu.cn](mailto:wwang@dase.ecnu.edu.cn)*
* 孙若愚 [@sundirac](https://gitcode.com/sundirac)，*[sunruoyu@cuhk.edu.cn](mailto:sunruoyu@cuhk.edu.cn)*

### Committer 列表

* 房春荣 [@Chunrong](https://gitcode.com/Chunrong)，*[fangchunr@nju.edu.cn](mailto:fangchunr@nju.edu.cn)*
* 陈淙靓 [@chcoliang](https://gitcode.com/chcoliang)，*[chencongliang@slai.edu.cn](mailto:chencongliang@slai.edu.cn)*
* 王祥丰 [@xfwang_ecnu](https://gitcode.com/xfwang_ecnu)，*[xfwang@cs.ecnu.edu.cn](mailto:xfwang@cs.ecnu.edu.cn)*
* 丁添 [@dingtian_sribd](https://gitcode.com/dingtian_sribd)，*[dingtian@autokernel.cn](mailto:dingtian@autokernel.cn)*
* 张犬俊 [@gcw_yVZogt1f](https://gitcode.com/gcw_yVZogt1f)，*[quanjunzhang@njust.edu.cn](mailto:quanjunzhang@njust.edu.cn)*
* 刘佳玮 [@keloJW](https://gitcode.com/keloJW)，*[jwliu@nju.edu.cn](mailto:jwliu@nju.edu.cn)*
* 王林木 [@llimwang](https://gitcode.com/llimwang)，*[wanglinmu@huawei.com](mailto:wanglinmu@huawei.com)*
* 雷森 [@zhuxiaosixu](https://gitcode.com/zhuxiaosixu)，*[leisen@huawei.com](mailto:leisen@huawei.com)*
* 李恒琼 [@bjisdbvjhbsdvk](https://gitcode.com/bjisdbvjhbsdvk)，*[870124465@qq.com](mailto:870124465@qq.com)*
* 姜耀国 [@jiangyaoguo](https://gitcode.com/jiangyaoguo)，*[jiangyaoguo@outlook.com](mailto:jiangyaoguo@outlook.com)*
* 周强 [@weixin_49894702](https://gitcode.com/weixin_49894702)，*[313670770@qq.com](mailto:313670770@qq.com)*
* 王思议 [@Morgan121250](https://gitcode.com/Morgan121250)，*[morgan121250@qq.com](mailto:morgan121250@qq.com)*
* 宋恺 [@songkai111](https://gitcode.com/songkai111)，*[songkai16@huawei.com](mailto:songkai16@huawei.com)*
* 高新宇 [@qq_33935895](https://gitcode.com/qq_33935895)，*[xinyugao@smail.nju.edu.cn](mailto:xinyugao@smail.nju.edu.cn)*

## 社区运作

### 会议组织

* 公开会议原则上每月召开一次，具体时间和议题以会议白板通知为准；
* [CANN 社区会议平台](https://meeting.osinfra.cn/cann/)
* [议题申报及会议纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-multimodal-ai)

例会主要跟踪以下内容：

* 多模态模型拆解与算子需求；
* 多模态算子实现、优化和合入进展；
* 基于新算子的模型 Sample 重构进展；
* 算子及重构模型的 Benchmark 建设情况；
* Issue 和 Pull Request 处理情况；
* 社区贡献者和成员变更；
* 与 CANN 社区其他项目及 SIG 的协同事项。

### 邮件列表

* SIG 邮件列表：[multimodal-ai@cann.osinfra.cn](mailto:multimodal-ai@cann.osinfra.cn)

邮件列表用于发布会议通知、议程、会议纪要和 SIG 重要事项。

## 贡献指南

欢迎高校、科研机构、企业和个人开发者参与 Multimodal-AI SIG 共建。社区成员可以通过以下方式参与：

* 提交多模态模型计算图、关键链路和性能瓶颈分析；
* 提交多模态算子需求、算子实现和优化方案；
* 使用新算子重构多模态模型并贡献可复现 Sample；
* 贡献测试数据、测试用例、评测工具和 Benchmark；
* 通过 Issue 反馈问题、需求或改进建议；
* 通过 Pull Request 贡献代码、文档和测试资产；
* 参与 SIG 例会，讨论技术路线、仓库规划和项目进展。

## 建设规划

### 启动阶段

* 完成 SIG 组织和治理信息配置；
* 完成三个仓库的创建与初始化；
* 明确仓库目录、接口、文档和贡献规范；
* 梳理首批多模态模型、算子需求和评测任务。

### 闭环建设阶段

* 拆解典型多模态模型的计算图和关键计算链路；
* 建设首批多模态算子及融合算子；
* 使用新算子完成首批模型 Sample 重构；
* 建立算子与重构模型的基础 Benchmark；
* 打通模型需求、算子建设、模型重构和评测反馈闭环。

### 持续演进阶段

* 每三个月集中更新多模态模型和算子需求；
* 持续吸收新的算子实现、模型 Sample 和评测资产；
* 根据 Benchmark 结果推动算子和模型重构方案迭代；
* 扩展典型多模态场景及社区协作范围；
* 沉淀多模态算子、模型重构和评测方面的社区最佳实践。

## License

SIG 所属仓库原则上采用 Apache License 2.0。所引用的上游模型、数据集及第三方组件遵循其各自许可证，并在对应仓库的 LICENSE 或 NOTICE 文件中进行说明。

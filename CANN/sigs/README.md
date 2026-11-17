# CANN Special Interest Groups (SIGs)

CANN社区由多个Special Interest Groups（SIGs）组成，每个SIG负责特定技术领域或垂直行业的开发、维护和社区协作。以下是当前所有SIG的列表，点击SIG名称可查看详细说明。

| SIG名称 | 简要描述                                                                                   |
|---------|----------------------------------------------------------------------------------------|
| [aal](./aal/README.md) | 领域加速库（Ascend Accelerated Libraries，简称aal）针对昇腾AI平台，提供特定领域的算子、算法、工具实现。                   |
| [ai-for-ran](./ai-for-ran/README.md) | 面向 6G 无线接入网智能化，聚焦信道表征与估计、无反馈 MIMO、多基站协作与智能定位等通信专用 AI 样例。 |
| [ascendc](./ascendc/README.md) | Ascend C是面向昇腾AI处理器的专用算子开发语言，提供对底层芯片的完整编程能力，助力实现算子极致性能。                                 |
| [asnumpy](./asnumpy/README.md) | 深度支持昇腾NPU并高度兼容numpy接口的轻量级Python数学运算库，基于pybind11封装华为Ascend C算子库。                        |
| [biomolecule-computing](./biomolecule-computing/README.md) | 面向生命科学领域，聚焦多组学数据处理、生物分子模拟和生物基础模型训练等核心场景，补齐和完善昇腾原生行业算子能力。                        |
| [cannbot](./cannbot/README.md) | CANN社区Agent智能体兴趣小组，为社区提供AI辅助开发、算子生成、生态建设的智能体最佳实践。                                      |
| [catlass](./catlass/README.md) | 昇腾算子模板库，聚焦于提供高性能矩阵乘类算子基础模板的代码库，负责CATLASS的版本规划与技术方案。                                    |
| [crypto](./crypto/README.md) | 密码学兴趣小组，围绕昇腾NPU打造高性能密码软件库，提供丰富的密码算子与算法实现。 |
| [doc](./doc/README.md) | 管理CANN开源开放项目的文档开发工作，致力于为开发者提供具备竞争力的文档体验。                                               |
| [driver](./driver/README.md) | 专注于CANN生态中驱动软件的设计、开发、维护与性能优化，提供基础驱动、设备管理、资源管理及调度、通信能力等功能。                              |
| [electrical-engineering](./electrical-engineering/README.md) | 电力行业算子库兴趣小组，联合电网、电力行业科研院所、设备厂家等，补齐和完善电力领域在仿真求解、负荷预测、装备巡检等场景的算子库。                       |
| [embodied-ai](./embodied-ai/README.md) | 面向具身智能领域，聚焦机器人操作、运动控制、视觉语言导航、世界模型、3D 感知与重建，以及模型训练、部署、评测和真实机器人硬件适配。                     |
| [financial-engineering](./financial-engineering/README.md) | 面向金融工程垂直领域的特别兴趣小组，聚焦金融AI基础设施的智能化与算力精细化运营需求，覆盖金融时序预测与潮汐调度、大尺寸 MoE 部署推理、金融多模态训推等核心场景。 |
| [framework-adapter](./framework-adapter/README.md) | 聚焦AI框架与昇腾芯片的深度适配，实现主流框架对昇腾硬件的原生支持，提高用户易用性并降低迁移成本。                                      |
| [ge](./ge/README.md) | 图模式研发的技术兴趣小组，聚焦于图编译器与图执行引擎的设计、演进与工程实践，打造开放、易用、性能领先的图编译基础设施。                            |
| [hccl](./hccl/README.md) | 提供集群通信库，开放底层基础通信能力，涵盖集合通信、点到点通信和单边通信等场景通信算子。                                           |
| [infrastructure](./infrastructure/README.md) | CANN社区基础设施聚焦为CANN相关的开源项目提供易用，高效，安全的开发者和用户服务。                                           |
| [intelligent-transportation-system](./intelligent-transportation-system/README.md) | 交通行业垂直领域兴趣小组，聚焦交通大数据分析、交通网络优化计算和交通大模型智能决策等场景，推进交通行业算子库、工具链和示例应用在 CANN 生态中的建设与落地。       |
| [local-ai](./local-ai/README.md) | 基于CANN在Kirin、昇腾等端、边芯片上，提供轻量、低延迟、低内存占用的LLM、VLM等大模型推理能力，含大模型转换工具与端到端推理引擎。 |
| [manufacturing](./manufacturing/README.md) | 面向制造业垂直领域的特别兴趣小组，覆盖工业软件、工业视觉等核心场景，聚焦制造业领域常用的三维视觉算法和智能制造解决方案领域的计算需求。 |
| [material-chemical-engineering](./material-chemical-engineering/README.md) | 面向材料化学、流程工业的垂直领域算子库，聚焦计算仿真、预测两大核心场景，填补通用算子库与工业落地之间的“最后一公里”。                            |
| [multimodal-ai](./multimodal-ai/README.md) | 面向多模态AI场景，以算子开发为基础、典型模型重构为验证、评测工具链与基准数据为反馈牵引，三位一体协同形成多模态计算能力的建设闭环。 |
| [ops-basic](./ops-basic/README.md) | 负责维护和开发深度学习框架中核心、基础算子（数学计算、张量变换、随机数、计算机视觉）的兴趣小组，提供高性能、高可靠性的基础运算组件。                     |
| [ops-linear-algebra](./ops-linear-algebra/README.md) | 算子线性代数领域相关的兴趣小组，负责线性代数基础算子能力建设与维护，如BLAS标准相关线性代数等算子。                                    |
| [ops-nn](./ops-nn/README.md) | 神经网络相关算子研发兴趣小组，负责如矩阵乘、卷积、激活等神经网络常用算子。                                                  |
| [ops-transformer](./ops-transformer/README.md) | 算子transformer领域相关的兴趣小组，负责transformer相关融合算子，如FlashAttention、MoE（Mixture of Experts）等算子。 |
| [oil-gas-engineering](./oil-gas-engineering/README.md) | 油气行业工程兴趣小组，围绕油气勘探、生产、炼化三大核心业务场景开展算子研发，持续补充并完善油气行业高性能计算算子库。                             |
| [pto](./pto/README.md) | 面向AI加速器的高性能编程系统，包括PyPTO编程框架和PTO虚拟指令集，旨在简化算子Kernel开发流程，提供高性能计算执行能力。                     |
| [QA](./QA/README.md) | QA（质量保障）项目团队对CANN社区发布软件进行测试，目标是不断提升CANN社区的发布质量和社区测试能力。                                 |
| [recipes](./recipes/README.md) | 提供拿来即用的算法模型样例，帮助用户简单、快速、高效地使用CANN进行模型开发及优化。                                            |
| [runtime](./runtime/README.md) | 专注于CANN生态中运行时的设计、开发、维护与性能优化，致力于构建高性能、可扩展、开放且面向未来的AI运行时系统。                              |
| [security](./security/README.md) | 致力于提升CANN开源社区的网络安全质量与竞争力，并持续做好应急响应。                                                    |
| [shmem](./shmem/README.md) | 致力于面向昇腾AI集群的分布式共享内存编程库的设计、开发与维护，遵循OpenSHMEM标准，为多机多卡场景提供统一的全局地址空间抽象与高性能通信能力。            |
| [tools](./tools/README.md) | 工具SIG，提供CANN开发、调试、测试等相关工具链支持。                                                          |
| [render](./render/README.md) | 致力于在昇腾AI处理器上实现3D GS、3D MESH等3D表征的高性能可微渲染处理。                                                          |

## 如何参与

每个SIG都有自己的例会、邮件列表和贡献指南。点击对应的SIG链接可查看详细联系方式、工作目标及参与方式。

## 新增SIG

如需新增SIG，请参考[CANN社区SIG治理章程](../../governance/sig-governance.md)提交申请。

# SHMEM SIG

shmem SIG 致力于面向昇腾AI集群的分布式共享内存编程库的设计、开发与维护。该库遵循 OpenSHMEM 标准，并与主流实现技术对齐，为多机多卡场景提供统一的全局地址空间抽象与高性能通信能力。我们提供远程内存访问、通信域管理、内存分配及传输同步等核心功能，通过高效易用的访存接口，支持跨节点全局内存共享，并赋能通算融合等新型算子的开发。该库旨在提升AI集群的通信性能与编程效率，为上层应用构建大容量内存池提供稳定可靠的基础设施支持。shmem SIG 负责该库的技术规划、版本演进与相应的社区支持工作。

# 工作目标

1. 负责分布式共享内存编程库的整体架构设计、功能模块规划、接口规范定义、平台适配策略以及编程模型演进等相关技术路线的制定与管理。
2. 针对库实现与演进过程中的关键技术难题（如通信性能优化、一致性模型、资源管理等），组织研讨并形成解决方案，推动技术架构的持续迭代与长期发展战略的落地。
3. 负责处理开源仓库中的代码缺陷（Bug）、响应用户提交的Issue与功能诉求，维护代码质量，保障库的稳定性与可用性，并协同社区推动问题的解决与改进。

# 成员

## Maintainer 列表

- 李东锋[@mlidongfeng](https://gitcode.com/mlidongfeng), *lidongfeng@huawei.com*
- 包小明[@minibao](https://gitcode.com/minibao), *baoxiaoming@huawei.com*
- 安宝怡[@Joyce_An](https://gitcode.com/Joyce_An), *anbaoyi@huawei.com*
- 石楠翔[@shi_nanxiang](https://gitcode.com/shi_nanxiang), *shinanxiang@huawei.com*
- 尹祺然[@nino888](https://gitcode.com/nino888), *yinqiran1@huawei.com*
- 苏建加[@suqwe](https://gitcode.com/suqwe), *sujianjia@huawei.com*

## Committer 列表

- 朱王逸[@zhu-wangyi](https://gitcode.com/zhu-wangyi), *zhuwangyi@huawei.com*
- 谢彬[@oioring](https://gitcode.com/oioring), *xiebin18@huawei.com*
- 王胜[@victor7wang](https://gitcode.com/victor7wang), *wangsheng325@huawei.com*
- 李绍勋[@lishaoxun](https://gitcode.com/lishaoxun), *lishaoxun1@huawei.com*
- 文敏[@gcw_hhwuOOa5](https://gitcode.com/gcw_hhwuOOa5), *wenmin@huawei.com*
- 叶珍妮[@YeZZzzz1](https://gitcode.com/YeZZzzz1), *yezhenni1@huawei.com*
- 姜新誉[@jiangxinyu3](https://gitcode.com/jiangxinyu3), *jiangxinyu3@hisilicon.com*
- 刘建星[@james88liu](https://gitcode.com/james88liu), *liujianxing1@huawei.com*
- 李宏波[@hyolee](https://gitcode.com/hyolee), *lihongbo14@huawei.com*
- 曹冰洁[@vector5](https://gitcode.com/vector5), *caobingjie@huawei.com*
- 张耘齐[@zhangyunqi](https://gitcode.com/zhangyunqi), *zhangyunqi5@huawei.com*

# 社区运作

- 双周例会，每双周周三 16:00-17:30（北京时间）；首次例会在`2026-01-14`举办，具体时间与调整可关注下方纪要与邮件列表
- [会议地址](https://meeting.huaweicloud.com:36443/#/j/982243344)
- [议题申报](https://etherpad-cann.meeting.osinfra.cn/p/sig-shmem)
- [会议纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-shmem)

# SIG订阅

- [邮件列表](https://mailweb.cann.osinfra.cn/mailman3/lists/shmem.cann.osinfra.cn/)

# 仓库清单

仓库地址：
- https://gitcode.com/cann/shmem
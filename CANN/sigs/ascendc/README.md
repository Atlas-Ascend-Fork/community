# Ascend C SIG
[Ascend C](https://asc.gitcode.com)是面向昇腾AI处理器的专用算子开发语言。它在标准C/C++基础上进行扩展，全面遵循C/C++规范，提供对底层芯片的完整编程能力，助力实现算子极致性能。同时，Ascend C 通过构建多层次编程接口，适应不同场景的算子开发需求，贴近业界开发习惯，显著提升开发效率。

Ascend C总体逻辑架构图如下所示：

<img src="../../../figures/sig/ascendc_architecture.png" alt="架构图"  width="850px" height="580px">

# 工作目标
- 规划与设计 Ascend C 多级编程接口（含 Python 前端），覆盖多样化的算子开发场景，兼顾开发效率与运行性能；
- 探讨并规划 Ascend C 在编译能力、调试与调优等方面的技术路线；
- 组织 Ascend C 算子编程领域技术例会，推动技术讨论与决策落地；
- 处理 Ascend C 相关代码仓的缺陷、问题及用户反馈，响应用户诉求。

# Maintainer列表
- 黄金华[@ascendhjh](https://gitcode.com/ascendhjh), *huangjinhua3@huawei.com*
- 诸葛洵[@xun_zhuge](https://gitcode.com/xun_zhuge), *zhugexun@hisilicon.com*

# 仓库清单
- ### AscDevKit: https://gitcode.com/cann/asc-devkit
  - #### 简介：Ascend C算子编程语言核心仓，提供语言扩展层C API和C++类库，支持异构编译和<<<>>>直调，实现芯片完备编程能力，实现极致性能开发
  - #### Committer 列表：
    - 吴兆麟[@wuzhaolin](https://gitcode.com/wuzhaolin), *wuzhaolin@huawei.com*
    - 田宏民[@horming](https://gitcode.com/horming), *tianhongmin@huawei.com*
    - 李东锋[@mlidongfeng](https://gitcode.com/mlidongfeng), *lidongfeng@huawei.com*
    - 石楠翔[@shi_nanxiang](https://gitcode.com/shi_nanxiang), *shinanxiang@huawei.com*
    - 吴洋[@wuyang_hw](https://gitcode.com/wuyang_hw), *wuyang74@hisilicon.com*
    - 杨厚玉[@houyuyang](https://gitcode.com/houyuyang), *yanghouyu@huawei.com*
    - 陈一源[@chenyiyuan](https://gitcode.com/chenyiyuan), *chenyiyuan5@huawei.com*
    - 张浩[@zhanghao_0689](https://gitcode.com/zhanghao_0689), *zhanghao152@huawei.com*
    - 邓静[@dengjing_aoe](https://gitcode.com/dengjing_aoe), *dengjing20@hisilicon.com*
    - 叶珍妮[@YeZZzzz1](https://gitcode.com/YeZZzzz1), *yezhenni1@huawei.com*
    - 黄铎[@DragonBornHD84](https://gitcode.com/DragonBornHD84), *huangduo4@hisilicon.com*
    - 钱鑫海[@bluesky901](https://gitcode.com/bluesky901), *qianxinhai@huawei.com*
    - 吴林玉[@wulinyu](https://gitcode.com/wulinyu), *wulinyu4@huawei.com*
    - 傅珺[@fujun19](https://gitcode.com/fujun19), *fujun19@hisilicon.com*
    - 艾鑫[@ai_xin](https://gitcode.com/ai_xin), *aixin2@hisilicon.com*
    - 李俊文[@Lycheeeee](https://gitcode.com/Lycheeeee), *lijunwen13@hisilicon.com*
    - 娄雨璇[@louyuxuan](https://gitcode.com/louyuxuan), *louyuxuan@huawei.com*
    - 陈民安[@chenma](https://gitcode.com/chenma), *<chenminan@hisilicon.com>*

- ### AscTools：https://gitcode.com/cann/asc-tools
  - #### 简介：Ascend C调试调优工具仓，主要包括CPU/NPU孪生调试
  - #### Committer 列表：
    - 诸葛洵[@xun_zhuge](https://gitcode.com/xun_zhuge), *zhugexun@hisilicon.com*
    - 王凯[@kevin365](https://gitcode.com/kevin365), *wangkai86@huawei.com*
    - 杨滨华[@yangbinhua](https://gitcode.com/yangbinhua), *yangbinhua1@huawei.com*
    - 杨学斌[@XuebinYang](https://gitcode.com/XuebinYang), *yangxuebin6@hisilicon.com*
    - 廖晓辉[@sjtulxh](https://gitcode.com/sjtulxh), *liaoxiaohui3@hisilicon.com*
    - 王筱治[@wangxiaozhi](https://gitcode.com/wangxiaozhi), *wangxiaozhi2@huawei.com*

- ### PyAsc：https://gitcode.com/cann/pyasc
  - #### 简介：Ascend C提供Python前端完备编程能力，支撑Python开发者实现极致性能算子
  - #### Committer 列表：
    - 秦名扬[@qin437231](https://gitcode.com/qin437231), *qinmingyang@huawei.com*
    - 苏统华[@sutonghua](https://gitcode.com/sutonghua), *tonghuasu@gmail.com*
    - 武震卿[@wuzhenqing](https://gitcode.com/wuzhenqing), *wuzhenqing@stu.hit.edu.cn*
    - 苏建加[@suqwe](https://gitcode.com/suqwe), *sujianjia@huawei.com*
    - 孔琼卓[@kong0808](https://gitcode.com/kong0808), *kongqiongzhuo@huawei.com*
    - 姜新誉[@jiangxinyu3](https://gitcode.com/jiangxinyu3), *jiangxinyu3@hisilicon.com*

- ### ATVC：https://gitcode.com/cann/atvc
  - #### 简介：Ascend C提供Vector算子模板库，助力用户快速实现Vector类算子开发。
  - #### Committer 列表：
    - 吴林玉[@wulinyu](https://gitcode.com/wulinyu), *wulinyu4@huawei.com*
    - 王筱治[@wangxiaozhi](https://gitcode.com/wangxiaozhi), *wangxiaozhi2@huawei.com*
    - 朱梁英[@zhuliangying](https://gitcode.com/zhuliangying), *zhuliangying@huawei.com*
    - 傅珺[@fujun19](https://gitcode.com/fujun19), *fujun19@hisilicon.com*

# 项目路标

- [Ascend C Development Roadmap (2026 Q2)](https://gitcode.com/cann/asc-devkit/issues/316)；
- [Ascend C Development Roadmap (2026 Q3)](https://gitcode.com/cann/asc-devkit/issues/938)；

# TOP外部优秀贡献者
  - 苏统华[@sutonghua](https://gitcode.com/sutonghua), *tonghuasu@gmail.com*
  - 武震卿[@wuzhenqing](https://gitcode.com/wuzhenqing), *wuzhenqing@stu.hit.edu.cn*

# 社区运作

### 会议组织

- 公开的会议时间：北京时间，两周一次例会，双周周五上午11:00-12:00
- [议题申报](https://etherpad-cann.meeting.osinfra.cn/p/sig-ascendc)

### 会议纪要

- [会议地址](https://meeting.osinfra.cn/cann/)
- [会议纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-ascendc)

# SIG订阅

- [邮件订阅](https://mailweb.cann.osinfra.cn/mailman3/lists/ascendc.cann.osinfra.cn/)

# 优秀实践

### asc-tools

- [孪生调试：基于Matmul高阶API快速落地矩阵乘法操作，以轻量Matmul算子为示例，具象化呈现孪生调试能力](https://gitcode.com/cann/asc-tools/tree/master/examples/02_matmul_kernellaunch/)

- [基于ATVC模板库的Elementwise算子实现：以TanhGrad为例，展示如何使用ATVC模板库快速实现ElementWise类算子，并呈现模板库提供的调试调优能力](https://gitcode.com/cann/atvc/tree/master/examples/tanh_grad/)
- [基于ATVC模板库的融合算子实现：以ReluWithReduceSum为例，展示如何使用ATVC模板库实现Reduce和Elementwise融合的算子](https://gitcode.com/cann/atvc/tree/master/examples/relu_with_reduce_sum/)

### pyasc
- [基于pyasc的算子实现：以MatmulLeakyRelu算子为例，展示如何使用pyasc提供的Python编程接口实现Matmul+LeayRelu的算子](https://gitcode.com/cann/pyasc/tree/master/python/tutorials/05_matmul_leakyrelu/)

### 基于Tpipe和TQue的编程实现
- [以Add算子为例，使用Tpipe的抽象模型进行算子开发，并通过TQue管理内存，实现高效的Add操作](https://gitcode.com/cann/asc-devkit/blob/master/examples/00_introduction/01_add/basic_api_tque_add/add.asc)

### 自定义算子开发系列
- [算子Kernel直调极简编程实践](https://mp.weixin.qq.com/s/gxDwV-Q_xA8DkuJdbKvFzA)

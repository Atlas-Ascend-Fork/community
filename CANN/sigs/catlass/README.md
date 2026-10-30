# CATLASS SIG

CATLASS，中文名为昇腾算子模板库，是一个聚焦于提供高性能矩阵乘类算子基础模板的代码库。本SIG负责确定 CATLASS 的版本规划与技术方案。

CATLASS 通过抽象分层的方式将矩阵乘及相关融合算子的实现代码模板化。算子实现可利用已提供的模板组件白盒化组装，模板组件可复用、替换或局部定制修改。各模板组件针对昇腾硬件特点设计，可支持FA等复杂算子运算逻辑在昇腾硬件上的高效流水排布，在上层代码逻辑共享的同时支持面向底层硬件的差异性特化。

CATLASS API 架构图：

<img src="../../../figures/sig/catlass_api_level.png" alt="架构图"  width="80%">

## 工作目标

- 规划与设计 CATLASS 组件模板、算子样例，覆盖多样化的 Gemm 算子开发场景、更全面的昇腾硬件，提升开发效率，提供定制场景极致性能优化案例；
- 组织 CATLASS 技术例会，推动技术讨论与决策落地；
- 处理 CATLASS 相关代码仓的缺陷、问题及用户反馈，响应用户诉求。

## Maintainer列表

- 周浩[@zhouhao176](https://gitcode.com/zhouhao176), *<zhouhao176@huawei.com>*
- 黄鑫[@huangxin361](https://gitcode.com/huangxin361), *<huangxin36@huawei.com>*
- 田行辉[@tianxinghui](https://gitcode.com/tianxinghui), *<tianxinghui@huawei.com>*
- 陆璐[@Lulu_scut](https://gitcode.com/Lulu_scut), *<lul@scut.edu.cn>*
- 周建伟[@zjw666888](https://gitcode.com/zjw666888), *<zhoujianwei4@huawei.com>*
- 肖婷[@xiaoting624](https://gitcode.com/xiaoting624), *<xiaoting11@hisilicon.com>*

## 仓库清单

### CATLASS: [https://gitcode.com/cann/catlass](https://gitcode.com/cann/catlass)

#### 简介：CATLASS 算子模板库主仓，提供 CATLASS 算子模板头文件、使用样例及调试工具等。

#### Committer列表
- 张云淞[@triwooder](https://gitcode.com/triwooder), *<zhangyunsong3@huawei.com>*
- 祝松祥[@weixin_42818618](https://gitcode.com/weixin_42818618), *<zhusongxiang1@huawei.com>*
- 陶源[@yuantao_](https://gitcode.com/yuantao_), *<taoyuan18@huawei.com>*
- 龙吉晖[@longjihui](https://gitcode.com/longjihui), *<longjihui@huawei.com>*
- 孙昊[@sunhao_hw](https://gitcode.com/sunhao_hw), *<sunhao203@huawei.com>*
- 金修浪[@jxlang](https://gitcode.com/jxlang), *<jinxiulang@huawei.com>*
- 龚思维[@gong-siwei](https://gitcode.com/gong-siwei), *<gongsiwei@huawei.com>*（[mstuner_catlass](https://gitcode.com/cann/catlass/blob/master/tools/tuner/README.md)工具**Committer**）
- 陈民安[@chenma](https://gitcode.com/chenma), *<chenminan@hisilicon.com>*
- MarioDrumond[@mdrumond](https://gitcode.com/mdrumond), *<mario.paulo.oliveira@huawei.com>*
- 高道兴[@weixin_63557130](https://gitcode.com/weixin_63557130), *<2829025546@qq.com>*
- 张浩波[@init__zhb__](https://gitcode.com/init__zhb__), *<zhanghaobo6@huawei.com>*
- 倪宇昊[@CheaterAbec](https://gitcode.com/CheaterAbec), *<niyuhao2@huawei.com>*
- 陈昊文[@Chen_HaoWen](https://gitcode.com/Chen_HaoWen), *<chenhaowen12@huawei.com>*

### CATCCOS: [https://gitcode.com/cann/catccos](https://gitcode.com/cann/catccos)

#### 简介：CATCCOS计算-通信融合算子模板库，聚焦于提供高性能计算通信融合类算子基础模板。

#### Committer列表
- 尹祺然[@nino888](https://gitcode.com/nino888), *<yinqiran1@huawei.com>*
- 张云淞[@triwooder](https://gitcode.com/triwooder), *<zhangyunsong3@huawei.com>*
- 李绍勋[@lishaoxun](https://gitcode.com/lishaoxun), *<lishaoxun1@huawei.com>*

## 项目路标

### CATLASS Roadmap

- [CATLASS Roadmap (2026 Q1&Q2)](https://gitcode.com/cann/catlass/issues/136)；
- [CATLASS Roadmap (2026 Q3)](https://gitcode.com/cann/catlass/issues/399)；

### CATCCOS Roadmap

- [CATCCOS Roadmap (2026 Q3)](https://gitcode.com/cann/catccos/issues/14)；

## 社区优秀贡献者

- 华南理工大学 陆璐老师团队
- 科大讯飞 研究院工程组
- 中国海洋大学 王胜科老师团队

## 社区运作

### 会议组织

- 双周例会，每双周周三 16:00-17:30 (北京时间)
  - 首次例会在`2025-10-29`举办，具体时间与调整可关注下方纪要与邮件列表
- 会议地址：[https://meeting.osinfra.cn/cann/](https://meeting.osinfra.cn/cann/)
- 议题申报&会议纪要：[https://etherpad-cann.meeting.osinfra.cn/p/sig-catlass](https://etherpad-cann.meeting.osinfra.cn/p/sig-catlass)

## SIG订阅

- 邮件列表：[https://mailweb.cann.osinfra.cn/mailman3/lists/catlass.cann.osinfra.cn/](https://mailweb.cann.osinfra.cn/mailman3/lists/catlass.cann.osinfra.cn/)

# AAL SIG
## 概述
领域加速库（Ascend Accelerated Libraries，简称aal）针对昇腾AI平台，提供特定领域的算子、算法、工具实现。根据需要每个加速库可以提供不同形式的功能：包括但不限于本领域算子的补充、特定算法或机制、特定辅助类工具等。

## 工作目标

- 愿景：构建面向大语言模型、推荐、AI4S领域的专用加速库
- 负责领域加速库相关组件社区技术发展和决策
- 负责领域加速库相关软件包的规划、升级和维护
- 及时响应领域加速库用户反馈和解决领域加速库相关问题

## 职责范围与核心仓库
本SIG主要负责以下核心仓库的开发与维护：
-  Ascend Transformer Boost
   -  定位：一款高效、可靠的Transformer加速库，基于华为Ascend AI处理器，提供Transformer定制化场景的高性能融合算子。
   -  功能： 其接口功能主要分成三部分：
      -  提供经过优化的融合算子（Operation），用户可以根据需求使用对应的算子完成计算功能。
      -  提供图算子机制，用户根据模型设计对应的图算子，使用加速库提供的原生算子和创建的自定义算子创建图算子，完成相应的计算。
      -  提供插件（Plugin）机制，用户可以根据自己的需求创建自定义的算子。
-  AscendSiPBoost
   -  定位： 一款基于华为Ascend AI处理，专门为信号处理领域设计的高性能算子加速库。
   -  功能： SiP提供基于Ascend硬件、深度优化的高性能算子，针对 Ascend NPU 架构特性做了并行计算与内存复用深度优化，用户可基于提供的高性能算子进行灵活业务编排，支撑通信、雷达、信号处理等场景下的任务处理，满足业务快速部署和计算需求。

-  Ascend Boost Comm
   -  定位： 领域加速库基础公共组件， 提供领域加速库公共功能， 如算子封包、下发等。
   -  功能： 提供算子封包、下发、日志、调测等功能，用户可以基于它快速开发新的领域加速库，而不必重复开发这些功能。


# 成员

## Maintainer List
- 尹祺然[@nino888](https://gitcode.com/nino888), *yinqiran1@huawei.com*
- 徐鲁威[@loov1](https://gitcode.com/loov1), *xuluwei@huawei.com*
- 朱志明[@QK_25415](https://gitcode.com/QK_25415), *zhuzhiming1@huawei.com*
- 张浩[@demoauguste](https://gitcode.com/demoauguste), *zhanghao418@huawei.com*
## Committer List
- 郭炅[@goodpeople233](https://gitcode.com/goodpeople233), *guojiong1@huawei.com*
- 马晨昊[@chenhao-ma](https://gitcode.com/chenhao-ma), *machenhao@cuhk.edu.cn*
- 张天娇[@ztj0209](https://gitcode.com/ztj0209), *zhangtianjiao6@huawei.com*
- 黄俊健[@monologue815](https://gitcode.com/monologue815), *huangjunjian3@huawei.com*
- 邢凯鹏[@kpxing](https://gitcode.com/kpxing), *xingkaipeng@huawei.com*
- 杨东[@east_yang](https://gitcode.com/east_yang), *yangdong48@huawei.com*
- 开腾[@kerten](https://gitcode.com/kerten), *kaiteng1@huawei.com*
- 骆文[@luowen203_gg123](https://gitcode.com/luowen203_gg123), *luowen16@huawei.com*

# 优秀贡献者
*欢迎大家积极贡献成为优秀贡献者*

# 社区运作

## 组织会议

- 公开的会议时间：北京时间，两周一次例会，单周(每月第二、第四周，节假日跳过)周四下午16:00-17:00
- [议题申报](https://etherpad-cann.meeting.osinfra.cn/p/aal)
- [会议地址](https://meeting.osinfra.cn/cann/)

## 联系方式

- [邮件列表](https://mailweb.cann.osinfra.cn/mailman3/lists/aal.cann.osinfra.cn/)

# 项目清单

- Ascend Transformer Boost
  - repository地址：https://gitcode.com/cann/ascend-transformer-boost

- AscendSiPBoost
  - repository地址：https://gitcode.com/cann/sip

- Ascend Boost Comm
  - repository地址：https://gitcode.com/cann/ascend-boost-comm

- ops-fft(快速傅里叶变换算子仓)
  - repository地址：[https://gitcode.com/cann/ops-fft](https://gitcode.com/cann/ops-fft)

- ops-spconv（稀疏卷积算子仓）
  - repository地址：[https://gitcode.com/cann/ops-spconv](https://gitcode.com/cann/ops-spconv)

- ops-df（DataFrame处理仓）
  - repository地址：[https://gitcode.com/cann/ops-df](https://gitcode.com/cann/ops-df)

- ops-gnn（图神经网络算子仓）
  - repository地址：[https://gitcode.com/cann/ops-gnn](https://gitcode.com/cann/ops-gnn)

- mp-ops-opt（数学规划优化求解器仓，提供 LP/MIP/VRP 求解能力）
  - repository地址：[https://gitcode.com/cann/mp-ops-opt](https://gitcode.com/cann/mp-ops-opt)

# 贡献指南
- [贡献指南](CONTRIBUTING.md)

# 优秀实践
- [MindIE-LLM ATB模型推理全流程解析](https://www.hiascend.com/forum/thread-0262186302014847027-1-1.html)

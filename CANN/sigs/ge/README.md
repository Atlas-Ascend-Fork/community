# ge SIG

## 概述

GE SIG 是 CANN 图模式研发的技术兴趣小组，聚焦于**图编译器与图执行引擎的设计、演进与工程实践**。
我们致力于打造**开放、易用、性能领先的图编译基础设施**，并持续推动其与主流 AI 框架和开源生态的深度融合，使开发者能够在昇腾 NPU 上获得**稳定、高效、可持续演进**的图模式体验。

## 工作目标

- 推动图编译与图执行相关技术路线的讨论、沉淀与演进。
- 通过例会、设计评审与技术分享，形成可复用的设计共识与最佳实践。
- 维护 SIG 范围内核心仓库的 Issue、Bug 与用户反馈，保障社区的响应效率与工程质量。

## 职责范围与核心仓库

本SIG 主要负责以下几个核心仓库的开发与维护：

- ge
  - **定位**：GE 是图编译与运行的控制中心，负责计算图的编译、优化与执行调度，是昇腾图模式的核心引擎。
  - **功能**：提供图编译与图执行能力，支持静态 / 动态 shape，包含图融合优化、内存与资源管理、下沉调度等关键机制，并通过统一的 Graph API 支撑用户自主构图与运行。

- metadef
  - **定位**：昇腾图与算子相关的元数据定义仓库，提供跨组件共享的数据结构与接口规范。
  - **功能**：提供算子与图共用的基础数据结构与接口，支持 eager 模式与图模式的统一调用。

- graph-autofusion
  - **定位**：面向昇腾 NPU 的轻量级、解耦式自动融合组件集合，聚焦通过自动融合提升模型执行效率。
  - **功能**：基于 codegen 的 JIT 编译机制实现高效融合与加速，包含 SuperKernel 和 Autofuse 两个组件。

- torchair
  - **定位**：TorchAir（Torch Ascend Intermediate Representation）是 PyTorch 与 GE 之间的图模式桥接组件，使 PyTorch 用户能够在昇腾 NPU 上使用图模式进行推理。
  - **功能**：TorchAir 基于 PyTorch Dynamo 机制工作，将 PyTorch FX 图转换为 GE 计算图，并提供 GE 图在昇腾 NPU 上的编译与执行能力。

- triton-inference-server-ge-backend
  - **定位**：Triton Inference Server 中面向昇腾 NPU 的 GE 推理后端。
  - **功能**：通过 Triton Backend 接口，基于 GE 实现模型在昇腾 NPU 上的图编译与推理执行。

## 边界与协作

本SIG负责的GE仓在CANN架构中位置如下图所示：

![alt text](image.png)

## 成员

### Maintainer列表

- 王涛[@wqtshg_wt](https://gitcode.com/wqtshg_wt), *wangtao123@huawei.com*
- 盛楠[@shengnan666](https://gitcode.com/shengnan666), *titan.sheng@huawei.com*
- 詹隽[@zhanj](https://gitcode.com/zhanj), *zhanjun6@hisilicon.com*

### Committer列表

- 唐群章[@tangqunzhang](https://gitcode.com/tangqunzhang), *tangqunzhang@huawei.com*
- 许亚非[@xuyafei](https://gitcode.com/xuyafei), *yxuyafei3@huawei.com*  
- 王笑天[@wangxiaotian995](https://gitcode.com/wangxiaotian995), *710309755@qq.com*
- 储星[@xchu42](https://gitcode.com/xchu42), *chuxing@huawei.com*
- 赵智慧[@zhaozhihui](https://gitcode.com/zhaozhihui), *zhaozhihui5@huawei.com*
- 李沛洋[@peiyang](https://gitcode.com/peiyang), *lipeiyang@huawei.com*
- 李宁[@lining23666](https://gitcode.com/lining23666), *lining.li@huawei.com*
- 耿超[@kobemini](https://gitcode.com/kobemini), *gengchao4@huawei.com*
- 黄桂军[@stevenaw0](https://gitcode.com/stevenaw0), *huangguijun@huawei.com*
- 薛鹏[@medivh-x](https://gitcode.com/medivh-x), *xuepeng4@huawei.com*
- 赵鑫鑫[@hugo111](https://gitcode.com/hugo111), *zhaoxinxin1@huawei.com*
- 张帆[@zhangfan_hanq](https://gitcode.com/zhangfan_hanq), *tonhi.zhangfan@huawei.com*
- 朱晶晶[@zhujingjing](https://gitcode.com/zhujingjing), *zhujingjing6@huawei.com*
- 丁炜秦[@dingweiqin_57](https://gitcode.com/dingweiqin_57), *d_viking@163.com*
- 劳大钊[@laodazhao1](https://gitcode.com/laodazhao1), *laodazhao@huawei.com*
- 袁野[@jason_yuan_ye](https://gitcode.com/jason_yuan_ye), *y1825181@163.com*
- 李培杰[@arthur_morgan_hw](https://gitcode.com/arthur_morgan_hw), *pjlee@aliyun.com*
- 李俊谕[@lijunyu_111](https://gitcode.com/lijunyu_111), *1005303540@qq.com*
- 刘伟[@liu-wei](https://gitcode.com/liu-wei), *ylovline.liuwei@huawei.com*
- 杨学斌[@XuebinYang](https://gitcode.com/XuebinYang), *yangxuebin@hisilicon.com*
- 廖晓辉[@sjtulxh](https://gitcode.com/sjtulxh), *liaoxiaohui3@hisilicon.com*
- 郭一伟[@guoyiwei1111](https://gitcode.com/guoyiwei1111), *guoyiwei2@huawei.com*
- 于海涛[@yuht9](https://gitcode.com/yuht9), *yuhaitao6@huawei.com*
- 张德鹏[@depeng1994](https://gitcode.com/depeng1994),*zhangdepeng2@huawei.com*
- 李沛洋[@peiyang](https://gitcode.com/peiyang),*lipeiyang@huawei.com*
- 杨永强[@yangyongqiang0606](https://gitcode.com/yangyongqiang0606),*yangyongqiang7@hisilicon.com*
- 夏国正[@Mexyy](https://gitcode.com/Mexyy),*xiaguozheng1@hisilicon.com*
- 许亚飞[@xuyafei](https://gitcode.com/xuyafei),*xuyafei3@huawei.com*
- 张盛杰[@zhang_shengjie](https://gitcode.com/user/zhang_shengjie),*jiesheng.zhang@huawei.com*
- 牛玉虎[@niuyuhu](https://gitcode.com/user/niuyuhu),*niuyuhu1@huawei.com*
- 李玥玮[@liyuewei](https://gitcode.com/user/liyuewei),*liyuewei1@huawei.com*
- 唐豪杰[@tang-haojie](https://gitcode.com/tang-haojie),*tanghaojie1@huawei.com*
- 谢正恺[@ClarkXie](https://gitcode.com/ClarkXie),*xiezhengkai@huawei.com*
- 杜花[@du-hua1024](https://gitcode.com/du-hua1024),*duhua2@huawei.com*
- 郭培安[@guopeian](https://gitcode.com/guopeian),*guopeian1@hisilicon.com*

## 社区运作

### 会议组织

- 公开的会议时间：北京时间，每两周一次例会，单周周五下午14:00-16:00
- [议题申报](https://etherpad-cann.meeting.osinfra.cn/p/sig-ge)

欢迎社区成员提交**技术讨论、设计提案、问题反馈或经验分享**等作为会议议题。

### 会议纪要

- [会议地址](https://meeting.osinfra.cn/cann/)
- [会议纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-ge)

## SIG订阅

- [邮件订阅](https://mailweb.cann.osinfra.cn/mailman3/lists/ge.cann.osinfra.cn/)

## 仓库清单

仓库地址：
- https://gitcode.com/cann/ge
- https://gitcode.com/cann/metadef
- https://gitcode.com/cann/graph-autofusion
- https://gitcode.com/Ascend/torchair
- https://gitcode.com/cann/triton-inference-server-ge-backend

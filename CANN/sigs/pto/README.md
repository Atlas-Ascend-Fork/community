# pto SIG

## 概述

PTO是CANN推出的一款面向AI加速器的高性能编程系统，包括**PyPTO编程框架**和**PTO虚拟指令集**。
该系统旨在简化算子Kernel开发流程，提供高性能计算执行能力，并通过虚拟指令集实现硬件平台的可移植性。

该系统采用PTO（Parallel Tensor/Tile Operation）编程范式，以基于Tile的编程模型为核心设计理念。
通过多层次的计算图表达，将用户构建的AI模型应用从高层次计算图逐步编译成PTO虚拟指令，最终生成目标平台上高效执行的代码。

## 工作目标
- 1、负责PTO的技术路线规划和落地；
- 2、组织PTO例会，引导技术讨论和决策；
- 3、负责周边组织沟通协调，推动落地相关项目；
- 4、负责SIG 仓库权限和邮件列表等基础设施的管理；
- 5、负责社区Bug、issue和邮件列表等渠道反馈的问题分发处理。

## 职责与范围
本SIG主要负责以下仓库的开发与维护：

- [PyPTO框架](https://gitcode.com/cann/pypto)
    - 定位：提供基于Python的高性能算子开发框架
    - 功能：简化算子Kernel开发流程，提供Tile编程模型和计算图编译能力
- [PTO虚拟指令集](https://gitcode.com/cann/pto-isa)
    - 定位：提供硬件无关的虚拟指令集抽象
    - 功能：定义PTO虚拟指令规范，支持跨硬件平台的可移植性

# 成员

### Maintainer列表

- 林嘉树 [@linjiashu](https://gitcode.com/linjiashu), *linjiashu@huawei.com*
- 周若愚 [@zhoubotcam](https://gitcode.com/zhoubotcam), *ruoyu.zhou@hisilicon.com*
- 冯思远 [@syfeng](https://gitcode.com/syfeng), *syfeng@sii.edu.cn*
- 尹杰 [@yinjie27_](https://gitcode.com/yinjie27_), *yinjie27@huawei.com*
- 孙文博 [@WenboCodes](https://gitcode.com/WenboCodes), *sunwenbo1@huawei.com*

### Committer列表

#### PyPTO仓库: https://gitcode.com/cann/pypto

- 张中 [@foundea](https://gitcode.com/foundea), *zhangzhong5@huawei.com*
- 袁野 [@jason_yuan_ye](https://gitcode.com/jason_yuan_ye), *yuanye17@huawei.com*
- 杨旭 [@DCGDDD](https://gitcode.com/DCGDDD) *yangxu14@huawei.com*
- 李东升 [@tsungl4](https://gitcode.com/tsungl4), *lidongsheng4@huawei.com*
- 张广军 [@gguuaanngg](https://gitcode.com/gguuaanngg), *zhangguangjun2@huawei.com*
- 戴振韬 [@dai-zhentao](https://gitcode.com/dai-zhentao), *daizhentao1@hisilicon.com*
- 张越兵 [@zhangyuebing](https://gitcode.com/zhangyuebing), *zhangyuebing@hisilicon.com*
- 胡俊 [@cam_bxh](https://gitcode.com/cam_bxh), *Bee.hujun@huawei.com*
- 杲兴旺 [@gaoxingwang](https://gitcode.com/gaoxingwang), *camuel.gao@huawei.com*
- 张芷萁 [@hw_zhangzhiqi](https://gitcode.com/hw_zhangzhiqi), *zhangzhiqi14@huawei.com*
- 王政 [@wangzheng97](https://gitcode.com/wangzheng97), *wangzheng97@hisilicon.com*
- 丛乾男 [@congqiannan](https://gitcode.com/congqiannan), *congqiannan@huawei.com*
- 余蒙 [@ym-HW](https://gitcode.com/ym-HW), *yumeng21@hisilicon.com*
- 韩君佩 [@codehjp423](https://gitcode.com/codehjp423), *hanjunpei@huawei.com*
- 曹慧林 [@caodongdong](https://gitcode.com/caodongdong), *caohuilin@huawei.com*
- 高翔 [@gaoxiang618](https://gitcode.com/gaoxiang618), *gaoxiang26@huawei.com*
- 王兵 [@wangbing110](https://gitcode.com/wangbing110), *wangbing110@huawei.com*
- 植伟原 [@zhiweiyuan](https://gitcode.com/zhiweiyuan), *zhiweiyuan@huawei.com*
- 刘鑫炜 [@xinweiliu](https://gitcode.com/xinweiliu), *liuxinwei12@huawei.com*
- 马可 [@make_pto](https://gitcode.com/make_pto), *make4@huawei.com*
- 时定坤 [@shi-dingkun](https://gitcode.com/shi-dingkun), *shidingkun1@huawei.com*
- 黄璐 [@lululu40888](https://gitcode.com/lululu40888), *huanglu22@hisilicon.com*

#### GYM仓库: https://gitcode.com/cann/pypto-gym

- 张中 [@foundea](https://gitcode.com/foundea), *zhangzhong5@huawei.com*
- 袁野 [@jason_yuan_ye](https://gitcode.com/jason_yuan_ye), *yuanye17@huawei.com*
- 杨旭 [@DCGDDD](https://gitcode.com/DCGDDD) *yangxu14@huawei.com*
- 李东升 [@tsungl4](https://gitcode.com/tsungl4), *lidongsheng4@huawei.com*
- 杲兴旺 [@gaoxingwang](https://gitcode.com/gaoxingwang), *camuel.gao@huawei.com*
- 王政 [@wangzheng97](https://gitcode.com/wangzheng97), *wangzheng97@hisilicon.com*
- 丛乾男 [@congqiannan](https://gitcode.com/congqiannan), *congqiannan@huawei.com*
- 余蒙 [@ym-HW](https://gitcode.com/ym-HW), *yumeng21@hisilicon.com*
- 韩君佩 [@codehjp423](https://gitcode.com/codehjp423), *hanjunpei@huawei.com*
- 高翔 [@gaoxiang618](https://gitcode.com/gaoxiang618), *gaoxiang26@huawei.com*
- 王兵 [@wangbing110](https://gitcode.com/wangbing110), *wangbing110@huawei.com*
- 刘鑫炜 [@xinweiliu](https://gitcode.com/xinweiliu), *liuxinwei12@huawei.com*
- 刘卢芳 [@liulufang_gitcode](https://gitcode.com/liulufang_gitcode), *liulufang1@hisilicon.com*
- 李圣贤[@li-shengxian3](https://gitcode.com/li-shengxian3), *lishengxian3@hisilicon.com*
- Lim Jiunn Bin [@lim-jiunnbin](https://gitcode.com/lim-jiunnbin), *lim.jiunn.bin@huawei.com*
- Pan Boyi [@pan-boyi](https://gitcode.com/pan-boyi), *panboyi@huawei.com*

#### PTO仓库: https://gitcode.com/cann/pto-isa

- 常先宇 [@changxianyu](https://gitcode.com/changxianyu), *changxianyu@hisilicon.com*
- 陈家乐  [@ChanKaLok](https://gitcode.com/ChanKaLok), *chan.ka.lok@huawei.com*
- 黄星源 [@HuangXingYuan_777](https://gitcode.com/HuangXingYuan_777), *huangxingyuan4@huawei.com*
- 陈金林 [@csjlchen](https://gitcode.com/csjlchen), *chenjinlin1@huawei.com*
- 章海剑 [@Zhanghaijian](https://gitcode.com/Zhanghaijian), *z.zhanghaijian@huawei.com*
- 瞿柯林 [@qukelin](https://gitcode.com/qukelin), *qukelin@huawei.com*
- 钱鑫海 [@bluesky901](https://gitcode.com/bluesky901), *qianxinhai@huawei.com*

#### PyPTO-VSCode仓库: https://gitcode.com/cann/pypto-vscode

- 孙志浩 [@sunmaxwell](https://gitcode.com/sunmaxwell), *sunzhihao1@huawei.com*
- 金文鼎 [@jinwending](https://gitcode.com/jinwending), *jinwending1@huawei.com*

# 社区运作

### 会议组织

- 公开的会议时间：北京时间，两周一次例会，双周(每月第二、第四周)周五下午14:00-16:00
- [议题申报](https://etherpad-cann.meeting.osinfra.cn/p/sig-pto)

### 会议纪要

- [会议地址](https://meeting.osinfra.cn/cann/)
- [会议纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-pto)

### 贡献指南

- [贡献指南](https://gitcode.com/cann/pypto/blob/master/CONTRIBUTION.md)

# SIG订阅

- [邮件订阅](https://mailweb.cann.osinfra.cn/mailman3/lists/pto.cann.osinfra.cn/)

# 仓库清单

仓库地址：
- https://gitcode.com/cann/pypto
- https://gitcode.com/cann/pypto-gym
- https://gitcode.com/cann/pypto-vscode
- https://gitcode.com/cann/pto-isa

# ops-nn SIG
## 概述
ops-nn SIG是神经网络相关算子研发兴趣小组，负责如矩阵乘、卷积、激活等神经网络常用算子。

## 工作目标
- 1、负责神经网络算子领域技术路线规划和落地；
- 2、组织神经网络算子领域例会，引导技术讨论和决策；
- 3、负责周边组织沟通协调，推动落地相关项目；
- 4、负责SIG 仓库权限和邮件列表等基础设施的管理；
- 5、负责社区Bug、issue和邮件列表等渠道反馈的问题分发处理。

## 职责与范围
本SIG主要负责[ops-nn](https://gitcode.com/cann/ops-nn) 和 [ops-tensor](https://gitcode.com/cann/ops-tensor) 仓库的开发与维护：
- ops-nn(神经网络算子)
    - 定位：提供神经网络计算常用算子
    - 功能：开发和管理以下类别的算子：
        - activation（激活类）：提供如relu、gelu等激活类算子
        - control（控制流类）：提供如条件分支、循环等流程控制能力算子，如assert算子
        - conv（卷积类）：提供conv2d等卷积操作类算子
        - foreach（循环操作类）：提供如foreach_abs、foreach_add等遍历计算算子
        - index（索引操作类）：提供index_fill、scatter等索引操作类算子
        - loss（损失函数类）：提供l1_loss、mse_loss等loss计算类算子
        - matmul（矩阵乘类）：提供matmul、batchmatmul等矩阵乘计算类算子
        - norm（归一化类）：提供layer_nrom、batch_norm等数据归一化计算算子
        - optim（优化器类）：提供adamw等优化器类算子
        - pooling（池化类）：提供avgpool、maxpool等池化计算类算子
        - quant（量化操作类）：提供quant、dequant等量化计算类算子
        - rnn（循环神经网络类）：提供rnn计算算子
        - vfusion（融合操作类）：提供vector融合计算类算子

## 边界与协作
为保持清晰的职责划分，ops-nn SIG与社区其他算子兴趣小组紧密协作，但专注于上述核心领域。 本SIG与[ops-basic SIG](../ops-basic/README.md)和[ops-transformer SIG](../ops-transformer/README.md)共同提供深度学习网络服务。本SIG负责ops-nn仓，其中在CANN架构中位置如下图所示：
![alt text](image.png)


# 成员

### Maintainer列表
- 唐玮玮[@tangweiwei2](https://gitcode.com/tangweiwei2), *tangweiwei2@huawei.com*
- 陈琦[@chenqi317](https://gitcode.com/chenqi317), *chenqi317@huawei.com*
- 刘波[@liubo75](https://gitcode.com/liubo75), *liubo75@huawei.com*
- 胡碧霞[@crystalhu](https://gitcode.com/crystalhu), *hubixia1@huawei.com*
- 唐超[@chaotang233](https://gitcode.com/chaotang233), *tangchao47@hisilicon.com*

### Committer列表
- 范其瑞[@fanqirui](https://gitcode.com/fanqirui), *fanqirui1@huawei.com*
- 郑李磊[@lileizheng](https://gitcode.com/lileizheng), *zhenglilei@huawei.com*
- 刘伟[@liu-wei](https://gitcode.com/liu-wei), *lovline.liuwei@huawei.com*
- 王永光[@wangyongguang](https://gitcode.com/wangyongguang), *wangyongguang1@huawei.com*
- 汤磊[@tang-lei01](https://gitcode.com/tang-lei01), *tanglei1@huawei.com*
- 於欣洁[@yu-xinjie62](https://gitcode.com/yu-xinjie62), *yuxinjie1@huawei.com*
- 查建青[@zhajianqing123](https://gitcode.com/zhajianqing123), *zhajianqing@huawei.com*
- 章武[@zhang-wu](https://gitcode.com/zhang-wu), *zhangwu3@huawei.com*
- 商晓波[@sxb154714](https://gitcode.com/sxb154714), *shangxiaobo1@hisilicon.com*
- 王子韬[@wangzitao_leo](https://gitcode.com/wangzitao_leo), *wangzitao4@huawei.com*
- 陈娇[@gitcode-chenjiao](https://gitcode.com/gitcode-chenjiao), *chenjiao31@huawei.com*
- 杜慧萍[@gitee-duhuiping](https://gitcode.com/gitee-duhuiping), *duhuiping@h-partners.com*
- 冯英[@fengying555682](https://gitcode.com/fengying555682), *fengying27@h-partners.com*
- 杨露[@yanglu-1](https://gitcode.com/yanglu-1), *yanglou1@h-partners.com*
- 蔡雯雯[@caiwenwen](https://gitcode.com/caiwenwen), *caiwenwen6@h-partners.com*
- 刘杰[@liujie12345678](https://gitcode.com/liujie12345678), *liujie81@huawei.com*
- 杨阳[@yangyang016](https://gitcode.com/yangyang016), *yangyang306@hisilicon.com*
- 陈昊文[@Chen_HaoWen](https://gitcode.com/Chen_HaoWen), *chenhaowen12@huawei.com*
- 陈风[@chenfeng61](https://gitcode.com/chenfeng61), *chenfeng61@huawei.com*
- 林鹏翔[@LinPX](https://gitcode.com/LinPX), *linpengxiang1@hisilicon.com*
- 余鑫[@yuxin5](https://gitcode.com/yuxin5), *yuxin5@huawei.com*
- 沈承宗[@shenchengzong](https://gitcode.com/shenchengzong), *shengchengzong1@huawei.com*
- 王慈孟[@wangcimeng](https://gitcode.com/wangcimeng), *wangcimeng@huawei.com*
- 陈华锋[@huafeng793](https://gitcode.com/huafeng793), *chenhuafeng2@huawei.com*
- 刘闯[@liuchuangdev](https://gitcode.com/liuchuangdev), *liuchuang51@huawei.com*
- 傅涛[@fullt](https://gitcode.com/fullt), *full.fu@huawei.com*
- 高成[@cheng_gao](https://gitcode.com/cheng_gao), *cheng.gao@huawei.com*
- 任如海[@renruhai](https://gitcode.com/renruhai), *renruhai1@huawei.com*
- 黄迪[@kevin_huang1234](https://gitcode.com/kevin_huang1234), *kevin.huangdi@huawei.com*
- 王星[@wang-xing001](https://gitcode.com/wang-xing001), *wangxing73@huawei.com*
- 徐炳麟[@xubinglin](https://gitcode.com/xubinglin), *xubinglin@huawei.com*
- 苏跃明[@su-yueming](https://gitcode.com/su-yueming), *suyueming@huawei.com*
- 柳宗谷[@LiuZonggu](https://gitcode.com/LiuZonggu), *liuzonggu1@huawei.com*
- 刘泱[@liuyang_806](https://gitcode.com/liuyang_806), *liuyang930@hisilicon.com*
- 曾娟[@zengjuan](https://gitcode.com/zengjuan), *zengjuan2@huawei.com*
- 汤平川[@pingchuantang](https://gitcode.com/pingchuantang), *tangpingchuan@huawei.com*
- 钱泽洪[@qianzehong](https://gitcode.com/qianzehong), *qianzehong@huawei.com*
- 林睿涵[@linruihan](https://gitcode.com/linruihan), *linruihan@huawei.com*
- 石向阳[@shi-xiangyang225](https://gitcode.com/shi-xiangyang225), *2678490361@qq.com*
- 陈兴宇[@chenxingyu18](https://gitcode.com/chenxingyu18), *chenxingyu18@huawei.com*
- 朱如意[@rueenov11](https://gitcode.com/rueenov11), *zhuruyi@huawei.com*
- 赵颖超[@zhaoyingchao2](https://gitcode.com/zhaoyingchao2), *zhaoyingchao1@hisilicon.com*
- 陈展熹[@yourealize](https://gitcode.com/yourealize), *chenzhanxi1@huawei.com*
- 陈律丞[@oscillated](https://gitcode.com/oscillated), *chenlyucheng@huawei.com*
- 上官秦南[@u010470851](https://gitcode.com/u010470851), *shangguanqinnan@huawei.com*
- 鲍超俊[@void_ptr](https://gitcode.com/void_ptr), *baochaojun@huawei.com*
- 杨东[@east_yang](https://gitcode.com/east_yang), *yangdong48@huawei.com*
- 张志伟[@Nice_try](https://gitcode.com/Nice_try), *zhangzhiwei108@huawei.com*

### 细分领域：
### foreach、activation、norm committer列表：
- 查建青[@zhajianqing123](https://gitcode.com/zhajianqing123), *zhajianqing@huawei.com*
- 刘杰[@liujie12345678](https://gitcode.com/liujie12345678), *liujie81@huawei.com*
- 陈昊文[@Chen_HaoWen](https://gitcode.com/Chen_HaoWen), *chenhaowen12@huawei.com*
- 黄迪[@kevin_huang1234](https://gitcode.com/kevin_huang1234), *kevin.huangdi@huawei.com*
- 王星[@wang-xing001](https://gitcode.com/wang-xing001), *wangxing73@huawei.com*
- 苏跃明[@su-yueming](https://gitcode.com/su-yueming), *suyueming@huawei.com*
- 汤平川[@pingchuantang](https://gitcode.com/pingchuantang), *tangpingchuan@huawei.com*
- 钱泽洪[@qianzehong](https://gitcode.com/qianzehong), *qianzehong@huawei.com*
- 陈兴宇[@chenxingyu18](https://gitcode.com/chenxingyu18), *chenxingyu18@huawei.com*
- 陈展熹[@yourealize](https://gitcode.com/yourealize), *chenzhanxi1@huawei.com*
- 上官秦南[@u010470851](https://gitcode.com/u010470851), *shangguanqinnan@huawei.com*
- 杨东[@east_yang](https://gitcode.com/east_yang), *yangdong48@huawei.com*

### quant committer列表：
- 查建青[@zhajianqing123](https://gitcode.com/zhajianqing123), *zhajianqing@huawei.com*
- 商晓波[@sxb154714](https://gitcode.com/sxb154714), *shangxiaobo1@hisilicon.com*
- 王子韬[@wangzitao_leo](https://gitcode.com/wangzitao_leo), *wangzitao4@huawei.com*
- 刘杰[@liujie12345678](https://gitcode.com/liujie12345678), *liujie81@huawei.com*
- 陈昊文[@Chen_HaoWen](https://gitcode.com/Chen_HaoWen), *chenhaowen12@huawei.com*
- 陈风[@chenfeng61](https://gitcode.com/chenfeng61), *chenfeng61@huawei.com*
- 林鹏翔[@LinPX](https://gitcode.com/LinPX), *linpengxiang1@hisilicon.com*
- 王星[@wang-xing001](https://gitcode.com/wang-xing001), *wangxing73@huawei.com*
- 徐炳麟[@xubinglin](https://gitcode.com/xubinglin), *xubinglin@huawei.com*
- 苏跃明[@su-yueming](https://gitcode.com/su-yueming), *suyueming@huawei.com*
- 刘泱[@liuyang_806](https://gitcode.com/liuyang_806/), *liuyang930@hisilicon.com*
- 汤平川[@pingchuantang](https://gitcode.com/pingchuantang), *tangpingchuan@huawei.com*
- 钱泽洪[@qianzehong](https://gitcode.com/qianzehong), *qianzehong@huawei.com*
- 陈展熹[@yourealize](https://gitcode.com/yourealize), *chenzhanxi1@huawei.com*
- 上官秦南[@u010470851](https://gitcode.com/u010470851), *shangguanqinnan@huawei.com*

### control committer列表：
- 刘伟[@liu-wei](https://gitcode.com/liu-wei), *lovline.liuwei@huawei.com*
- 查建青[@zhajianqing123](https://gitcode.com/zhajianqing123), *zhajianqing@huawei.com*

### index、hash committer列表：
- 陈风[@chenfeng61](https://gitcode.com/chenfeng61), *chenfeng61@huawei.com*
- 黄迪[@kevin_huang1234](https://gitcode.com/kevin_huang1234), *kevin.huangdi@huawei.com*
- 王星[@wang-xing001](https://gitcode.com/wang-xing001), *wangxing73@huawei.com*
- 苏跃明[@su-yueming](https://gitcode.com/su-yueming), *suyueming@huawei.com*
- 汤平川[@pingchuantang](https://gitcode.com/pingchuantang), *tangpingchuan@huawei.com*
- 钱泽洪[@qianzehong](https://gitcode.com/qianzehong), *qianzehong@huawei.com*
- 陈兴宇[@chenxingyu18](https://gitcode.com/chenxingyu18), *chenxingyu18@huawei.com*
- 陈展熹[@yourealize](https://gitcode.com/yourealize), *chenzhanxi1@huawei.com*
- 上官秦南[@u010470851](https://gitcode.com/u010470851), *shangguanqinnan@huawei.com*

### vfusion、loss、optim committer列表：
- 於欣洁[@yu-xinjie62](https://gitcode.com/yu-xinjie62), *yuxinjie1@huawei.com*
- 陈风[@chenfeng61](https://gitcode.com/chenfeng61), *chenfeng61@huawei.com*
- 王星[@wang-xing001](https://gitcode.com/wang-xing001), *wangxing73@huawei.com*
- 苏跃明[@su-yueming](https://gitcode.com/su-yueming), *suyueming@huawei.com*
- 汤平川[@pingchuantang](https://gitcode.com/pingchuantang), *tangpingchuan@huawei.com*
- 钱泽洪[@qianzehong](https://gitcode.com/qianzehong), *qianzehong@huawei.com*
- 陈展熹[@yourealize](https://gitcode.com/yourealize), *chenzhanxi1@huawei.com*
- 上官秦南[@u010470851](https://gitcode.com/u010470851), *shangguanqinnan@huawei.com*
- 杨东[@east_yang](https://gitcode.com/east_yang), *yangdong48@huawei.com*

### rnn、pooling committer列表：
- 刘闯[@liuchuangdev](https://gitcode.com/liuchuangdev), *liuchuang51@huawei.com*
- 黄迪[@kevin_huang1234](https://gitcode.com/kevin_huang1234), *kevin.huangdi@huawei.com*
- 王星[@wang-xing001](https://gitcode.com/wang-xing001), *wangxing73@huawei.com*
- 苏跃明[@su-yueming](https://gitcode.com/su-yueming), *suyueming@huawei.com*
- 汤平川[@pingchuantang](https://gitcode.com/pingchuantang), *tangpingchuan@huawei.com*
- 钱泽洪[@qianzehong](https://gitcode.com/qianzehong), *qianzehong@huawei.com*
- 陈兴宇[@chenxingyu18](https://gitcode.com/chenxingyu18), *chenxingyu18@huawei.com*
- 陈展熹[@yourealize](https://gitcode.com/yourealize), *chenzhanxi1@huawei.com*
- 上官秦南[@u010470851](https://gitcode.com/u010470851), *shangguanqinnan@huawei.com*
- 张志伟[@Nice_try](https://gitcode.com/Nice_try), *zhangzhiwei108@huawei.com*

### matmul committer列表：
- 范其瑞[@fanqirui](https://gitcode.com/fanqirui), *fanqirui1@huawei.com*
- 唐超[@chaotang233](https://gitcode.com/chaotang233), *tangchao47@hisilicon.com*
- 商晓波[@sxb154714](https://gitcode.com/sxb154714), *shangxiaobo1@hisilicon.com*
- 王子韬[@wangzitao_leo](https://gitcode.com/wangzitao_leo), *wangzitao4@huawei.com*
- 杨阳[@yangyang016](https://gitcode.com/yangyang016), *yangyang306@hisilicon.com*
- 林鹏翔[@LinPX](https://gitcode.com/LinPX), *linpengxiang1@hisilicon.com*
- 徐炳麟[@xubinglin](https://gitcode.com/xubinglin), *xubinglin@huawei.com*
- 刘泱[@liuyang_806](https://gitcode.com/liuyang_806/), *liuyang930@hisilicon.com*
- 朱如意[@rueenov11](https://gitcode.com/rueenov11), *zhuruyi@huawei.com*
- 赵颖超[@zhaoyingchao2](https://gitcode.com/zhaoyingchao2), *zhaoyingchao1@hisilicon.com*
- 陈律丞[@oscillated](https://gitcode.com/oscillated), *chenlyucheng@huawei.com*
- 鲍超俊[@void_ptr](https://gitcode.com/void_ptr), *baochaojun@huawei.com*

### conv committer列表：
- 郑李磊[@lileizheng](https://gitcode.com/lileizheng), *zhenglilei@huawei.com*
- 余鑫[@yuxin5](https://gitcode.com/yuxin5), *yuxin5@huawei.com*
- 沈承宗[@shenchengzong](https://gitcode.com/shenchengzong), *shengchengzong1@huawei.com*
- 王慈孟[@wangcimeng](https://gitcode.com/wangcimeng), *wangcimeng@huawei.com*
- 陈华锋[@huafeng793](https://gitcode.com/huafeng793), *chenhuafeng2@huawei.com*
- 高成[@cheng_gao](https://gitcode.com/cheng_gao), *cheng.gao@huawei.com*
- 柳宗谷[@LiuZonggu](https://gitcode.com/LiuZonggu), *liuzonggu1@huawei.com*
- 林睿涵[@linruihan](https://gitcode.com/linruihan), *linruihan@huawei.com*
- 陈兴宇[@chenxingyu18](https://gitcode.com/chenxingyu18), *chenxingyu18@huawei.com*
- 张志伟[@Nice_try](https://gitcode.com/Nice_try), *zhangzhiwei108@huawei.com*

### 资料 committer列表
- 陈娇[@gitcode-chenjiao](https://gitcode.com/gitcode-chenjiao), *chenjiao31@huawei.com*
- 杜慧萍[@gitee-duhuiping](https://gitcode.com/gitee-duhuiping), *duhuiping@h-partners.com*
- 冯英[@fengying555682](https://gitcode.com/fengying555682), *fengying27@h-partners.com*
- 杨露[@yanglu-1](https://gitcode.com/yanglu-1), *yanglou1@h-partners.com*
- 蔡雯雯[@caiwenwen](https://gitcode.com/caiwenwen), *caiwenwen6@h-partners.com*

### API committer列表
- 王永光[@wangyongguang](https://gitcode.com/wangyongguang), *wangyongguang1@huawei.com*
- 汤磊[@tang-lei01](https://gitcode.com/tang-lei01), *tanglei1@huawei.com*

### torch_extension committer列表：
- 唐玮玮[@tangweiwei2](https://gitcode.com/tangweiwei2), *tangweiwei2@huawei.com*
- 陈琦[@chenqi317](https://gitcode.com/chenqi317), *chenqi317@huawei.com*
- 刘波[@liubo75](https://gitcode.com/liubo75), *liubo75@huawei.com*
- 胡碧霞[@crystalhu](https://gitcode.com/crystalhu), *hubixia1@huawei.com*
- 范其瑞[@fanqirui](https://gitcode.com/fanqirui), *fanqirui1@huawei.com*
- 唐超[@chaotang233](https://gitcode.com/chaotang233), *tangchao47@hisilicon.com*

# 社区运作

### 会议组织

- 公开的会议时间：北京时间，两周一次例会，周五下午14:15-16:00
- [议题申报](https://etherpad-cann.meeting.osinfra.cn/p/sig-ops-nn)
- [会议地址](https://meeting.osinfra.cn/cann/)

### 会议纪要

- [会议纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-ops-nn)

### 贡献指南
- [贡献指南](https://gitcode.com/cann/ops-nn/blob/master/CONTRIBUTING.md)

# SIG订阅

- [邮件订阅](https://mailweb.cann.osinfra.cn/mailman3/lists/ops-nn.cann.osinfra.cn/)

# 仓库清单

仓库地址：
- https://gitcode.com/cann/ops-nn
- https://gitcode.com/cann/ops-tensor

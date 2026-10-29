# ops-transformer SIG
算子transformer领域相关的兴趣小组，负责transformer相关融合算子，如FlashAttention、MoE（Mixture of Experts）等算子。

## 工作目标
- 1、负责transformer 算子领域技术路线规划和落地；
- 2、组织transformer 算子领域例会，引导技术讨论和决策；
- 3、负责周边组织沟通协调，推动落地相关项目；
- 4、负责SIG 仓库权限和邮件列表等基础设施的管理；
- 5、负责社区Bug、issue和邮件列表等渠道反馈的问题分发处理。

## 职责与范围
本SIG主要负责[ops-transformer](https://gitcode.com/cann/ops-transformer) 和 [ops-tilelang](https://gitcode.com/cann/ops-tilelang) 仓库的开发与维护：
- ops-transformer(transformer算子)
    - 定位：提供transformer相关常用算子
    - 功能：开发和管理以下类别的算子：
        - attention：对应各类attention 推理和训练算子
        - moe：对应MoE计算中，topk计算，合并MoE FFN的输出结果计算和routing计算等算子
        - gmm：对应实现分组矩阵乘计算等算子
        - mc2：对应通算并行算子和MOE 通信dispatch和combine算子
        - posembedding：对应旋转位置编码计算算子
        - ffn：对应MoeFFN和FFN等相关计算算子

# 社区运作

## 组织会议：
两周一次例会，每单周周三下午15:30点-17:30点
- [会议链接](https://meeting.osinfra.cn/cann/)
- [会议议题&纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-ops-transformer)
- [邮件列表订阅](https://mailweb.cann.osinfra.cn/mailman3/lists/ops-transformer.cann.osinfra.cn/)

## 贡献指南
- [贡献指南](https://gitcode.com/cann/ops-transformer/blob/master/CONTRIBUTING.md)

# 成员

## Maintainer列表
- 刘丹 [@liudan12](https://gitcode.com/liudan12), *liudan12@huawei.com*
- 俞郑中 [@Allan_Yu](https://gitcode.com/Allan_Yu), *yuzhengzhong1@huawei.com*
- 黄俊健 [@monologue815](https://gitcode.com/monologue815), *huangjunjian3@huawei.com*
- 马兵 [@mabing1118](https://gitcode.com/mabing1118), *mabing726@huawei.com*
- 蒋礼锐 [@jiang-lirui](https://gitcode.com/jiang-lirui), *jianglirui1@huawei.com*


## Committer列表
- 陈建军 [@chenjianjun11](https://gitcode.com/chenjunjian11), *chenjianjun11@huawei.com*
- 杨彬榕 [@yang-binrong](https://gitcode.com/yang-binrong), *yangbinrong@huawei.com*
- 王民波 [@wang-minbo](https://gitcode.com/wang-minbo), *wangminbo1@hisilicon.com*
- 陈康 [@chenkang30](https://gitcode.com/chenkang30), *chenkang30@huawei.com*
- 宋凯 [@songkai111](https://gitcode.com/songkai111), *songkai16@huawei.com*
- 高翔 [@gaoxiang618](https://gitcode.com/gaoxiang618), *gaoxiang26@huawei.com*
- 黄伟 [@huangwei791](https://gitcode.com/huangwei791), *huangwei791@huawei.com*
- 苗方正 [@miaofangzheng](https://gitcode.com/miaofangzheng), *miaofangzheng@huawei.com*
- 温忻 [@wenxin_fight](https://gitcode.com/wenxin_fight), *wenxin20@hisilicon.com*
- 王永光 [@wangyongguang](https://gitcode.com/wangyongguang), *wangyongguang1@huawei.com*
- 於欣洁 [@yu-xinjie62](https://gitcode.com/yu-xinjie62), *yuxinjie1@huawei.com*
- 俞浩 [@yuhao_](https://gitcode.com/yuhao_), *yuhao93@huawei.com*
- 刘博熙 [@liuboxi](https://gitcode.com/liuboxi), *liuboxi1@huawei.com*
- 唐超 [@chaotang233](https://gitcode.com/chaotang233), *tangchao47@hisilicon.com*
- 胡碧霞 [@crystalhu](https://gitcode.com/crystalhu), *hubixia1@huawei.com*
- 陈琳鑫 [@chen-linxin4](https://gitcode.com/chen-linxin4), *chenlinxin4@huawei.com*
- 赵臣臣 [@cc-z](https://gitcode.com/cc-z), *zhaochenchen11@huawei.com*
- 张硕累 [@zhangshuoleiokok](https://gitcode.com/zhangshuoleiokok), *zhangshuolei1@huawei.com*
- 魏纳川 [@Wei_NaChuan](https://gitcode.com/Wei_NaChuan), *weinachuan1@huawei.com*
- 杨子奇 [@yangziqi_007](https://gitcode.com/yangziqi_007), *yangziqi4@huawei.com*
- 赵志勇 [@zzy__](https://gitcode.com/zzy__), *zhaozhiyong15@hisilicon.com*
- 张海杰 [@haijie_699874](https://gitcode.com/haijie_699874), *zhanghaijie4@hisilicon.com*
- 沈维铃 [@shen_weiling](https://gitcode.com/shen_weiling), *shenweiling@huawei.com*
- 唐浩 [@tang-hao-hw-gitcode](https://gitcode.com/tang-hao-hw-gitcode), *tanghao71@hisilicon.com*
- 鞠阳 [@juyangokok](https://gitcode.com/juyangokok), *juyang@huawei.com*
- 李博浩 [@libohao6](https://gitcode.com/libohao6), *libohao3@huawei.com*
- 陈陆淳 [@macech](https://gitcode.com/macech), *chenluchun1@huawei.com*
- 杨泽恒 [@yangzeheng](https://gitcode.com/yangzeheng), *yangzeheng@huawei.com*
- 罗柏清 [@luobaiqing](https://gitcode.com/luobaiqing), *luobaiqing1@huawei.com*
- 林玮 [@tgwsakiko_](https://gitcode.com/tgwsakiko_), *linwei69@huawei.com*
- 郑雯文 [@Ww7012](https://gitcode.com/Ww7012), *zhengwenwen7@huawei.com*
- 陈娇 [@gitcode-chenjiao](https://gitcode.com/gitcode-chenjiao), *chenjiao31@huawei.com*
- 蔡雯雯 [@caiwenwen](https://gitcode.com/caiwenwen), *caiwenwen6@h-partners.com*
- 杜慧萍 [@gitee-duhuiping](https://gitcode.com/gitee-duhuiping), *duhuiping@h-partners.com*
- 冯英[@fengying555682](https://gitcode.com/fengying555682), *fengying27@h-partners.com*
- 杨露[@yanglu-1](https://gitcode.com/yanglu-1), *yanglou1@h-partners.com*
- 袁滔 [@claire8090](https://gitcode.com/claire8090), *yuantao27@h-partners.com*
- 周云飞 [@zzzzzzyf_](https://gitcode.com/zzzzzzyf_), *zhouyunfei10@huawei.com*
- 林竹 [@coder_linx](https://gitcode.com/coder_linx), *linzhu3@huawei.com*
- 宋炯辉 [@songjionghui](https://gitcode.com/songjionghui), *songjionghui@huawei.com*
- 王哲 [@wangzhe123456789](https://gitcode.com/wangzhe123456789), *wangzhe92@huawei.com*
- 黄立 [@huang_li](https://gitcode.com/huang_li), *huangli84@hisilicon.com*
- 徐柯南 [@kknan](https://gitcode.com/kknan), *xukenan@huawei.com*
- 石睿 [@shi-rui](https://gitcode.com/shi-rui), *shirui17@huawei.com*
- 陈鹏屹 [@cpy_123456](https://gitcode.com/cpy_123456), *chenpengyi@huawei.com*
- 郭秋毫 [@guoqiuhao](https://gitcode.com/guoqiuhao), *guoqiuhao1@huawei.com*
- 吴奕 [@wuyi_huawei](https://gitcode.com/wuyi_huawei), *wuyi36@hisilicon.com*
- 宋智琪 [@captainmiaow](https://gitcode.com/captainmiaow), *songzhiqi1@huawei.com*
- 丁勇 [@xuanyuandy](https://gitcode.com/xuanyuandy), *dingyong19@huawei.com*
- 韩孝斌 [@L_Euler](https://gitcode.com/L_Euler), *hanxiaobin3@huawei.com*
- 周扬帆 [@hz36amy_00](https://gitcode.com/hz36amy_00), *zhouyangfan8@huawei.com*
- 安沙沙 [@shasha_an](https://gitcode.com/shasha_an), *anshasha@hisilicon.com*
- 桂建伟 [@guijianwei](https://gitcode.com/guijianwei), *guijianwei@huawei.com*
- 陆威 [@luwei_1104](https://gitcode.com/luwei_1104), *luwei44@huawei.com*
- 王荀 [@wangxun21](https://gitcode.com/wangxun21), *wangxun21@huawei.com*
- 孔德元 [@kdy18482276080](https://gitcode.com/kdy18482276080), *kongdeyuan3@huawei.com*
- 朱逸君 [@Julius47](https://gitcode.com/Julius47), *zhuyijun8@hisilicon.com*
- 徐诚阳 [@xuchengyang](https://gitcode.com/xuchengyang), *xuchengyang4@huawei.com*
- 陈黄威 [@huang-wei-chen](https://gitcode.com/huang-wei-chen), *chenhuangwei1@huawei.com*
- 蒋家炜 [@jiangjiawei](https://gitcode.com/jiangjiawei), *jiangjiawei10@huawei.com*
- 李宁 [@lining_210](https://gitcode.com/lining_210), *lining210@huawei.com*
- 黄帅 [@huangshuai59](https://gitcode.com/huangshuai59), *huangshuai59@huawei.com*
- 薛靖晖 [@xuejinghui](https://gitcode.com/xuejinghui), *xuejinghui@huawei.com*
- 朱铭哲 [@zhu-mingzhe71](https://gitcode.com/zhu-mingzhe71), *zhumingzhe2@huawei.com*
- 程志炜 [@cheng_zhiwei](https://gitcode.com/cheng_zhiwei), *chengzhiwei10@huawei.com*

## 细分领域：
## moe committer列表：
- 宋凯 [@songkai111](https://gitcode.com/songkai111), *songkai16@huawei.com*
- 陈琳鑫 [@chen-linxin4](https://gitcode.com/chen-linxin4), *chenlinxin4@huawei.com*
- 於欣洁 [@yu-xinjie62](https://gitcode.com/yu-xinjie62), *yuxinjie1@huawei.com*
- 赵臣臣 [@cc-z](https://gitcode.com/cc-z), *zhaochenchen11@huawei.com*
- 魏纳川 [@Wei_NaChuan](https://gitcode.com/Wei_NaChuan), *weinachuan1@huawei.com*
- 鞠阳 [@juyangokok](https://gitcode.com/juyangokok), *juyang@huawei.com*
- 陈鹏屹 [@cpy_123456](https://gitcode.com/cpy_123456), *chenpengyi@huawei.com*
- 郭秋毫 [@guoqiuhao](https://gitcode.com/guoqiuhao), *guoqiuhao1@huawei.com*
- 孔德元 [@kdy18482276080](https://gitcode.com/kdy18482276080), *kongdeyuan3@huawei.com*
- 朱逸君 [@Julius47](https://gitcode.com/Julius47), *zhuyijun8@hisilicon.com*
- 徐诚阳 [@xuchengyang](https://gitcode.com/xuchengyang), *xuchengyang4@huawei.com*
- 程志炜 [@cheng_zhiwei](https://gitcode.com/cheng_zhiwei), *chengzhiwei10@huawei.com*

## mc2 committer列表：
- 陈建军 [@chenjianjun11](https://gitcode.com/chenjunjian11), *chenjianjun11@huawei.com*
- 王民波 [@wang-minbo](https://gitcode.com/wang-minbo), *wangminbo1@hisilicon.com*
- 刘博熙 [@liuboxi](https://gitcode.com/liuboxi), *liuboxi1@huawei.com*
- 李博浩 [@libohao6](https://gitcode.com/libohao6), *libohao3@huawei.com*
- 陈陆淳 [@macech](https://gitcode.com/macech), *chenluchun1@huawei.com*
- 杨泽恒 [@yangzeheng](https://gitcode.com/yangzeheng), *yangzeheng@huawei.com*
- 罗柏清 [@luobaiqing](https://gitcode.com/luobaiqing), *luobaiqing1@huawei.com*
- 林玮 [@tgwsakiko_](https://gitcode.com/tgwsakiko_), *linwei69@huawei.com*
- 宋智琪 [@captainmiaow](https://gitcode.com/captainmiaow), *songzhiqi1@huawei.com*
- 钟梓莘 [@zhong-zixin](https://gitcode.com/zhong-zixin), *zhongzixin@huawei.com*
- 黄帅 [@huangshuai59](https://gitcode.com/huangshuai59), *huangshuai59@huawei.com*
- 朱铭哲 [@zhu-mingzhe71](https://gitcode.com/zhu-mingzhe71), *zhumingzhe2@huawei.com*

## ffn committer列表：
- 唐超 [@chaotang233](https://gitcode.com/chaotang233), *tangchao47@hisilicon.com*
- 陈黄威 [@huang-wei-chen](https://gitcode.com/huang-wei-chen), *chenhuangwei1@huawei.com*

## gmm committer列表：
- 陈康 [@chenkang30](https://gitcode.com/chenkang30), *chenkang30@huawei.com*
- 王永光 [@wangyongguang](https://gitcode.com/wangyongguang), *wangyongguang1@huawei.com*
- 陈琳鑫 [@chen-linxin4](https://gitcode.com/chen-linxin4), *chenlinxin4@huawei.com*
- 赵臣臣 [@cc-z](https://gitcode.com/cc-z), *zhaochenchen11@huawei.com*
- 张硕累 [@zhangshuoleiokok](https://gitcode.com/zhangshuoleiokok), *zhangshuolei1@huawei.com*
- 魏纳川 [@Wei_NaChuan](https://gitcode.com/Wei_NaChuan), *weinachuan1@huawei.com*
- 杨子奇 [@yangziqi_007](https://gitcode.com/yangziqi_007), *yangziqi4@huawei.com*
- 鞠阳 [@juyangokok](https://gitcode.com/juyangokok), *juyang@huawei.com*
- 徐柯南 [@kknan](https://gitcode.com/kknan), *xukenan@huawei.com*
- 吴奕 [@wuyi_huawei](https://gitcode.com/wuyi_huawei), *wuyi36@hisilicon.com*
- 石睿 [@shi-rui](https://gitcode.com/shi-rui), *shirui17@huawei.com*
- 孔德元 [@kdy18482276080](https://gitcode.com/kdy18482276080), *kongdeyuan3@huawei.com*
- 朱逸君 [@Julius47](https://gitcode.com/Julius47), *zhuyijun8@hisilicon.com*
- 程志炜 [@cheng_zhiwei](https://gitcode.com/cheng_zhiwei), *chengzhiwei10@huawei.com*

## posembedding committer列表：
- 宋凯 [@songkai111](https://gitcode.com/songkai111), *songkai16@huawei.com*
- 於欣洁 [@yu-xinjie62](https://gitcode.com/yu-xinjie62), *yuxinjie1@huawei.com*
- 俞浩 [@yuhao_](https://gitcode.com/yuhao_), *yuhao93@huawei.com*
- 陈琳鑫 [@chen-linxin4](https://gitcode.com/chen-linxin4), *chenlinxin4@huawei.com*
- 赵臣臣 [@cc-z](https://gitcode.com/cc-z), *zhaochenchen11@huawei.com*
- 魏纳川 [@Wei_NaChuan](https://gitcode.com/Wei_NaChuan), *weinachuan1@huawei.com*
- 鞠阳 [@juyangokok](https://gitcode.com/juyangokok), *juyang@huawei.com*
- 丁勇 [@xuanyuandy](https://gitcode.com/xuanyuandy), *dingyong19@huawei.com*
- 周扬帆 [@hz36amy_00](https://gitcode.com/hz36amy_00), *zhouyangfan8@huawei.com*
- 陆威 [@luwei_1104](https://gitcode.com/luwei_1104), *luwei44@huawei.com*
- 王荀 [@wangxun21](https://gitcode.com/wangxun21), *wangxun21@huawei.com*
- 孔德元 [@kdy18482276080](https://gitcode.com/kdy18482276080), *kongdeyuan3@huawei.com*
- 朱逸君 [@Julius47](https://gitcode.com/Julius47), *zhuyijun8@hisilicon.com*
- 徐诚阳 [@xuchengyang](https://gitcode.com/xuchengyang), *xuchengyang4@huawei.com*
- 蒋家炜 [@jiangjiawei](https://gitcode.com/jiangjiawei), *jiangjiawei10@huawei.com*
- 程志炜 [@cheng_zhiwei](https://gitcode.com/cheng_zhiwei), *chengzhiwei10@huawei.com*

## attention committer列表：
- 杨彬榕 [@yang-binrong](https://gitcode.com/yang-binrong), *yangbinrong@huawei.com*
- 高翔 [@gaoxiang618](https://gitcode.com/gaoxiang618), *gaoxiang26@huawei.com*
- 黄伟 [@huangwei791](https://gitcode.com/huangwei791), *huangwei791@huawei.com*
- 胡碧霞 [@crystalhu](https://gitcode.com/crystalhu), *hubixia1@huawei.com*
- 苗方正 [[@miaofangzheng]](https://gitcode.com/miaofangzheng), *miaofangzheng@huawei.com*
- 於欣洁 [[@yu-xinjie62]](https://gitcode.com/yu-xinjie62), *yuxinjie1@huawei.com*
- 俞浩 [@yuhao_](https://gitcode.com/yuhao_), *yuhao93@huawei.com*
- 赵臣臣 [@cc-z](https://gitcode.com/cc-z), *zhaochenchen11@huawei.com*
- 张硕累 [@zhangshuoleiokok](https://gitcode.com/zhangshuoleiokok), *zhangshuolei1@huawei.com*
- 魏纳川 [@Wei_NaChuan](https://gitcode.com/Wei_NaChuan), *weinachuan1@huawei.com*
- 杨子奇 [@yangziqi_007](https://gitcode.com/yangziqi_007), *yangziqi4@huawei.com*
- 赵志勇 [@zzy__](https://gitcode.com/zzy__), *zhaozhiyong15@hisilicon.com*
- 张海杰 [@haijie_699874](https://gitcode.com/haijie_699874), *zhanghaijie4@hisilicon.com*
- 沈维铃 [@shen_weiling](https://gitcode.com/shen_weiling), *shenweiling@huawei.com*
- 唐浩 [@tang-hao-hw-gitcode](https://gitcode.com/tang-hao-hw-gitcode), *tanghao71@hisilicon.com*
- 鞠阳 [@juyangokok](https://gitcode.com/juyangokok), *juyang@huawei.com*
- 宋炯辉 [@songjionghui](https://gitcode.com/songjionghui), *songjionghui@huawei.com*
- 王哲 [@wangzhe123456789](https://gitcode.com/wangzhe123456789), *wangzhe92@huawei.com*
- 黄立 [@huang_li](https://gitcode.com/huang_li), *huangli84@hisilicon.com*
- 林竹 [@coder_linx](https://gitcode.com/coder_linx), *linzhu3@huawei.com*
- 丁勇 [@xuanyuandy](https://gitcode.com/xuanyuandy), *dingyong19@huawei.com*
- 韩孝斌 [@L_Euler](https://gitcode.com/L_Euler), *hanxiaobin3@huawei.com*
- 周扬帆 [@hz36amy_00](https://gitcode.com/hz36amy_00), *zhouyangfan8@huawei.com*
- 安沙沙 [@shasha_an](https://gitcode.com/shasha_an), *anshasha@hisilicon.com*
- 桂建伟 [@guijianwei](https://gitcode.com/guijianwei), *guijianwei@huawei.com*
- 陆威 [@luwei_1104](https://gitcode.com/luwei_1104), *luwei44@huawei.com*
- 王荀 [@wangxun21](https://gitcode.com/wangxun21), *wangxun21@huawei.com*
- 孔德元 [@kdy18482276080](https://gitcode.com/kdy18482276080), *kongdeyuan3@huawei.com*
- 朱逸君 [@Julius47](https://gitcode.com/Julius47), *zhuyijun8@hisilicon.com*
- 徐诚阳 [@xuchengyang](https://gitcode.com/xuchengyang), *xuchengyang4@huawei.com*
- 陈黄威 [@huang-wei-chen](https://gitcode.com/huang-wei-chen), *chenhuangwei1@huawei.com*
- 李宁 [@lining_210](https://gitcode.com/lining_210), *lining210@huawei.com*
- 程志炜 [@cheng_zhiwei](https://gitcode.com/cheng_zhiwei), *chengzhiwei10@huawei.com*

## mhc committer列表:
- 陆威 [@luwei_1104](https://gitcode.com/luwei_1104), *luwei44@huawei.com*
- 孔德元 [@kdy18482276080](https://gitcode.com/kdy18482276080), *kongdeyuan3@huawei.com*
- 王荀 [@wangxun21](https://gitcode.com/wangxun21), *wangxun21@huawei.com*
- 薛靖晖 [@xuejinghui](https://gitcode.com/xuejinghui), *xuejinghui@huawei.com*

## 资料 committer列表：
- 郑雯文 [@Ww7012](https://gitcode.com/Ww7012), *zhengwenwen7@huawei.com*
- 陈娇 [@gitcode-chenjiao](https://gitcode.com/gitcode-chenjiao), *chenjiao31@huawei.com*
- 蔡雯雯 [@caiwenwen](https://gitcode.com/caiwenwen), *caiwenwen6@h-partners.com*
- 杜慧萍 [@gitee-duhuiping](https://gitcode.com/gitee-duhuiping), *duhuiping@h-partners.com*
- 冯英[@fengying555682](https://gitcode.com/fengying555682), *fengying27@h-partners.com*
- 杨露[@yanglu-1](https://gitcode.com/yanglu-1), *yanglou1@h-partners.com*
- 袁滔 [@claire8090](https://gitcode.com/claire8090), *yuantao27@h-partners.com*

# SIG订阅

- [邮件订阅](https://mailweb.cann.osinfra.cn/mailman3/lists/ops-transformer.cann.osinfra.cn/)

# 仓库清单

仓库地址：
- https://gitcode.com/cann/ops-transformer
- https://gitcode.com/cann/ops-tilelang

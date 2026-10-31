# CANN 9.2.1 测试报告
## 1. 概述

版本新增特性、修复问题请参考release-nodes：https://gitcode.com/cann/release-management/blob/master/9.2.1/release-notes.md

## 2. 版本测试信息
**硬件和版本摘要**

*产品型号：Ascend 950DT、Ascend 950PR、Atlas 900 A3 SuperPoD、Atlas 800T A2、Atlas 200T A2 Box16*

*操作系统：EulerOS 2.0 (SP12)、Ubuntu 24.04 LTS、OpenEuler22.03 LTS SP4*

*CANN版本：CANN 9.2.1*

*驱动版本：	Ascend HDK 26.2.RC1、Ascend HDK 26.1.1、Ascend HDK 26.0.RC1、Ascend HDK 25.7.RC1、Ascend HDK 25.5.0、Ascend HDK 25.3.RC1*



## 3. 测试结论

**本次发版本，共计执行20k测试用例，有两个遗留问题，整体质量良好，满足出口质量标准。**


## 4. 特性质量评估
| 序号  | 子包                       |特性   |测试结论   |功能   |精度   |性能   |可靠性   |兼容性   |
|-----|--------------------------| ------------ | ------------ |------------   |------------   |------------   |------------   |------------   |
| 1   | cann-hccl                |Pass |Pass   |Pass   |Pass   |Pass   |Pass   |Pass   |
| 2   | cann-hixl                |Pass |Pass   |Pass   |Pass   |Pass   |Pass   |Pass   |
| 3   | cann-ops-math            |Pass |Pass   |Pass   |Pass   |Pass   |Pass   |Pass   |
| 4   | cann-ops-nn              |Pass |Pass   |Pass   |Pass   |Pass   |Pass   |Pass   |
| 5   | cann-ops-cv              |Pass |Pass   |Pass   |Pass   |Pass   |Pass   |Pass   |
| 6   | cann-ops-transformer     |Pass |Pass   |Pass   |Pass   |Pass   |Pass   |Pass   |
| 7 | ascend-transformer-boost |Pass |Pass   |Pass   |Pass   |Pass   |Pass   |Pass   |

## 5. DFX专项质量评估
### 5.1 安全测试
1. 该版本整体安全测试结论为通过；
2. 该版本继承CANN 9.2.0商发版本的fuzz测试、端口扫描均通过的结论；
3. 该版本合入的bugfix经评估对安全无影响；
4. 其余安全测试项的结论如下，详见安全测试报告：


| 序号  | 测试项                       |安全性特性   |测试结论   |遗留风险   |
|-----|--------------------------| ------------ | ------------ |------------   |
| 1   | 静态代码扫描               |Pass |Pass   |无 |
| 2   | 病毒扫描                |Pass |Pass   |无 |
| 3   | 安全配置            |Pass |Pass   |无 |
| 4   | 编译选项              |Pass |Pass   |无 |
| 5   | 安全漏洞扫描              |Pass |Pass   |无 |


### 5.2 3*24h 可靠性测试
本次测试覆盖各仓可靠性特性测试，及整包稳定性测试，符合版本出口稳定性要求。

| 序号  | 子包                       |可靠性特性   |测试结论   |遗留风险   |
|-----|--------------------------| ------------ | ------------ |------------   |
| 1   | cann-hccl                |Pass |Pass   |无 |
| 2   | cann-hixl                |Pass |Pass   |无 |
| 3   | cann-ops-math            |Pass |Pass   |无 |
| 4   | cann-ops-nn              |Pass |Pass   |无 |
| 5   | cann-ops-cv              |Pass |Pass   |无 |
| 6   | cann-ops-transformer     |Pass |Pass   |无 |
| 7 | ascend-transformer-boost |Pass |Pass   |无 |



### 5.3 性能测试


| 序号  | 子包                       | 性能指标  | 测试结论 | 遗留问题 |
|-----|--------------------------|-------|-----|-----|
| 1   | cann-hccl                | 性能无劣化 |Pass   |无 |
| 2   | cann-hixl                | 性能无劣化 |Pass   |无 |
| 3   | cann-ops-math            | 性能无劣化 |Pass   |无 |
| 4   | cann-ops-nn              | 性能无劣化 |Pass   |无 |
| 5   | cann-ops-cv              | 性能无劣化 |Pass   |无 |
| 6   | cann-ops-transformer     | 性能无劣化 |Pass   |无 |
| 7 | ascend-transformer-boost | 性能无劣化 |Pass   |无 |





### 5.4 兼容性测试
本次测试覆盖历史版本升级、各子包独立升级等兼容性测试，满足兼容性要求

| 序号  | 子包                       |验证结果   |遗留风险 |
|-----|--------------------------| ----------| -------|
| 1   | cann-hccl                |通过   |  无 |
| 2   | cann-hixl                |通过  |  无  |
| 3   | cann-ops-math            |通过   |  无  |
| 4   | cann-ops-nn              |通过   |  无  |
| 5   | cann-ops-cv              |通过  |  无  |
| 6   | cann-ops-transformer     |通过   | 无 |
| 7   | ascend-transformer-boost |通过   | 无   |




## 6. 测试执行评估

### 6.1 整包测试覆盖

### 6.1.1 冒烟测试

| 测试活动   |测试结论   |用例数   |用例覆盖率   |用例通过率
| ------------ | ------------ | ------------ |------------|------------|
|  算子 |pass   |729  | 100%   | 100% |
|  cann 多OS|pass |653  | 100%   | 100% |
|  atb |pass   |301   | 100%   | 100% |
|  HCCL |pass   |156   | 100%   | 100% |

### 6.1.2 3*24h长稳测试

| 测试活动   |测试结论   |用例数   |用例覆盖率   |用例通过率
| ------------ | ------------ | ------------ |------------|------------|
|  算子 |pass   |1274  | 100%   | 100% |
|  cann 多OS|pass |2448  | 100%   | 100% |
|  atb |pass   |3456   | 100%   | 100% |
|  HCCL |pass   |1110  | 100%   | 100% |

### 6.1.3 全量测试

| 测试活动   |测试结论   |用例数   |用例覆盖率   |用例通过率
| ------------ | ------------ | ------------ |------------|------------|
|  算子 |pass   |5260   | 100%   | 100% |
|  cann 多OS|pass |2097  | 100%   | 100% |
|  atb |pass   |1677   | 100%   | 100% |
|  HCCL |pass   |746   | 100%   | 100% |


### 6.1.4 其他测试项
| 测试活动   |测试结论   |用例数   |用例覆盖率   |用例通过率
| ------------ | ------------ | ------------ |------------|------------|
|  兼容性测试 |pass   |2   | 100%   | 100% |
|  头文件静态测试 |pass |1  | 100%   | 100% |
|  独立升级兼容性 |pass   |5   | 100%   | 100% |
|  二进制一致性 |pass   |1   | 100%   | 100% |
|  合包测试 |pass   | 4   | pass   | pass |


## 7. 遗留问题和关键风险

### 7.1  遗留问题和关键风险

1. A2 allreduce算子开启pipeline和确定性时，在1024B数据量下出现功能问题
2. allreduce算子开启NB算法时，特定数据量下出现FFTS子图规则校验失败

## 8. 附件
不涉及
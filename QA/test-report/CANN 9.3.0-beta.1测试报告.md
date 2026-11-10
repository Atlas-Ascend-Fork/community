# CANN 9.3.0-beta1  测试报告

## 1. 概述

版本新增特性、修复问题请参考release-notes：https://gitcode.com/cann/release-management/blob/master/9.3.0-beta.1/release-notes.md

## 2. 版本测试信息

**硬件和版本摘要**

*产品型号：Ascend 950DT、Ascend 950PR、Atlas 900 A3 SuperPoD、Atlas 800T A2、Atlas 200T A2 Box16*

*操作系统：EulerOS 2.0 (SP12)、Ubuntu 24.04 LTS、OpenEuler22.03 LTS SP4*

*CANN版本：CANN 9.3.0 beta.1

*驱动版本：Ascend HDK 26.2.RC1、Ascend HDK 26.1.1、Ascend HDK 26.0.RC1、Ascend HDK 25.7.RC1、Ascend HDK 25.5.0、Ascend HDK 25.3.RC1*

## 3. 测试结论

**本次社区发版本，全仓完成基础功能用例、可靠性用例、性能用例全回归测试，并完成了版本兼容性测试**

**测试执行率100%，整体测试通过率100%，无遗留问题，整体质量良好，满足出口质量标准。**

****

## 4. 特性质量评估

| 序号 | 子包                     | 特性 | 测试结论 | 功能 | 精度 | 性能 | 可靠性 | 兼容性 |
| ---- | ------------------------ | ---- | -------- | ---- | ---- | ---- | ------ | ------ |
| 1    | cann-hccl                | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 2    | cann-hixl                | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 3    | cann-ops-legacy          | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 4    | cann-ops-math            | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 5    | cann-ops-nn              | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 6    | cann-ops-cv              | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 7    | cann-ops-transformer     | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 8    | cann-dvpp                | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 9    | cann-hcomm               | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 10   | cann-tbe-tik             | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 11   | cann-dflow-executor      | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 12   | cann-acl-extend          | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 13   | cann-oam-tools           | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 14   | cann-aoe                 | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 15   | cann-ncs                 | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 16   | cann-npu-runtime         | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 17   | cann-asc-tools           | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 18   | cann-asc-devkit          | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 19   | cann-ge-compiler         | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 20   | cann-graph-autofusion    | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 21   | cann-ge-executor         | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 22   | cann-metadef             | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 23   | cann-bisheng-compiler    | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 24   | cann-pypto               | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 25   | cann-opbase              | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 26   | cann-pypto-tools         | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 27   | cann-amct                | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 28   | pyasc                    | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 29   | hdk-driver-compat        | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 30   | ascend-transformer-boost | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |
| 31   | sip                      | Pass | Pass     | Pass | Pass | Pass | Pass   | Pass   |

## 5. DFX专项质量评估

### 5.1 可靠性测试

本次测试覆盖各仓可靠性特性测试，及整包稳定性测试，符合版本出口稳定性要求（>3*24H）。

| 序号 | 子包                     | 可靠性特性 | 测试结论 | 遗留风险 |
| ---- | ------------------------ | ---------- | -------- | -------- |
| 1    | cann-hccl                | Pass       | Pass     | 无       |
| 2    | cann-hixl                | Pass       | Pass     | 无       |
| 3    | cann-ops-legacy          | Pass       | Pass     | 无       |
| 4    | cann-ops-math            | Pass       | Pass     | 无       |
| 5    | cann-ops-nn              | Pass       | Pass     | 无       |
| 6    | cann-ops-cv              | Pass       | Pass     | 无       |
| 7    | cann-ops-transformer     | Pass       | Pass     | 无       |
| 8    | cann-dvpp                | Pass       | Pass     | 无       |
| 9    | cann-hcomm               | Pass       | Pass     | 无       |
| 10   | cann-tbe-tik             | Pass       | Pass     | 无       |
| 11   | cann-dflow-executor      | Pass       | Pass     | 无       |
| 12   | cann-acl-extend          | Pass       | Pass     | 无       |
| 13   | cann-oam-tools           | Pass       | Pass     | 无       |
| 14   | cann-aoe                 | Pass       | Pass     | 无       |
| 15   | cann-ncs                 | Pass       | Pass     | 无       |
| 16   | cann-npu-runtime         | Pass       | Pass     | 无       |
| 17   | cann-asc-tools           | Pass       | Pass     | 无       |
| 18   | cann-asc-devkit          | Pass       | Pass     | 无       |
| 19   | cann-ge-compiler         | Pass       | Pass     | 无       |
| 20   | cann-graph-autofusion    | Pass       | Pass     | 无       |
| 21   | cann-ge-executor         | Pass       | Pass     | 无       |
| 22   | cann-metadef             | Pass       | Pass     | 无       |
| 23   | cann-bisheng-compiler    | Pass       | Pass     | 无       |
| 24   | cann-pypto               | Pass       | Pass     | 无       |
| 25   | cann-opbase              | Pass       | Pass     | 无       |
| 26   | cann-pypto-tools         | Pass       | Pass     | 无       |
| 27   | cann-amct                | Pass       | Pass     | 无       |
| 28   | pyasc                    | Pass       | Pass     | 无       |
| 29   | hdk-driver-compat        | Pass       | Pass     | 无       |
| 30   | ascend-transformer-boost | Pass       | Pass     | 无       |
| 31   | sip                      | Pass       | Pass     | 无       |

### 5.2 性能测试

| 序号 | 子包                     | 性能指标   | 测试结论 | 遗留问题 |
| ---- | ------------------------ | ---------- | -------- | -------- |
| 1    | cann-hccl                | 性能无劣化 | Pass     | 无       |
| 2    | cann-hixl                | 性能无劣化 | Pass     | 无       |
| 3    | cann-ops-legacy          | 性能无劣化 | Pass     | 无       |
| 4    | cann-ops-math            | 性能无劣化 | Pass     | 无       |
| 5    | cann-ops-nn              | 性能无劣化 | Pass     | 无       |
| 6    | cann-ops-cv              | 性能无劣化 | Pass     | 无       |
| 7    | cann-ops-transformer     | 性能无劣化 | Pass     | 无       |
| 8    | cann-dvpp                | 性能无劣化 | Pass     | 无       |
| 9    | cann-hcomm               | 性能无劣化 | Pass     | 无       |
| 10   | cann-tbe-tik             | 性能无劣化 | Pass     | 无       |
| 11   | cann-dflow-executor      | 性能无劣化 | Pass     | 无       |
| 12   | cann-acl-extend          | 性能无劣化 | Pass     | 无       |
| 13   | cann-oam-tools           | 性能无劣化 | Pass     | 无       |
| 14   | cann-aoe                 | 性能无劣化 | Pass     | 无       |
| 15   | cann-ncs                 | 性能无劣化 | Pass     | 无       |
| 16   | cann-npu-runtime         | 性能无劣化 | Pass     | 无       |
| 17   | cann-asc-tools           | 性能无劣化 | Pass     | 无       |
| 18   | cann-asc-devkit          | 性能无劣化 | Pass     | 无       |
| 19   | cann-ge-compiler         | 性能无劣化 | Pass     | 无       |
| 20   | cann-graph-autofusion    | 性能无劣化 | Pass     | 无       |
| 21   | cann-ge-executor         | 性能无劣化 | Pass     | 无       |
| 22   | cann-metadef             | 性能无劣化 | Pass     | 无       |
| 23   | cann-bisheng-compiler    | 性能无劣化 | Pass     | 无       |
| 24   | cann-pypto               | 性能无劣化 | Pass     | 无       |
| 25   | cann-opbase              | 性能无劣化 | Pass     | 无       |
| 26   | cann-pypto-tools         | 性能无劣化 | Pass     | 无       |
| 27   | cann-amct                | 性能无劣化 | Pass     | 无       |
| 28   | pyasc                    | 性能无劣化 | Pass     | 无       |
| 29   | hdk-driver-compat        | 性能无劣化 | Pass     | 无       |
| 30   | ascend-transformer-boost | 性能无劣化 | Pass     | 无       |
| 31   | sip                      | 性能无劣化 | Pass     | 无       |

### 5.3 兼容性测试

本次测试覆盖历史版本升级、各子包独立升级等兼容性测试，满足兼容性要求

| 序号 | 子包                     | 验证结果 | 遗留风险 |
| ---- | ------------------------ | -------- | -------- |
| 1    | cann-hccl                | 通过     | 无       |
| 2    | cann-hixl                | 通过     | 无       |
| 3    | cann-ops-math            | 通过     | 无       |
| 4    | cann-ops-nn              | 通过     | 无       |
| 5    | cann-ops-cv              | 通过     | 无       |
| 6    | cann-ops-transformer     | 通过     | 无       |
| 7    | cann-opbase              | 通过     | 无       |
| 8    | ascend-transformer-boost | 通过     | 无       |
| 9    | sip                      | 通过     | 无       |

## 6. 测试执行评估

### 6.1 测试覆盖

### 6.1.1 cann-hccl

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 358    | 100%       | 100%       |
| 性能测试     | pass     | 70     | 100%       | 100%       |
| 可靠性测试   | pass     | 25     | 100%       | 100%       |
| 继承特性测试 | pass     | 1514    | 100%       | 100%       |
| 兼容性测试   | pass     | 12    | 100%       | 100%       |

### 6.1.2 cann-hixl

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 345    | 100%       | 100%       |
| 性能测试     | pass     | 26     | 100%       | 100%       |
| 可靠性测试   | pass     | 42     | 100%       | 100%       |
| 继承特性测试 | pass     | 1108    | 100%       | 83.1%      |
| 兼容性测试   | pass     | 157    | 100%       | 100%       |

### 6.1.3 cann-ops-legacy

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 79     | 100%       | 100%       |
| 性能测试     | pass     | 17     | 100%       | 100%       |
| 可靠性测试   | pass     | 7      | 100%       | 100%       |
| 继承特性测试 | pass     | 78     | 100%       | 100%       |
| 兼容性测试   | pass     | 12     | 100%       | 100%       |

### 6.1.4 cann-ops-math

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 38688  | 100%       | 100%       |
| 性能测试     | pass     | 38688  | 100%       | 100%       |
| 可靠性测试   | pass     | 850    | 100%       | 100%       |
| 继承特性测试 | pass     | 12542  | 100%       | 100%       |
| 兼容性测试   | pass     | 不涉及 | 100%       | 100%       |

### 6.1.5 cann-ops-nn

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 15324  | 100%       | 100%       |
| 性能测试     | pass     | 15324  | 100%       | 100%       |
| 可靠性测试   | pass     | 630    | 100%       | 100%       |
| 继承特性测试 | pass     | 9581   | 100%       | 100%       |
| 兼容性测试   | pass     | 4      | 100%       | 100%       |

### 6.1.6 cann-ops-cv

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 3387   | 100%       | 100%       |
| 性能测试     | pass     | 3387   | 100%       | 100%       |
| 可靠性测试   | pass     | 312    | 100%       | 100%       |
| 继承特性测试 | pass     | 1316   | 100%       | 100%       |
| 兼容性测试   | pass     | 不涉及 | 100%       | 100%       |

### 6.1.7 cann-ops-transformer

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     |  4563  | 100%       | 98%        |
| 性能测试     | pass     | 3656   | 100%       | 100%       |
| 可靠性测试   | pass     | 7      | 100%       | 100%       |
| 继承特性测试 | pass     | 14700   | 100%       | 100%       |
| 兼容性测试   | pass     | 1      | 100%       | 100%       |

### 6.1.8 cann-dvpp

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 639    | 100%       | 100%       |
| 性能测试     | pass     | 36     | 100%       | 100%       |
| 可靠性测试   | pass     | 5      | 100%       | 100%       |
| 继承特性测试 | pass     | 8050   | 100%       | 100%       |
| 兼容性测试   | pass     | 5      | 100%       | 100%       |

### 6.1.9 cann-hcomm

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 210   | 100%       | 100%       |
| 性能测试     | pass     | 10   | 100%       | 100%       |
| 可靠性测试   | pass     | 20      | 100%       | 100%       |
| 继承特性测试 | pass     | 1205   | 100%       | 100%       |
| 兼容性测试   | pass     | 4      | 100%       | 100%       |

### 6.1.10 cann-tbe-tik

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 7163   | 100%       | 100%       |
| 性能测试     | pass     | 不涉及 | 100%       | 100%       |
| 可靠性测试   | pass     | 93     | 100%       | 100%       |
| 继承特性测试 | pass     | 不涉及 | 100%       | 100%       |
| 兼容性测试   | pass     | 不涉及 | 100%       | 100%       |

### 6.1.11 cann-dflow-executor

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 0   | 100%       | 100%       |
| 性能测试     | pass     | 125 | 100%       | 100%       |
| 可靠性测试   | pass     | 56     | 100%       | 100%       |
| 继承特性测试 | pass     | 1640   | 100%       | 100%       |
| 兼容性测试   | pass     | 384    | 100%       | 100%       |

### 6.1.12 cann-acl-extend

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 65     | 100%       | 100%       |
| 性能测试     | pass     | 18     | 100%       | 100%       |
| 可靠性测试   | pass     | 15     | 100%       | 100%       |
| 继承特性测试 | pass     | 98     | 100%       | 100%       |
| 兼容性测试   | pass     | 13     | 100%       | 100%       |

### 6.1.13 cann-oam-tools

| 测试活动   |测试结论   |用例数   | 用例覆盖率 |用例通过率
| ------------ | ------------ | ------------ |-------|------------|
|  特性测试    |pass   |97  | 100%  | 100%   |
|  性能测试    |pass |44| 100%  | 100% |
|  可靠性测试|pass   |39| 100%  |100% |
|  继承特性测试|pass   |920   | 100%  |100%   |
|   兼容性测试|pass   |60   | 100%  | 100% |

### 6.1.14 cann-aoe

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 24   | 100%       | 100%       |
| 性能测试     | pass     | 5   | 100%       | 100%       |
| 可靠性测试   | pass     | 5      | 100%       | 100%       |
| 继承特性测试 | pass     | 560   | 100%       | 100%       |
| 兼容性测试   | pass     | 8      | 100%       | 100%       |

### 6.1.15 cann-ncs

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 0   | 100%       | 100%       |
| 性能测试     | pass     | 0   | 100%       | 100%       |
| 可靠性测试   | pass     | 7      | 100%       | 100%       |
| 继承特性测试 | pass     | 42   | 100%       | 100%       |
| 兼容性测试   | pass     | 0      | 100%       | 100%       |

### 6.1.16 cann-npu-runtime

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 296   | 100%       | 100%       |
| 性能测试     | pass     | 522   | 100%       | 100%       |
| 可靠性测试   | pass     | 554      | 100%       | 100%       |
| 继承特性测试 | pass     | 6392   | 100%       | 100%       |
| 兼容性测试   | pass     | 5549      | 100%       | 100%       |

### 6.1.17 cann-asc-tools

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- |-----| ---------- | ---------- |
| 特性测试     | pass     | 98  | 100%       | 100%       |
| 可靠性测试   | pass     | 4   | 100%       | 100%       |
| 继承特性测试 | pass     | 98  | 100%       | 100%       |
| 兼容性测试   | pass     | 98   | 100%       | 100%       |

### 6.1.18 cann-asc-devkit

| 测试活动     | 测试结论      | 用例数    | 用例覆盖率 | 用例通过率 |
| ------------ |-----------|--------| ---------- | ---------- |
| 特性测试  | pass      | 64815  | 100% | 100%   |
| 性能测试  | pass      | 790    | 100%    | 100%   |
| 可靠性测试 | pass      | 158    | 100%    | 100%   |
| 继承特性测试 | pass      | 64815  | 100%       | 100%       |
| 兼容性测试 | pass      | 64815  | 100%   | 100%   |

### 6.1.19 cann-ge-compiler

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 13131 | 100%       | 98%   |
| 性能测试     | pass     | 355   | 100%       | 100%       |
| 可靠性测试   | pass     | 25      | 100%       | 100%       |
| 继承特性测试 | pass     | 13131   | 100%       | 100%       |
| 兼容性测试   | pass     | 2000     | 100%       | 100%       |

### 6.1.20 cann-graph-autofusion

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 11002 | 100%       | 100%       |
| 性能测试     | pass     | 355   | 100%       | 100%       |
| 可靠性测试   | pass     | 25      | 100%       | 100%       |
| 继承特性测试 | pass     | 11002   | 100%       | 100%       |
| 兼容性测试   | pass     | 2000      | 100%       | 100%       |

### 6.1.21 cann-metadef

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 不涉及   | 100%       | 100%       |
| 性能测试     | pass     | 355   | 100%       | 100%       |
| 可靠性测试   | pass     | 25      | 100%       | 100%       |
| 继承特性测试 | pass     | 13131  | 100%       | 100%       |
| 兼容性测试   | pass     | 2000      | 100%       | 100%       |

### 6.1.22 cann-bisheng-compiler

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 4118 | 100%       | 100%       |
| 性能测试     | pass     | 320 | 100%       | 100%       |
| 可靠性测试   | pass     | 21 | 100%       | 100%       |
| 继承特性测试 | pass     | 72 | 100%       | 100%       |
| 兼容性测试   | pass     | 3 | 100%       | 100%       |

### 6.1.23 cann-pypto

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |				
| ------------ | -------- | ------ | ---------- | ---------- |				
| 特性测试     | pass     | 2645   | 100%       | 100%       |				
| 性能测试     | pass     | 1566   | 100%       | 100%       |				
| 可靠性测试   | pass     | 7      | 100%       | 100%       |				
| 继承特性测试 | pass     | 27984   | 100%       | 100%     |				
| 兼容性测试   | pass     | 4      | 100%       | 100%       |	


### 6.1.24 cann-pypto-toolkit

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 不涉及   | 100%       | 100%       |
| 性能测试     | pass     | 不涉及  | 100%       | 100%       |
| 可靠性测试   | pass     | 7      | 100%       | 100%       |
| 继承特性测试 | pass     | 521  | 100%       | 100%       |
| 兼容性测试   | pass     | 4      | 100%       | 100%       |

### 6.1.24 cann-opbase

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 64815  | 100%       | 100%       |
| 性能测试     | pass     | 790    | 100%       | 100%       |
| 可靠性测试   | pass     | 158    | 100%       | 100%       |
| 继承特性测试 | pass     | 64815  | 100%       | 100%       |
| 兼容性测试   | pass     | 64185  | 100%       | 100%       |

### 6.1.26 cann-amct

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 424   | 100%       | 100%       |

### 6.1.27 pyasc

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率  |
| ------------ | -------- | ------ | ---------- |--------|
| 特性测试  |pass   | 2100 | 100%  | 100%   |
| 性能测试  |pass   | 350  | 100%  | 100%   |
| 可靠性测试 |pass   | 10   | 100%    | 100%   |
| 兼容性测试 |pass   | 2100  | 100%  | 100%   |

### 6.1.28 hdk-driver-compat

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 132    | 100%       | 100%       |
| 性能测试     | pass     | 58     | 100%       | 100%       |
| 可靠性测试   | pass     | 10     | 100%       | 100%       |
| 继承特性测试 | pass     | 418   | 100%       | 100%       |
| 兼容性测试   | pass     | 2      | 100%       | 100%       |

### 6.1.29 ascend-transformer-boost

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 312    | 100%       | 100%       |
| 性能测试     | pass     | 121    | 100%       | 100%       |
| 可靠性测试   | pass     | 27     | 100%       | 100%       |
| 继承特性测试 | pass     | 1152   | 100%       | 100%       |
| 兼容性测试   | pass     | 110    | 100%       | 100%       |

### 6.1.30 sip

| 测试活动     | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| ------------ | -------- | ------ | ---------- | ---------- |
| 特性测试     | pass     | 169    | 100%       | 100%       |
| 性能测试     | pass     | 31     | 100%       | 100%       |
| 可靠性测试   | pass     | 7      | 100%       | 100%       |
| 继承特性测试 | pass     | 130    | 100%       | 100%       |
| 兼容性测试   | pass     | 4      | 100%       | 100%       |

## 7. 遗留问题和关键风险

### 7.1  遗留问题和关键风险

无


## 8. 附件

不涉及
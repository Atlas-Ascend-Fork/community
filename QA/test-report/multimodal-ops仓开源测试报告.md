# multimodal-ops仓开源测试报告

## 1. 概述

本报告为 multimodal-ops 仓开源测试报告。multimodal-ops 是 Multimodal-AI SIG 的算子核心仓，面向昇腾 NPU 提供高性能多模态融合算子实现，基于 PyPTO Pro 编程框架开发。本次测试覆盖已合入的 2 个融合算子的功能、精度、性能验证，以及合规文件完整性、CI 流水线通过性和安全扫描。

### 新增特性清单

| 序号 | 特性名称 | 特性描述 |
|------|---------|---------|
| 1 | FusedConvSigmoid | 卷积+Sigmoid 融合算子，Cube-Vector 片上直传融合（L0C 累加结果经 fixpipe 直传 UB，激活在片上完成，中间数据不落 HBM），fp16 |
| 2 | FusedConvTanh | 卷积+Tanh 融合算子，双 Kernel 流水融合（K1 Cube 完成卷积写出 HBM，K2 Vector 读入完成激活），fp16 |
| 3 | CI 流水线与合规文件 | PreBuild + CodeCheck 门禁，LICENSE/README.md/CONTRIBUTING.md/SECURITY.md/.gitignore/OAT.xml 共 6 个合规文件齐全 |

### 解决问题列表

不涉及（首次合入业务代码，无历史问题）

## 2. 版本测试信息

**硬件和版本要求**

- 产品型号：Atlas 800I A2
- NPU 芯片：Ascend 950（dav-3510，28 AI Core，Cube 28 + Vector 56）
- 操作系统：Ubuntu 24.04.3 LTS (x86_64)
- CANN 版本：9.1.0
- 驱动版本：25.7.rc1
- Python 版本：3.12.3
- PyTorch 版本：2.7.1
- 依赖三方库版本：torch_npu 2.7.1.post8、PyPTO 0.2.1（CANN 内置）

**测试源**

- 仓库地址：https://gitcode.com/cann/multimodal-ops
- 测试分支：master
- 最新 commit：8337500（docs: 补充版本配套信息、英文 README、requirements.txt）
- CI 流水线：GitCode Action（PreBuild + CodeCheck）
- CI 状态：ci-pipeline-passed

## 3. Readme内容评估

Readme内容评估：通过；

| 验证项 | 验证内容 |
|--------|---------|
| 文档内容完整性 | 1、提供算子族总览表（融合/编码/几何/扩散），说明已实现与待共建状态<br/>2、提供已有算子清单（FusedConvSigmoid/FusedConvTanh），包含公式、融合方式、评测得分、加速比<br/>3、提供开发框架说明（PyPTO Pro 编程模型）<br/>4、提供快速使用指南（`pip install .` 安装命令）<br/>5、提供版本配套表（Atlas 800I A2 / CANN 9.1.0 / 驱动 / Python / PyTorch / torch_npu / PyPTO）<br/>6、提供英文 README（README_en.md），结构与中文一致<br/>7、提供 requirements.txt 依赖声明<br/>8、提供贡献指南（CONTRIBUTING.md）、安全声明（SECURITY.md）、许可证（LICENSE） |
| 文档内容正确性 | 1、算子介绍与实际代码一致（融合方式、数据类型 fp16、芯片 Ascend 950 均与 impl/ 代码匹配）<br/>2、目录排版合理，算子族→已有算子→快速使用层次清晰，空目录已标注"待共建"<br/>3、安装命令（`pip install . --force-reinstall --no-deps`）经实际验证可正确执行<br/>4、所有链接（multimodal-benchmark 仓、SIG 主页、CONTRIBUTING/SECURITY/LICENSE）跳转正确 |

## 4. 测试结论

共计执行 48 个算子功能/精度/性能用例（2 算子 × 24 case，每个 case 同时验证精度和性能）、6 个合规文件检查、1 项 Readme 内容评估、1 项 CI 流水线验证，通过率 100%。整体质量良好，满足出口质量标准。

## 5. 特性质量评估

| 序号 | 特性 | 测试结论 | 功能 | 精度 | 性能 | 可靠性 | 兼容性 |
|------|------|---------|------|------|------|--------|--------|
| 1 | FusedConvSigmoid | 通过 | Pass | Pass | Pass | NA | NA |
| 2 | FusedConvTanh | 通过 | Pass | Pass | Pass | NA | NA |
| 3 | CI 与合规 | 通过 | Pass | NA | NA | NA | NA |

### 5.1 精度测试

| 算子 | test case 数 | 通过数 | 通过率 |
|------|-------------|-------|--------|
| FusedConvSigmoid | 24 | 24 | 100% |
| FusedConvTanh | 24 | 24 | 100% |
| **合计** | **48** | **48** | **100%** |

### 5.2 性能测试

| 算子 | 融合方式 | test case 数 | 达标数(≥1.0×) | avg_speedup | overall_score |
|------|---------|-------------|-------------|-------------|---------------|
| FusedConvSigmoid | Cube-Vector 片上直传融合 | 24 | 24 | 2.87× | 87.50 |
| FusedConvTanh | 双 Kernel 流水融合 | 24 | 24 | 3.92× | 90.82 |

FusedConvSigmoid worst cases：

| case | baseline(μs) | elapsed(μs) | speedup |
|------|-------------|-------------|---------|
| case_20 | 38.21 | 31.65 | 1.21× |
| case_14 | 54.38 | 40.11 | 1.36× |
| case_3 | 67.38 | 46.93 | 1.44× |

FusedConvTanh worst cases：

| case | dtype | baseline(μs) | elapsed(μs) | speedup |
|------|-------|-------------|-------------|---------|
| case_18 | fp32 | 33.97 | 29.83 | 1.14× |
| case_20 | bf16 | 37.64 | 31.25 | 1.20× |
| case_21 | fp16 | 30.25 | 16.44 | 1.84× |

## 6. DFX专项质量评估

### 6.1 安全测试

| 序号 | 检查项 | 测试结论 | 遗留风险 |
|------|--------|---------|---------|
| 1 | 病毒扫描 | 通过 | 无 |
| 2 | 漏洞扫描 | 通过 | 无 |
| 3 | 安全编译选项扫描 | 不适用（Python 仓，无编译产物） | 无 |
| 4 | 开源片段引用扫描 | 通过 | 无 |
| 5 | 开源软件 License 合规检查 | 通过 | 无 |
| 6 | 开源组件扫描 | 通过 | 无 |

### 6.2 可靠性测试
不涉及

### 6.3 性能测试
见 5.2 节

### 6.4 兼容性测试
不涉及

## 7. 测试执行评估

### 7.1 测试覆盖

| 测试活动 | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
|---------|---------|-------|-----------|-----------|
| 算子功能/精度/性能测试 | pass | 48 | 100% | 100% |
| 合规文件检查 | pass | 6 | 100% | 100% |
| Readme 内容评估 | pass | 1 | 100% | 100% |
| CI 流水线验证 | pass | 1 | 100% | 100% |
| 安全测试 | pass | 6 | 100% | 100% |

## 8. 遗留问题和关键风险

### 8.1 遗留问题统计

| | 问题总数 | 严重 | 主要 | 次要 | 不重要 | 已取消 |
|---|---|---|---|---|---|---|
| 数目 | 0 | 0 | 0 | 0 | 0 | 0 |

### 8.2 遗留问题列表

| 问题单(issue链接) | 问题描述 | 问题级别 | 问题影响和规避措施 | 当前状态 |
|------------------|---------|---------|-----------------|---------|
| 无 | — | — | — | — |

**双语化说明**：英文 README（README_en.md）已随本次开源同步提交，后续版本将同步维护中英文文档。

## 9. 附件
不涉及

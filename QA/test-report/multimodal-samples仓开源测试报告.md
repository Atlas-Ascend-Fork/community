# multimodal-samples仓开源测试报告

## 1. 概述

本报告为 multimodal-samples 仓开源测试报告。multimodal-samples 是 Multimodal-AI SIG 的模型层仓库，当前提供自动驾驶场景的多传感器融合模型预训练权重，模型定义、训练配置与昇腾 NPU 适配待社区共建。本次测试覆盖已合入的 8 个模型权重的完整性验证，以及合规文件完整性、CI 流水线通过性和安全扫描。

### 新增特性清单

| 序号 | 特性名称 | 特性描述 |
|------|---------|---------|
| 1 | BEVFusion | Camera + LiDAR 融合的 BEV 3D 检测模型权重 |
| 2 | CLOCs | Camera-LiDAR 后融合目标检测模型权重 |
| 3 | EPNet | 点云 + 图像端到端融合检测模型权重 |
| 4 | EPNet++ | EPNet 改进版，残差融合模型权重 |
| 5 | FarAway | 远距离目标融合检测模型权重 |
| 6 | HMFI | 层次化多模态融合推理模型权重 |
| 7 | LOGONet | 局部-全局融合网络模型权重 |
| 8 | PointPainting | 语义分割投影到点云的融合检测模型权重 |
| 9 | CI 流水线与合规文件 | PreBuild + CodeCheck 门禁，LICENSE/README.md/CONTRIBUTING.md/SECURITY.md/.gitignore/OAT.xml 共 6 个合规文件齐全 |

### 解决问题列表

不涉及（首次合入业务代码，无历史问题）

## 2. 版本测试信息

**硬件和版本要求**

- 产品型号：Atlas 800I A2
- NPU 芯片：Ascend 950
- 操作系统：Ubuntu 24.04.3 LTS (x86_64)
- 训练环境 CANN 版本：9.1.0
- Python 版本：3.12.3
- PyTorch 版本：2.7.1
- 依赖三方库版本：torch 2.7.1

**测试源**

- 仓库地址：https://gitcode.com/cann/multimodal-samples
- 测试分支：master
- 最新 commit：b91bcd0（docs: 补充版本配套信息、英文 README、模型来源说明）
- CI 流水线：GitCode Action（PreBuild + CodeCheck）
- CI 状态：ci-pipeline-passed

## 3. Readme内容评估

Readme内容评估：通过；

| 验证项 | 验证内容 |
|--------|---------|
| 文档内容完整性 | 1、提供已有模型清单（8 个自动驾驶模型），说明权重文件名、模型用途和来源<br/>2、提供场景分类表（自动驾驶/AIGC/软件工程），说明已有与待共建状态<br/>3、提供版本配套表（Atlas 800I A2 / CANN 9.1.0 / PyTorch 2.7.1 / Python 3.12.3）<br/>4、提供英文 README（README_en.md），结构与中文一致<br/>5、提供源码下载和 Git LFS 使用说明<br/>6、提供贡献指南（CONTRIBUTING.md）、安全声明（SECURITY.md）、许可证（LICENSE） |
| 文档内容正确性 | 1、模型清单与实际权重文件一致（8 个 .pth 文件名与 README 表格匹配）<br/>2、概述与仓库实际内容一致（明确标注仅提供权重，其余待共建）<br/>3、目录排版合理，场景→模型→权重文件层次清晰<br/>4、`git lfs pull` 命令经验证可正确拉取权重文件<br/>5、所有链接跳转正确 |

## 4. 测试结论

共计执行 8 项模型权重完整性验证、6 个合规文件检查、1 项 Readme 内容评估、1 项 CI 流水线验证，通过率 100%。整体质量良好，满足出口质量标准。

## 5. 特性质量评估

| 序号 | 特性 | 测试结论 | 功能 | 精度 | 性能 | 可靠性 | 兼容性 |
|------|------|---------|------|------|------|--------|--------|
| 1 | 模型权重（8 个） | 通过 | Pass | NA | NA | NA | NA |
| 2 | CI 与合规 | 通过 | Pass | NA | NA | NA | NA |

### 5.1 模型权重完整性验证

| 模型 | 权重文件 | 文件大小 | LFS 管理 | README 描述 | 来源 | 验证结果 |
|------|----------|---------|---------|------------|------|---------|
| BEVFusion | bevfusion_kitti_fusion_latest.pth | 211.5 MB | 是 | 匹配 | 论文复现 | Pass |
| CLOCs | clocs_fusion_trained.pth | 178.0 MB | 是 | 匹配 | 论文复现 | Pass |
| EPNet | epnet_fusion_refine_best.pth | 240.0 MB | 是 | 匹配 | 论文复现 | Pass |
| EPNet++ | epnetpp_residual_car_v5_best.pth | 213.3 MB | 是 | 匹配 | 论文复现 | Pass |
| FarAway | faraway_gate40_epoch1_best.pth | 3.2 MB | 是 | 匹配 | 论文复现 | Pass |
| HMFI | hmfi_fusion_trained_best.pth | 372.1 MB | 是 | 匹配 | 论文复现 | Pass |
| LOGONet | logonet_fusion_trained_best_loss.pth | 216.1 MB | 是 | 匹配 | 论文复现 | Pass |
| PointPainting | pointpainting_kitti_car_best_ap.pth | 55.4 MB | 是 | 匹配 | 论文复现 | Pass |

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
不涉及

### 6.4 兼容性测试
不涉及

## 7. 测试执行评估

### 7.1 测试覆盖

| 测试活动 | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
|---------|---------|-------|-----------|-----------|
| 模型权重完整性验证 | pass | 8 | 100% | 100% |
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

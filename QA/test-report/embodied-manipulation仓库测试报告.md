# embodied-manipulation仓库测试报告

## 1. 概述

本报告覆盖 `cann/embodied-manipulation` 仓库中的 Wh0 与 3D FlowMatch Actor（简称 3DFA）两个项目，验证其昇腾适配、功能、数值一致性、工程交付及 DFX 质量。

| 项目 | 测试范围 |
| --- | --- |
| Wh0 | WM-H 在 Ascend 910 上的单卡、单条指令生成链路，包括指令生成、图像编辑、视频提示增强和四步视频生成；运行文档检查及文档变更门禁 |
| 3DFA | Python 包构建安装、核心算法回归、PerAct2 离线推理、Ascend 910B3 单卡 FP32/BF16 推理与 BF16 训练、数据增强、checkpoint 恢复；数值、吞吐、显存、稳定性及安全合规检查 |

新增特性及已解决问题如下：

- **Wh0：**完成 NPU 设备检测与隔离、随机数设备、显存释放、LoRA 参数和后端依赖适配；打通 Qwen Image Edit、Qwen3-VL 与 Wan2.2 最小生成链路，补充运行说明。
- **3DFA：**新增统一设备抽象、NPU 原生增强、精确分块 kNN、安全 checkpoint、依赖约束与 Python 打包配置；解决配置表达式执行、HTTPS 证书校验关闭、checkpoint 安全恢复、增强路径 CPU fallback 和采样大工作区 OOM 问题。

测试活动包括功能与数值回归、单卡集成验证、包构建安装，以及安全、可靠性、性能和兼容性测试。

## 2. 版本测试信息

| 项目 | Wh0 | 3DFA |
| --- | --- | --- |
| 项目目录 | `Wh0/WM-H/` | `3d_flowmatch_actor/` |
| 软件版本/代码基线 | `0.1.0` `7eecf33c` | `0.1.0` `7eecf33c` |
| 测试时间 | 2026-10-24 | NPU：2026-09-03；CPU 复核：2026-10-22 |

**硬件和版本要求**

| 环境项 | Wh0 NPU 验证 | 3DFA NPU 验证 | 3DFA CPU 复核 |
| --- | --- | --- | --- |
| 产品型号 | Ascend 910，单卡，64 GiB HBM | Ascend 910B3，单卡，64 GiB HBM | AArch64 容器 CPU |
| 操作系统 | Ubuntu 20.04.5 LTS，Linux `5.10.0-182.0.0.95.r2220_156.hce2.aarch64` | Huawei Cloud EulerOS 系列，Linux 5.10，AArch64 | Linux `5.10.0-182.0.0.95.r2673_211.hce2.aarch64` |
| CANN版本 | `9.0.0` | `9.0.0` | 不涉及 |
| 驱动版本 | `25.5.5` | `25.5.0` | 不涉及 |
| Python版本 | `3.11.16` | `3.11.4` | `3.11.4` |
| PyTorch版本 | `2.7.1+cpu`，由 torch_npu 注册 NPU 后端 | `2.7.1+cpu`，由 torch_npu 注册 NPU 后端 | `2.7.1+cpu` |
| torch_npu版本 | `2.7.1.post4` | `2.7.1.post4` | `2.7.1.post4`，仅导入 |
| torchvision版本 | `0.22.1` | `0.22.1` | `0.22.1` |
| NumPy版本 | `1.26.4` | 依赖约束 `1.26.4`；实装版本未单列 | `2.4.6`，存在 SciPy 配套告警 |
| 依赖三方库版本 | Transformers `5.16.1`；qwen-vl-utils `0.0.14`；DiffSynth-Studio `a84251704224d6189f695ce72c3d834b7f84557c`；Qwen Image Edit、Qwen3-VL、Wan2.2 I2V/Lightning | 依赖由 requirements/constraints 文件声明，详细配套见验证材料 | 复测依赖另见下文 |

3DFA 使用官方 PerAct2 checkpoint、PerAct2 数据（train 9,415 条、val 9,382 条）、CLIP RN50 及 `openai/clip-vit-base-patch32`；数据压缩包 CRC 检查通过，模型和数据验证材料见附件。

## 3. 测试结论

**本次测试范围内验证通过，建议发布。**

Wh0 0.1.0在 Ascend 910 上完成单卡、单条指令的 WM-H 最小生成链路验证，预期图片、任务文件和视频均成功生成；安全合规检查通过。

3DFA 0.1.0 的 30 个 CPU 自动化用例、10 类 NPU 集成/专项场景均通过；另完成 3 项包构建安装检查及 5 项安全合规检查，结果均通过。2026-10-22 CPU 复核为 `30 passed, 3 warnings in 58.54s`，退出码 0。

本轮确认的 2 个有效安全代码问题均已修复并经回归验证；两项目已执行活动中记录的遗留测试问题为 4个，其中1个为“主要”层级，3个为“次要”层级。各活动按其实际单位分别计量，数量和通过率见第 6 节。

## 4. 特性质量评估

| 序号 | 特性 | 测试结论 | 功能 | 精度 | 性能 | 可靠性 | 兼容性 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Wh0：WM-H NPU 生成链路 | 通过（单卡、单条指令） | 最小链路及预期产物生成通过 | 未量化生成质量 | 未建立基线 | 单次验证通过 | Ascend 910/CANN 9.0.0 |
| 2 | 3DFA：Python 包与统一设备抽象 | 通过（已测 CPU/NPU） | 构建安装、导入、设备解析及回退通过 | 不适用：包及设备管理 | 未单独计量 | 异常参数回归通过 | CPU、单卡 Ascend 910B3 |
| 3 | 3DFA：FP32/BF16 离线推理 | 有条件通过 | 合成及真实样本推理通过 | BF16 相对 FP32 最大/平均绝对误差 `0.0043004/0.0016051` | 推理性能未单独量化 | 训练后 checkpoint 推理通过 | 单卡 Ascend 910B3 |
| 4 | 3DFA：NPU 增强与精确分块 kNN | 通过（已测场景） | 几何一致性及采样回归通过 | 采样集合重合率 `1.0` | 显存结果见 5.3 | 已知 CPU fallback 消除 | 已测 CPU/NPU |
| 5 | 3DFA：BF16 训练与安全恢复 | 通过（已测步数） | 训练、保存及恢复通过 | 固定样本 100 步 loss 均值下降 `39.30%` | 训练基线见 5.3 | 稳定性及恢复结果见 5.2 | 单卡 Ascend 910B3 |

## 5. DFX专项质量评估

### 5.1 安全测试

已记录的安全检查通过，实际检查范围及使用限制如下。

| 项目 | 检查内容 | 测试结论及限制 |
| --- | --- | --- |
| Wh0：安全合规扫描 | Antipoison 通过；SCA 未确认文件 0、问题 0；CodeCheck 通过 | Pass |
| Wh0：Fuzz测试 | 无网络协议服务或自有 C/C++ 二进制解析接口；配置恶意输入和非法边界由单元测试覆盖 | Pass |
| 3DFA：安全合规扫描 | CodeCheck、Antipoison、开源片段、License、SCA 通过 | Pass |
| 3DFA：输入、下载及 checkpoint 安全 | 安全解析配置、恢复 HTTPS 证书验证；安全加载、CPU 可移植状态及原子保存验证通过 | Pass；2 个有效安全问题已修复 |
| 3DFA：Fuzz 测试 | 无网络协议服务或自有 C/C++ 二进制解析接口；配置恶意输入和非法边界由单元测试覆盖 | Pass |
| 3DFA：RLBench 数据反序列化 | 使用 pickle 读取数据 | Pass；仅处理官方或已校验哈希的可信数据，禁止来源不明或用户上传文件 |

Wh0, 3DFA 为纯 Python 项目、不产生自有 C/C++ 编译产物，安全编译选项测试不适用。

### 5.2 可靠性测试

可靠性结论限于以下单卡场景及测试时长。

| 序号 | 可靠性特性 | 测试结论 | 遗留风险 |
| --- | --- | --- | --- |
| 1 | Wh0：WM-H 最小生成链路 | 通过：单条指令执行及预期产物生成 | 长批次、长时间运行和异常恢复未验证 |
| 2 | 3DFA：训练数值与显存稳定性 | 通过：累计 1000 步数值有限；allocated/reserved 显存漂移约 `0.0005/0 MiB` | 未执行 300,000 步完整训练 |
| 3 | 3DFA：断点保存与恢复 | 通过：从 step 200 恢复至 1000，原子保存及恢复后推理通过 | 生产训练仍需持续保存 checkpoint 并监控运行状态 |
| 4 | 3DFA：NPU fallback | 通过：消除已知 inverse/solve CPU fallback；1000 步验收未见未知 fallback | 仅覆盖已测单卡路径 |

### 5.3 性能测试

3DFA 已形成单卡训练吞吐和显存基线；Wh0 模型性能及 3DFA 独立推理时延/吞吐尚未量化。

| 场景 | 模型 | 特性 | 性能指标 | 测试环境 | 测试结果 | 遗留风险 |
| --- | --- | --- | --- | --- | --- | --- |
| 图像/视频生成 | Wh0 WM-H | 最小生成链路 | 未提供时延、吞吐、显存及量化门槛 | 第 2 节 Wh0 环境 | 未测试性能基线 | 无批量性能结论 |
| 训练 | 3DFA | 推荐 batch | `49.3–50.9 samples/s`；reserved 约 `33,420 MiB`，余量约 28 GiB | Ascend 910B3 单卡、BF16，物理/有效 batch `256/256`，workers `0`；其余见第 2 节 | Pass | 限该配套，无迁移前同环境吞吐基线 |
| 点云密度采样 | 3DFA | 精确分块 kNN | batch 1 reserved 显存约 `9,700 → 1,244 MiB` | 第 2 节 3DFA NPU 环境 | Pass | 该实现对比不代表整模型吞吐提升比例 |
| 训练容量边界 | 3DFA | batch 上限探测 | batch 480 可训练并保存；batch 512 OOM | 第 2 节 3DFA NPU 环境 | Pass（预期边界探测） | batch 512 不支持，推荐已测 batch 256 |

### 5.4 兼容性测试

兼容性评估：通过，限于以下已测组合和流程。

| 序号 | 兼容性场景 | 验证结果 | 遗留风险 |
| --- | --- | --- | --- |
| 1 | Wh0：Ascend 910/CANN 9.0.0 单卡 WM-H 链路 | 通过（基础验证） | - |
| 2 | 3DFA：CPU 包构建、隔离安装及导入 | 通过，CPU 自动化用例 30/30 | 开发环境存在依赖及文件属主告警 |
| 3 | 3DFA：Ascend 910B3/Driver 25.5.0/CANN 9.0.0/Python 3.11.4/PyTorch 2.7.1+cpu/torch_npu 2.7.1.post4/torchvision 0.22.1 | 通过（单卡） | 不外推其他驱动、CANN 或芯片配套 |
| 4 | CUDA、多卡及其他 Ascend 型号 | 未验证 | 不纳入本次支持结论 |

## 6. 测试执行评估

### 6.1 测试覆盖

| 测试活动 | 测试结论 | 用例数 | 用例覆盖率 | 用例通过率 |
| --- | --- | --- | --- | --- |
| 特性测试 | Wh0 最小链路通过；3DFA 核心功能通过 | Wh0：10条指令；3DFA：30 个 CPU 用例、10 类 NPU 场景 | Wh0：100%；3DFA：100% | Wh0：10/10；3DFA：30/30、10/10，分别 100% |
| 性能测试 | Wh0 未测试；3DFA 已测指标通过 | 3DFA 包含于 NPU 场景，未单列数量 | 未单列专项分母 | Wh0：无；3DFA：已测场景通过，未单列比例 |
| 可靠性测试 | Wh0 单次验证通过；3DFA 稳定性及恢复通过 | Wh0 复用 1 条指令；3DFA 复用 CPU/NPU 测试 | 未单列专项分母 | 已报告场景通过，未单列比例 |
| 兼容性测试 | Wh0 单卡基础验证、3DFA CPU/单卡 NPU 通过 | 3DFA 包构建安装 3 项；其余复用 CPU/NPU 验证 | 3DFA 包交付计划 100% | 3DFA 包检查 3/3，100% |
| 安全测试 | Wh0 文档扫描、3DFA 指定代码基线门禁通过 | Wh0：Antipoison、SCA、CodeCheck 3 项；3DFA：5 项检查 | Wh0：100%；3DFA：100% | Wh0：3/3；3DFA：5/5，分别 100% |

## 7. 遗留问题和关键风险

### 7.1 遗留问题统计

|  | 问题总数 | 严重 | 主要 | 次要 | 不重要 | 已取消 |
| --- | --- | --- | --- | --- | --- | --- |
| 数目 | 4 | 0 | 1 | 3 | 0 | 0 |
| 百分比 | 100% | - | 25% | 75% | - | - |

### 7.2  遗留问题列表

| 问题单(issue链接) | 问题描述 | 问题级别 | 问题影响和规避措施 | 当前状态 |
| --- | --- | --- | --- | --- |
| 无 | Wh0生成质量、模型性能和长批次未验证 | 次要 | 当前支持声明限第 1 节的 WM-H 单卡最小链路 | 范围限制保留 |
| 无 | 3DFA 通过 pickle 读取 RLBench 数据 | 次要 | 不可信反序列化可能执行任意代码；仅处理官方或已校验哈希的数据，禁止来源不明或用户上传文件 | 已有规避措施，可信来源限制保留 |
| 无 | 3DFA 未验证在线任务、300,000 步完整训练、CUDA/多卡/其他 NPU；batch 512 OOM | 次要 | 不保证长周期训练稳定性及未测平台支持；推荐 batch 256；生产训练保留 checkpoint 并监控数值、显存和吞吐 | 未测范围保留；batch 512 不支持 |
| 无 | 3DFA 环境属主、NumPy/SciPy 配套及旧 CLIP 告警 | 主要 | 按锁定依赖创建干净环境、统一文件属主后复核，保留告警处置记录 | 未造成用例失败；发布环境处置记录未提供 |

## 8. 附件

- Wh0：[测试检查记录](https://gitcode.com/cann/embodied-manipulation/actions/runs/9c2607e26bb24265a0ff51fcc1fe1b5e)、[SCA 扫描记录](https://www.openlibing.com/apps/personalScandTaskInfor/person/e151c66f-c97e-4703-89f1-f908f147bb5c?projectId=300033&codeHostingPlatformFlag=gitcode)。
- 3DFA：[特性及 DFX 质量评估](https://gitcode.com/m0_74494151/embodied-manipulation/blob/bfc5020/3d_flowmatch_actor/docs/test_reports/b14_b15_quality_assessment.md)、[安全合规检查记录](https://gitcode.com/cann/embodied-manipulation/merge_requests/8)。
- 3DFA 专项验证：[离线推理](https://gitcode.com/m0_74494151/embodied-manipulation/blob/bfc5020/3d_flowmatch_actor/docs/work_notes/phase1_ascend_offline_inference.md)、[训练与稳定性](https://gitcode.com/m0_74494151/embodied-manipulation/blob/bfc5020/3d_flowmatch_actor/docs/work_notes/phase2_ascend_training.md)、[性能](https://gitcode.com/m0_74494151/embodied-manipulation/blob/bfc5020/3d_flowmatch_actor/docs/work_notes/phase3_ascend_performance.md)。
- 3DFA 三方件材料：[软件清单](https://gitcode.com/m0_74494151/embodied-manipulation/blob/bfc5020/3d_flowmatch_actor/Third_Party_Open_Source_Software_List.yaml)、[版权与许可证声明](https://gitcode.com/m0_74494151/embodied-manipulation/blob/bfc5020/3d_flowmatch_actor/Third_Party_Open_Source_Software_Notice)。

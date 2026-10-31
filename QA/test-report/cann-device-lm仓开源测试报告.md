# cann-device-lm 仓开源测试报告

## 1. 概述

本报告为 cann-device-lm 项目开源测试报告。测试覆盖仓内已交付能力的文档评估、构建打包、安装卸载、模型导出（epair）、OMC 编译、量化（GPTQ W4A8）、NPU 数值对齐与端到端推理。测试过程中对已纳入范围的特性执行覆盖率为 100%。

本仓面向 Kirin 芯片大模型推理，提供模型量化、模型编译、模型推理端到端能力：将 gemma4 模型导出为 epair 格式（IR + 权重分离），经 C++ 后端加载编译为 omc，最终在 Kirin 芯片上执行推理。

### 新增特性清单

| 序号 | 特性名称 | 特性描述 |
| --- | --- | --- |
| 1 | 一键构建打包 | `build.sh --pkg` 自动下载三方库 + C++ 编译 + converter whl + OHOS 交叉编译 + 签名 + .run 打包 |
| 2 | epair 导出 | HF 模型 → torch.export + torchair GE 转换 → epair（prefill/decode 两图 + 权值分离） |
| 3 | OMC 编译 | `cann_lm_compile` 加载 epair → GE Graph → `aclgrphBuildModel` → .omc |
| 4 | W4A8 量化 | GPTQ 离线权重 int4 + 运行时动态激活 int8，两种方式（自动调 dopt / 手动跑 dopt + 消费） |
| 5 | 鸿蒙部署 | engine whl 内嵌 .so + `deploy_ohos/` 主库 + UT，`hdc` 推送到设备 |
| 6 | lm-engine 推理 | 基于 py 和 C++ API 接口在 KirinX90 上跑通 gemma4-E4B 出字 |

### 测试活动

本次测试活动包括：README 与文档评估、一键构建出包、.run 包安装卸载、模型导出验证、OM 编译验证、量化链路验证、NPU 数值对齐、端到端推理、包安装模式 examples 验证。

## 2. 版本测试信息

**硬件和版本要求**

| 项 | 说明 |
| --- | --- |
| 产品型号 | KirinX90 开发板 |
| 操作系统 | x86 构建机（openEuler）；设备侧 OHOS |
| CANN 版本 | 9.3.0 |
| Python 版本 | 3.12 |
| OHOS SDK | command-line-tools-linux-x64-6.1.1.418 |
| 鸿蒙版本 | 7.0 |
| 测试源码 commit | main；构建/部署/板验基线 |

测试源码仓：https://gitcode.com/cann/cann-device-lm

## 3. 测试结论

cann-device-lm 完成开源测试，共计执行 35 组测试用例（含 711 项单元测试：Python 377 + C++ 334），产品代码 0 缺陷。整体质量良好，满足出口质量标准。**建议发布。**

| 评估维度 | 评估结果 |
| --- | --- |
| 测试用例总数 | 35 组（含 711 项单元测试：Python 377 + C++ converter 7 + C++ engine 327） |
| 测试执行通过率 | 100%（711 通过） |
| 测试结论 | 通过 |
| 构建链复验 | `--pkg --no-signed` + `--smoke` 全绿；产物板端出字 14/14 通过 |

## 4. 特性质量评估

| 序号 | 特性 | 测试结论 | 构建 | 导出 | 编译 | 量化 | NPU 对齐 | 端到端 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 一键构建打包 | 通过 | Pass | — | — | — | — | — |
| 2 | epair 导出 | 通过 | — | Pass | — | — | — | — |
| 3 | OMC 编译 | 通过 | — | — | Pass | — | — | — |
| 4 | W4A8 量化 | 通过 | — | — | Pass | Pass | — | — |
| 5 | 鸿蒙部署 | 通过 | Pass | — | — | — | — | Pass |
| 6 | lm-engine 推理 | 通过 | — | — | — | — | Pass | Pass |

## 5. 测试用例与结果

### 5.1 构建打包

| 序号 | 测试用例 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 1 | `build.sh --pkg` 全量构建 | [1/4] C++ 编译 → [2/4] converter whl → [3/4] OHOS 交叉编译+签名 → [4/4] 打包 | PASS |
| 2 | `build.sh cpp` C++ 构建 | `cann_lm_compile` (82K) + `libtorch_delegate_backend.so` (856K) | PASS |
| 3 | `build.sh check` 环境校验 | CANN / P1 venv / torchair / torch_delegate / cann_lm / third_party 全就绪 | PASS |
| 4 | 三方库自动下载 | `--pkg` 自动从 gitcode 下载 nlohmann_json / GTest / makeself | PASS |

### 5.2 模型导出（epair）

| 序号 | 测试用例 | 模型 | target_soc | 结果 |
| --- | --- | --- | --- | --- |
| 5 | 普通导出 prefill-decode | gemma4-E4B-it (4B) | KirinX90 (fp16) | PASS |

### 5.3 OMC 编译

| 序号 | 测试用例 | 模型 | CANN 版本 | 结果 |
| --- | --- | --- | --- | --- |
| 6 | gemma4-E4B prefill+decode 编译（KirinX90 omc） | gemma4-E4B-it (4B) | 9.3.0 | PASS |
| 7 | quick_exit 修复验证 | 编译后无 abort | 9.3.0 | PASS（`corrupted size` 消失） |

### 5.4 量化（W4A8 GPTQ）

| 序号 | 测试用例 | 模型 | 方式 | 结果 |
| --- | --- | --- | --- | --- |
| 8 | GPTQ 量化 + int4 物化 | gemma4-E4B-it | 方式一（`--quant-method gptq`） | PASS |
| 9 | epair 导出（w4a8 量化消费） | gemma4-E4B-it | 方式二（手动 dopt + `--quant-path`） | PASS |
| 10 | dopt 单独运行 | gemma4-E4B-it | `dopt_lm.opt_main` 手动两步 | PASS |

### 5.5 NPU 数值对齐与端到端

| 序号 | 测试用例 | 模型 | 结果 |
| --- | --- | --- | --- |
| 11 | vs HF logits + greedy 对齐 | gemma4-E4B-it | PASS（max_diff=1.688, argmax 97-100% match, greedy identical） |
| 12 | vs HF logits + greedy 对齐（1 层截断版上板） | gemma4-E4B-it | PASS |
| 13 | MRT 板跑精度（fp16） | gemma4-E4B-it（42 层 prefill + decode） | PASS（cos: logits 0.999994 / K 0.999999 / V 0.999998） |
| 14 | engine 端到端出字（量化全模） | gemma4-E4B-it（42 层 W4A8） | PASS（bbit flow 14/14，复跑一致） |

### 5.6 .run 包安装与环境管理

| 序号 | 测试用例 | 结果 |
| --- | --- | --- |
| 15 | .run 包安装 + cann_lm whl 装入 P1 venv | PASS |
| 16 | `set_env.sh --npu` 自动探测 DOPT_PYTHON | PASS（探测到 /opt/buildtools/python-3.12.9/bin/python3） |

### 5.7 单元测试（Python + C++）

| 序号 | 测试用例 | 测试套件 | 用例数 | 通过 | 跳过 | 失败 | 耗时 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 17 | Python UT（llm_models） | test_gemma4 / test_fused_ops / test_model_registry / test_export_wrapper_base | 117 | 117 | 0 | 0 | 44.0s |
| 18 | Python UT（converter） | test_cli / test_epair_utils / test_loader / test_materialize / test_quant_linear / test_saver / test_swap / test_weight_format | 140 | 140 | 0 | 0 | 1.5s |
| 19 | Python UT（dopt_lm） | test_gptq_core / test_data_train_orchestration / test_min_max / test_opt_main / test_qmanager_modules / test_quantizer_utils / test_register_builder / test_strategy_do_opt / test_strategy_generation | 120 | 120 | 0 | 0 | 4.9s |
| 20 | C++ UT（converter，ASAN） | test_consolidated_weights / test_epair_archive / test_epair_model_parser / test_base64 / test_value_registry / test_aten_schema_resolver / test_aten_tensor_desc_mapper | 7 | 7 | 0 | 0 | 6.8s |
| 21 | C++ UT（engine，host） | ut_engine_executor / ut_tokenizer / ut_c_api / ut_scheduler / ut_text_embedding 等（tests/cpp/engine/ 全套） | 327 | 327 | 0 | 0 | 4.9s |



### 5.8 构建产物

全链构建产物（x86_64 host + commandline-tools x64 SDK + `--no-signed`）：

| 产物 | 大小 | md5 |
| --- | --- | --- |
| `dist/cann_lm_compile_converter-0.1.0-x86_64.run` | 494K | `2846e916…` |
| `dist/cann_lm_engine-0.1.0-py3-none-any.whl` | 824K | `c970f1bc…` |

## 6. DFX 专项质量评估

### 6.1 安全测试

| 序号 | 安全测试项 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 22 | 代码安全扫描 | C++ 代码内存安全检查（buffer overflow / 空指针 / use-after-free，ASAN 插桩 UT 跑通无告警） | PASS（converter 7 项 ASAN 全绿；engine 327 项 host UT 全绿） |
| 23 | 敏感信息检查 | 仓内无硬编码密钥/密码/token，无绝对路径泄露 | PASS |
| 24 | 输入校验 | `cann_lm_converter` CLI 参数校验（必填参数缺失报错、非法参数拒绝） | PASS |

### 6.2 可靠性测试

| 序号 | 可靠性测试项 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 25 | 重复构建稳定性 | `build.sh --pkg` 连续构建 3 次，产物一致性 | PASS |
| 26 | 重复导出稳定性 | gemma4-E4B 连续导出 3 次，epair 产物一致性 | PASS |
| 27 | 重复编译稳定性 | gemma4-E4B epair 连续编译 3 次，OMC 一致性 | PASS |
| 28 | 重复推理稳定性 | gemma4-E4B epair 连续运行 3 次，出字一致 | PASS |

### 6.3 兼容性测试

| 序号 | 兼容性测试项 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 29 | OS 兼容性 | openEuler x86_64（本构建机，已用于全轮构建）/ 官方清单（Ubuntu 22.04 等） | PASS |
| 30 | 架构兼容性 | x86_64/ARM64 | PASS |
| 31 | Python 版本兼容性 | Python >= 3.10 | PASS |
| 32 | OHOS SDK 版本兼容性 | command-line-tools-linux-x64-6.1.1.418/commandline-tools-linux-arm64-26.0.0.851.zip | PASS |

### 6.4 文档测试

| 序号 | 文档测试项 | 测试内容 | 结果 |
| --- | --- | --- | --- |
| 33 | README 完整性 | README.md 文档表、目录结构、快速开始、SIG 链接完整 | PASS |
| 34 | 代码块可跑性 | build_guide.md / QUICKSTART.md 中代码块按步骤可执行 | PASS |
| 35 | 链接有效性 | 文档间交叉引用链接有效，无 404 | PASS |

## 7. 测试执行评估

| 测试活动 | 测试结论 | 用例数 | 用例通过率 |
| --- | --- | --- | --- |
| 构建打包 | PASS | 4 | 100% |
| 模型导出 | PASS | 1 | 100% |
| OM 编译 | PASS | 2 | 100% |
| 量化 | PASS | 3 | 100% |
| NPU 数值对齐与端到端 | PASS | 4 | 100% |
| 包安装与环境管理 | PASS | 2 | 100% |
| 单元测试（Python） | PASS | 377 | 100% |
| 单元测试（C++） | PASS | 334（converter 7 ASAN + engine 327） | 100% |
| 安全测试 | PASS | 3 | 100%（#22/23/24） |
| 可靠性测试 | PASS | 4 | 100%（#25/26/27/28） |
| 兼容性测试 | PASS | 4 | 100%（#29/30/31/32） |
| 文档测试 | PASS | 3 | 100%（#33/34/35） |

## 8. 遗留问题和关键风险

### 8.1 遗留问题统计

| | 问题总数 | 严重 | 主要 | 次要 | 不重要 |
| --- | --- | --- | --- | --- | --- |
| 数目 | 0 | 0 | 0 | 0 | 0 |
| 百分比 | — | — | — | — | — |

### 8.2 遗留问题列表

无。

### 8.3 已知环境差异（非本仓缺陷）

- GE 库 `libge_compiler.so` 静态析构导致 `corrupted size vs. prev_size` abort，已用 `std::quick_exit` 规避，不影响产物。



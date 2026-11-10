# 开源版权与许可证声明规范

## 文档定义

本文档是本社区的**开源版权与许可证声明规范**，明确本社区仓库的许可选择（发布类默认 CANN-2.0）、文件头要求、分类治理与声明模板，指导维护者、贡献者与评审按统一口径完成声明与验收。

本文档适用于本社区托管的全部代码仓库。制品分发协议、商标规则、CLA 本身不在本文范围内，由社区另行规定。

---

## 1. 目的与原则

1. **声明清晰**：他人打开仓库或源文件时，能明确知道版权归属与使用许可。
2. **分层分级治理**：不同类型仓库采用不同治理规则，既能保证合规也能保证开发者体验，支持创新类代码快速合入。
3. **源码优先**：可执行、可编译、可被下游直接复用的**源码类文件**是声明重点；文档与配置类不强制逐文件声明。
4. **仓级必有许可**：无论何类仓库，根目录均须具备可读的 `LICENSE`。

### 1.1 为何要声明版权与许可证

#### 版权声明（Copyright）的意义与价值

| 价值 | 说明 |
|---|---|
| **标明权利主体** | 写明版权人（组织或个人）与年份，避免「无主代码」，使权属可识别、可追溯。 |
| **支撑贡献与权属管理** | 与 CLA / 贡献协议衔接，厘清个人贡献与组织贡献的关系，减少合入后的权属争议。 |
| **便于审计与举证** | 合规审查、客户尽调、纠纷处理时，可依据文件头与仓级声明定位权利人。 |
| **尊重原作者与再分发义务** | 引入或再分发代码时，保留原 Copyright 是多数开源许可的基本要求。 |

#### 许可证声明（License）的意义与价值

| 价值 | 说明 |
|---|---|
| **划清使用边界** | 明确下游能否使用、修改、再分发、商用，以及须履行的义务（如保留声明、同源公开等）。 |
| **降低合规与集成成本** | 仓级 `LICENSE` 与文件头中的许可指明，便于 SBOM / 扫描工具与人工审查快速判定，减少「无许可不敢用」。 |
| **建立上下游互信** | 对内统一 SIG / 门禁验收口径；对外向客户、合作方、开源社区表明本仓可合法复用、可合规引入。 |
| **避免默示风险** | 无有效许可声明时，合规实践上通常默认**不得随意商用或再分发**，反而阻碍代码被采用。 |

---

## 2. 仓库三类定义

| 类型 | 典型场景 | 许可与版权规则 | 文件头规则 |
|---|---|---|---|
| **发布类** | 正式产品组件、对外发布/配套的核心库与工具（算子库、运行时、框架适配、正式工具链等） | **必须**使用社区批准许可（默认 CANN Open Software License Agreement Version 2.0，或经评审批准的许可）；版权人按贡献与 CLA 如实填写（华为主导组件通常为 `Huawei Technologies Co., Ltd.`，联合贡献按实际署名）；仓级 `LICENSE` 见第 3 节 | **源码类文件必须**具备完整版权+许可证头（见第 5.1 节）；构建脚本等不强制（见第 5.2、5.3 节） |
| **创新类** | 高校/合作方联合创新、孵化课题、竞赛衍生可独立演进的实验仓、非产品主线的探索项目等 | **不强制** CANN-2.0；须选用 **OSI 批准**的开源许可（如 MulanPSL-2.0、Apache-2.0、MIT、BSD-3-Clause 等，清单见 [opensource.org/licenses](https://opensource.org/licenses)），并在仓级 `LICENSE` 与源码文件中规范声明版权人与许可（见第 3、6 节） | **源码类文件建议**有规范文件头 |
| **文档指南类** | 纯文档、教程、指南、规范汇编、活动说明、几乎无自研源码的配置/元数据仓等 | **必须**有仓级 `LICENSE`（见第 3 节）；许可可选 CANN-2.0 或 MulanPSL-2.0 / Apache-2.0 / MIT / BSD-3-Clause 等友好许可 | **不强制**逐文件头；若仓内含少量示例源码，该源码建议按创新类或发布类从高要求侧遵守 |

> **判定提示**：同一仓库以主用途为准。若文档仓中附带大量可运行示例源码且对外作为可复用代码分发，应升格为创新类或发布类，或将示例拆仓。

---

## 3. 仓级 LICENSE 规范

根目录 `LICENSE` 是整仓许可的**条款文本**，无论发布类、创新类还是文档指南类均**必须**具备。仓库类型总则见第 2 节；本节按类型说明仓级 `LICENSE` 的操作要点。

### 3.1 共性要求

1. **位置**：放在仓库根目录，文件名建议 `LICENSE`，便于工具与访客识别。
2. **内容**：须为所选许可证的**完整正文**（或社区批准许可的官方全文），禁止仅写一句「本项目开源」而无具体条款。
3. **与源码文件声明一致**：源码文件中写明的许可名称 / SPDX 标识，须与仓级 `LICENSE` 所载许可一致。
4. **可读性**：使用纯文本；勿以扫描件 PDF、图片代替。
5. **变更**：更换仓级许可须经约定评审（如 SIG / PMC）确认，并同步更新源码文件头与 README 中的许可说明。

### 3.2 发布类

1. **默认许可**：仓级 `LICENSE` 放置 **CANN Open Software License Agreement Version 2.0（CANN-2.0）** 官方全文；若使用经社区评审批准的其他许可，须同样放置该许可全文。
2. **获取与放置**：从社区官方渠道（如 `cann-agreements`）获取 CANN-2.0 全文，原样放入根目录 `LICENSE`，勿自行删改条款。
3. **版权人**：按贡献与 CLA 如实填写；主导组件通常为相应组织署名，联合贡献按实际署名。

### 3.3 创新类

创新类仓库在仓级选许可上把握以下要点（类型总则见第 2 节）：

1. **不强制 CANN-2.0**  
   联合创新、高校课题、孵化实验等场景，可采用贡献方更熟悉的常见开源许可，降低合入与协作摩擦。

2. **必须选用 OSI 批准的开源许可**  
   推荐优先考虑社区常用、兼容性较好的许可，例如：
   - 木兰宽松许可证，第2版（`MulanPSL-2.0`）
   - Apache License 2.0（`Apache-2.0`）
   - MIT License（`MIT`）
   - BSD 3-Clause（`BSD-3-Clause`）
   - 以及其他 OSI 已批准许可

3. **从哪里获取正式许可文本**  
   - OSI 批准许可列表与说明：**<https://opensource.org/licenses>**  
   - 选定后，将官方全文复制到本仓根目录 `LICENSE`；源码文件使用对应全称或 SPDX 短标识，并指向根目录 `LICENSE`。

4. **版权人如实声明**  
   按项目实际情况填写版权人（如高校、合作方、个人或联合署名等），并与 CLA / 贡献约定一致。

5. **一仓一主许可**  
   创新类仓应有清晰的主许可证；引入三方代码时保留其原许可与声明，并在 Notice/List 中登记，禁止把上游树批量改成与主许可不符的头。

### 3.4 文档指南类

1. **必须有仓级 `LICENSE`**：即使几乎无自研源码、以文档为主，根目录仍须具备完整许可正文。
2. **许可可选**：可为 CANN-2.0，或 MulanPSL-2.0 / Apache-2.0 / MIT / BSD-3-Clause 等友好开源许可；选定后将官方全文放入 `LICENSE`。OSI 许可列表见 <https://opensource.org/licenses>。

### 3.5 仓级 LICENSE 完整声明模板示例

#### （1）CANN-2.0

```text
CANN Open Software License Agreement Version 2.0
              
This CANN Open Software License Agreement Version 2.0 (hereinafter referred to as this "Agreement") is a legal agreement between you and Huawei, and it governs your use, modification, or distribution of CANN Open Software (hereinafter referred to as "Software"). Please read this Agreement carefully.

If you are entering into this Agreement on behalf of a company or other legal entity, you represent that you have the legal authority to bind that entity to this Agreement, in which case "you" will mean the entity you represent.

BY DOWNLOADING, INSTALLING, OR USING THE SOFTWARE, YOU AGREE YOU HAVE FULLY UNDERSTOOD AND ACCEPTED THE TERMS CONTAINED HEREIN. IF YOU DO NOT AGREE TO ANY OF THE TERMS OF THIS AGREEMENT, OR IF YOU DO NOT QUALIFY FOR AGREEING TO THIS AGREEMENT, YOU ARE NOT AUTHORIZED TO AND SHALL NOT DOWNLOAD, INSTALL, OR MAKE ANY USE OF THE SOFTWARE.

1. Definition

1.1   Software means the APIs, source code files, binaries, and related documents of Compute Architecture for Neural Networks("CANN") that are licensable by Huawei, and provided and licensed under this Agreement.

1.2   Huawei AI Processors mean AI chipsets (i) branded with "Ascend", "Kirin"," Yueying" or other brands owned or controlled by Huawei; or (ii) manufactured (including have manufactured), supplied (including have supplied) or designed (including have designed) by Huawei.

2.  Grant of Intellectual Property Rights
2.1 Subject to the terms and conditions of this Agreement, including your full compliance thereof, Huawei hereby grants you a limited, worldwide, royalty-free, non-transferable, non-sublicensable, and revocable license for you to (i) download, use, modify, integrate, and distribute the Software or its derivative works for the purpose of developing software solely for use in systems with Huawei AI Processors and/or Software, and (ii) distribute any software developed based upon Software and/or its derivative works solely for use in systems with Huawei AI Processors and/or Software. 

3.  Restrictions
3.1 You are not authorized to, and shall not use, modify, or distribute this Software or its derivative works for any other purposes than those expressly permitted by this Agreement. You shall not make any use of the Software or its derivative works to develop or distribute any software for use in systems with processors other than Huawei AI Processors. All rights not expressly granted herein are expressly reserved by Huawei.

3.2 You are not authorized to, and shall not remove, obscure, or alter any copyright or other notices in this Software or any part of it.

3.3 Distribution Restrictions 
You may distribute the Software or its derivative works in any medium, whether in source or executable forms, for the purpose stipulated in Section 2; provided that you provide recipients with a copy of this Agreement, and retain all notices in the Software.

4. Disclaimer of Warranty and Limitation of Liability
THE SOFTWARE IS PROVIDED WITHOUT WARRANTIES OF ANY KIND, EITHER EXPRESS OR IMPLIED. IN NO EVENT SHALL HUAWEI OR ANY OTHER COPYRIGHT HOLDER BE LIABLE TO YOU FOR ANY DAMAGES, INCLUDING, BUT NOT LIMITED TO ANY DIRECT, OR INDIRECT, SPECIAL OR CONSEQUENTIAL DAMAGES ARISING FROM YOUR USE OR INABILITY TO USE THE SOFTWARE, IN WHOLE OR IN PART, NO MATTER HOW IT IS CAUSED OR THE LEGAL THEORY IT IS BASED ON, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.

5. Termination
5.1 This Agreement will continue to apply until terminated by either you or Huawei as described below:
a．You may terminate this Agreement by ceasing your use of the Software;
b.  Huawei may at any time, terminate this Agreement if: (i) you fail to comply with any term of this Agreement; or (ii) you directly or indirectly initiate any legal proceeding against any individual or entity by alleging that the Software or any part of it infringes your intellectual property rights.
5.2 By termination, all the rights granted to you under this Agreement are terminated, and you shall cease to use and delete this Software or any derivative works immediately. All rights granted to you under this Agreement shall hereby be void ab initio in the event of termination in accordance with Section 5.1. b above. Huawei reserves the right to pursue any and all legal remedies available to enforce the terms and conditions of this Agreement or to protect Huawei’s intellectual property rights for such breach or violation. All provisions shall survive the termination of this Agreement except for Section 2 and Section 3.3.

6. MISCELLANEOUS
If the application of any provision of this Agreement to any particular facts or circumstances is held to be invalid or unenforceable by a court of competent jurisdiction, then (a) the validity and enforceability of such provision as applied to any other particular facts or circumstances and the validity of other provisions of this Agreement shall not in any way be affected or impaired thereby and (b) such provision shall be enforced to the maximum extent possible so as to affect the intent of the you and Huawei and reformed without further action by you and Huawei to the extent necessary to make such provision valid and enforceable.

END OF THE TERMS AND CONDITIONS
```

#### （2）木兰宽松许可证，第2版 / MulanPSL-2.0（创新类等可选）

官方说明：<http://license.coscl.org.cn/MulanPSL2>。该许可证以中英文双语表述、两版本具有同等法律效力，放入根目录 `LICENSE` 时应保留完整双语正文：

```text
木兰宽松许可证，第2版

木兰宽松许可证，第2版
2020年1月 http://license.coscl.org.cn/MulanPSL2

您对“软件”的复制、使用、修改及分发受木兰宽松许可证，第2版（“本许可证”）的如下条款的约束：

0. 定义

“软件”是指由“贡献”构成的许可在“本许可证”下的程序和相关文档的集合。

“贡献”是指由任一“贡献者”许可在“本许可证”下的受版权法保护的作品。

“贡献者”是指将受版权法保护的作品许可在“本许可证”下的自然人或“法人实体”。

“法人实体”是指提交贡献的机构及其“关联实体”。

“关联实体”是指，对“本许可证”下的行为方而言，控制、受控制或与其共同受控制的机构，此处的控制是指有受控方或共同受控方至少50%直接或间接的投票权、资金或其他有价证券。

1. 授予版权许可

每个“贡献者”根据“本许可证”授予您永久性的、全球性的、免费的、非独占的、不可撤销的版权许可，您可以复制、使用、修改、分发其“贡献”，不论修改与否。

2. 授予专利许可

每个“贡献者”根据“本许可证”授予您永久性的、全球性的、免费的、非独占的、不可撤销的（根据本条规定撤销除外）专利许可，供您制造、委托制造、使用、许诺销售、销售、进口其“贡献”或以其他方式转移其“贡献”。前述专利许可仅限于“贡献者”现在或将来拥有或控制的其“贡献”本身或其“贡献”与许可“贡献”时的“软件”结合而将必然会侵犯的专利权利要求，不包括对“贡献”的修改或包含“贡献”的其他结合。如果您或您的“关联实体”直接或间接地，就“软件”或其中的“贡献”对任何人发起专利侵权诉讼（包括反诉或交叉诉讼）或其他专利维权行动，指控其侵犯专利权，则“本许可证”授予您对“软件”的专利许可自您提起诉讼或发起维权行动之日终止。

3. 无商标许可

“本许可证”不提供对“贡献者”的商品名称、商标、服务标志或产品名称的商标许可，但您为满足第4条规定的声明义务而必须使用除外。

4. 分发限制

您可以在任何媒介中将“软件”以源程序形式或可执行形式重新分发，不论修改与否，但您必须向接收者提供“本许可证”的副本，并保留“软件”中的版权、商标、专利及免责声明。

5. 免责声明与责任限制

“软件”及其中的“贡献”在提供时不带任何明示或默示的担保。在任何情况下，“贡献者”或版权所有者不对任何人因使用“软件”或其中的“贡献”而引发的任何直接或间接损失承担责任，不论因何种原因导致或者基于何种法律理论，即使其曾被建议有此种损失的可能性。

6. 语言

“本许可证”以中英文双语表述，中英文版本具有同等法律效力。如果中英文版本存在任何冲突不一致，以中文版为准。

条款结束

如何将木兰宽松许可证，第2版，应用到您的软件

如果您希望将木兰宽松许可证，第2版，应用到您的新软件，为了方便接收者查阅，建议您完成如下三步：

1， 请您补充如下声明中的空白，包括软件名、软件的首次发表年份以及您作为版权人的名字；
2， 请您在软件包的一级目录下创建以“LICENSE”为名的文件，将整个许可证文本放入该文件中；
3， 请将如下声明文本放入每个源文件的头部注释中。

Copyright (c) [Year] [name of copyright holder]
[Software Name] is licensed under Mulan PSL v2.
You can use this software according to the terms and conditions of the Mulan PSL v2.
You may obtain a copy of Mulan PSL v2 at:
         http://license.coscl.org.cn/MulanPSL2
THIS SOFTWARE IS PROVIDED ON AN "AS IS" BASIS, WITHOUT WARRANTIES OF ANY KIND,
EITHER EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO NON-INFRINGEMENT,
MERCHANTABILITY OR FIT FOR A PARTICULAR PURPOSE.
See the Mulan PSL v2 for more details.

Mulan Permissive Software License，Version 2

Mulan Permissive Software License，Version 2 (Mulan PSL v2)
January 2020 http://license.coscl.org.cn/MulanPSL2

Your reproduction, use, modification and distribution of the Software shall be subject to Mulan PSL v2 (this License) with the following terms and conditions:

0. Definition

Software means the program and related documents which are licensed under this License and comprise all Contribution(s).

Contribution means the copyrightable work licensed by a particular Contributor under this License.

Contributor means the Individual or Legal Entity who licenses its copyrightable work under this License.

Legal Entity means the entity making a Contribution and all its Affiliates.

Affiliates means entities that control, are controlled by, or are under common control with the acting entity under this License, 'control' means direct or indirect ownership of at least fifty percent (50%) of the voting power, capital or other securities of controlled or commonly controlled entity.

1. Grant of Copyright License

Subject to the terms and conditions of this License, each Contributor hereby grants to you a perpetual, worldwide, royalty-free, non-exclusive, irrevocable copyright license to reproduce, use, modify, or distribute its Contribution, with modification or not.

2. Grant of Patent License

Subject to the terms and conditions of this License, each Contributor hereby grants to you a perpetual, worldwide, royalty-free, non-exclusive, irrevocable (except for revocation under this Section) patent license to make, have made, use, offer for sale, sell, import or otherwise transfer its Contribution, where such patent license is only limited to the patent claims owned or controlled by such Contributor now or in future which will be necessarily infringed by its Contribution alone, or by combination of the Contribution with the Software to which the Contribution was contributed. The patent license shall not apply to any modification of the Contribution, and any other combination which includes the Contribution. If you or your Affiliates directly or indirectly institute patent litigation (including a cross claim or counterclaim in a litigation) or other patent enforcement activities against any individual or entity by alleging that the Software or any Contribution in it infringes patents, then any patent license granted to you under this License for the Software shall terminate as of the date such litigation or activity is filed or taken.

3. No Trademark License

No trademark license is granted to use the trade names, trademarks, service marks, or product names of Contributor, except as required to fulfill notice requirements in section 4.

4. Distribution Restriction

You may distribute the Software in any medium with or without modification, whether in source or executable forms, provided that you provide recipients with a copy of this License and retain copyright, patent, trademark and disclaimer statements in the Software.

5. Disclaimer of Warranty and Limitation of Liability

THE SOFTWARE AND CONTRIBUTION IN IT ARE PROVIDED WITHOUT WARRANTIES OF ANY KIND, EITHER EXPRESS OR IMPLIED. IN NO EVENT SHALL ANY CONTRIBUTOR OR COPYRIGHT HOLDER BE LIABLE TO YOU FOR ANY DAMAGES, INCLUDING, BUT NOT LIMITED TO ANY DIRECT, OR INDIRECT, SPECIAL OR CONSEQUENTIAL DAMAGES ARISING FROM YOUR USE OR INABILITY TO USE THE SOFTWARE OR THE CONTRIBUTION IN IT, NO MATTER HOW IT'S CAUSED OR BASED ON WHICH LEGAL THEORY, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.

6. Language

THIS LICENSE IS WRITTEN IN BOTH CHINESE AND ENGLISH, AND THE CHINESE VERSION AND ENGLISH VERSION SHALL HAVE THE SAME LEGAL EFFECT. IN THE CASE OF DIVERGENCE BETWEEN THE CHINESE AND ENGLISH VERSIONS, THE CHINESE VERSION SHALL PREVAIL.

END OF THE TERMS AND CONDITIONS

How to Apply the Mulan Permissive Software License，Version 2 (Mulan PSL v2) to Your Software

To apply the Mulan PSL v2 to your work, for easy identification by recipients, you are suggested to complete following three steps:

i. Fill in the blanks in following statement, including insert your software name, the year of the first publication of your software, and your name identified as the copyright owner;
ii. Create a file named "LICENSE" which contains the whole context of this License in the first directory of your software package;
iii. Attach the statement to the appropriate annotated syntax at the beginning of each source file.

Copyright (c) [Year] [name of copyright holder]
[Software Name] is licensed under Mulan PSL v2.
You can use this software according to the terms and conditions of the Mulan PSL v2.
You may obtain a copy of Mulan PSL v2 at:
         http://license.coscl.org.cn/MulanPSL2
THIS SOFTWARE IS PROVIDED ON AN "AS IS" BASIS, WITHOUT WARRANTIES OF ANY KIND,
EITHER EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO NON-INFRINGEMENT,
MERCHANTABILITY OR FIT FOR A PARTICULAR PURPOSE.
See the Mulan PSL v2 for more details.
```

#### （3）MIT（创新类等可选）

官方说明：<https://opensource.org/license/mit>。将 `<yyyy>`、`[name of copyright owner]` 替换为实际情况后，整份作为根目录 `LICENSE`：

```text
MIT License

Copyright (c) <yyyy> [name of copyright owner]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

> 选用 Apache-2.0 等其他 OSI 许可时，从 <https://opensource.org/licenses> 获取对应**官方全文**放入 `LICENSE`，写法同理。源码文件头部声明模板见第 6 节。

---

## 4. 源码文件「完整声明」的最低内容

对需要文件头的文件，头部声明须同时包含：

1. **Copyright 行**：年份 + 版权人（组织或个人）
2. **许可证指明**：许可证全称或 SPDX 短标识，并说明「详见根目录 LICENSE」或给出许可证官方链接

仅写 `Copyright` 而无许可指明，或仅写仓级 `LICENSE` 文件名而无版权人，均视为**源码文件声明不完整**。

引入第三方开源代码片段时，另须遵守社区《片段引用指导》：本项目声明 + 来源声明 + 原项目版权与许可原文。

---

## 5. 源码文件按后缀的覆盖规则

下列规则适用于**仓库自有文件**的文件头。第三方完整拷贝树、生成物、二进制等按第 5.4 节处理。

### 5.1 源码类

下列后缀的**新建与修改的自有源文件**，必须包含完整版权+许可证头：

| 类别 | 后缀 / 文件名 |
|---|---|
| C/C++ | `.c` `.cc` `.cpp` `.cxx` `.h` `.hh` `.hpp` `.hxx` `.inl` `.inc` |
| GPU/NPU 相关 | `.cu` `.cuh` `.cl` |
| Python | `.py` `.pyi` `.pyx` `.pxd` |
| JS/TS | `.js` `.jsx` `.mjs` `.cjs` `.ts` `.tsx` |
| 其他语言 | `.go` `.rs` `.java` `.kt` `.scala` `.swift` `.m` `.mm` `.s` `.asm` |
| MLIR / IR | `.mlir` `.td` `.ll` `.metal` |
| 接口描述 | `.proto` `.thrift` `.sql` |
| Fortran | `.f` `.f90` `.f95` `.for` |
| Shell | `.sh` `.bash` `.zsh` `.ksh` `.fish` |
| PowerShell / 批处理 | `.ps1` `.cmd` `.bat` |

> 发布类：许可与版权须符合第 2 节；仓级操作见第 3.2 节。  
> 创新类：许可与版权人可按实际项目填写，格式须完整规范；仓级选许可见第 3.3 节。  
> 文档指南类：仓级操作见第 3.4 节。  
> **可执行脚本**（`.sh` / `.bash` / `.ps1` / `.cmd` / `.bat` 等）：默认同源码类必须带头；仅当符合第 5.4 节「纯构建 / CI 编排」等豁免条件时可不声明。含核心逻辑、对外工具入口或可被下游直接复用的脚本**必须**带头。

### 5.2 构建脚本 / 类源码

下列构建与脚本文件**不强制**文件头；仓级 `LICENSE` 已覆盖整仓许可。新建时可按需带头，若文件中已有历史文件头，可保留，不要求删除。

| 类别 | 后缀 / 文件名 |
|---|---|
| CMake | `CMakeLists.txt` `.cmake` |
| Make | `Makefile` `GNUmakefile` `*.mk` |
| Bazel | `.bzl` `BUILD` `BUILD.bazel` `WORKSPACE` |

### 5.3 非源码类

下列类型**不强制**文件头；仓级 `LICENSE` 已覆盖整仓许可。若文件中已有历史文件头，可保留，不要求删除。

| 类别 | 典型后缀 / 文件 | 说明 |
|---|---|---|
| 文档 | `.md` `.rst` `.adoc` `.txt` | 文档指南类主体 |
| 配置 | `.yml` `.yaml` `.json` `.toml` `.ini` `.cfg` `.conf` | 工具配置 |
| 锁与清单 | `package-lock.json` `pnpm-lock.yaml` `Cargo.lock` `go.sum` 等 | 生成/锁定 |
| 许可与合规元数据 | `LICENSE*` `NOTICE*` `OAT.xml` `Third_Party_Open_Source_Software_*` `SECURITY.md` `CODEOWNERS` | 本身即声明载体 |
| 编辑器/VCS | `.gitignore` `.gitattributes` `.editorconfig` `.clang-format` `.clang-tidy` 等 | |
| 资源与二进制 | `.png` `.jpg` `.svg` `.gif` `.pdf` `.whl` `.so` `.a` `.o` 等 | 二进制禁止随意入库；资源不强制头 |
| Notebook | `.ipynb` | 默认不强制；若作为正式发布的可复用代码载体，发布类建议在 README/LICENSE 说明，并尽量将核心逻辑抽到 `.py` 并带头 |

### 5.4 一律豁免或特殊处理

| 情形 | 要求 |
|---|---|
| `third_party/` / `vendor/` / 上游镜像完整树 | 保留上游原有声明；禁止改写为 CANN 许可证；在 Notice/List 中登记 |
| 测试夹具中的第三方片段 | 保留原声明；或按片段引用指导处理 |
| 超大文件 / 纯数据文件 | 不强制头；发布类避免把需声明的逻辑藏在数据文件中 |
| **可执行脚本豁免（须同时满足「纯编排」特征）** | 见下方专条；不满足则按第 5.1 节必须带头 |

#### 可执行脚本（Shell / PowerShell / 批处理）可豁免不声明的情形

`.sh` / `.bash` / `.zsh` / `.ps1` / `.cmd` / `.bat` 等默认属源码类（第 5.1 节）。下列情形**可以**不逐文件声明，许可由仓级 `LICENSE` 覆盖；**不得**借豁免把核心逻辑留在无头脚本中。

| 可豁免情形 | 判定要点 | 示例 |
|---|---|---|
| **纯构建 / CI 编排** | 仅串联 `cmake` / `make` / `ninja`、拷贝产物、设置环境变量；无可复用算法或业务逻辑 | `ci/build.sh` 只调 `cmake --build`；`scripts/run_tests.ps1` 只循环调用已带头的测试 |
| **安装 / 打包编排** | 解压、改权限、调用安装器，无独立实现 | `packaging/install.sh` 仅 `cp`/`ln`/`chmod`；`packaging/install.bat` 仅 `copy`/`xcopy` |
| **仅转发的入口脚本** | 实质只有 `exec` / `&` 转发或调用已带头程序 | `bin/tool` → `exec .../libexec/tool "$@"` |
| **机器生成** | 由生成器产出；建议在模板中内置声明 | 配置模板展开出的 `generated/*.sh` / `generated/*.ps1` |
| **第三方树内脚本** | 位于 `third_party/` / `vendor/` 等，保留上游声明 | 上游自带的 `bootstrap.sh` / `build.bat` |
| **测试夹具脚本** | 作为测试数据或夹具，无对外复用意图 | `testdata/fixtures/run_once.sh` |

**不得豁免**：对外发布的 CLI / 工具入口、含业务或算法的运维脚本、可被下游直接拷贝复用的部署 / 编排脚本、示例与模板中的可运行脚本、「表面为编排脚本但实际内嵌大量自研逻辑」的脚本。有疑义时按**必须带头**处理。

---

## 6. 源码文件声明模板

> 以下模板用于**文件头部**声明；仓级许可全文仍须按第 3 章放入根目录 `LICENSE`。

### 6.1 发布类（CANN Open Software License Agreement Version 2.0）

C/C++ 等块注释：

```text
/*
 * Copyright (c) <yyyy> [name of copyright owner].
 * This program is free software, you can redistribute it and/or modify it under the terms and conditions of
 * CANN Open Software License Agreement Version 2.0 (the "License").
 * Please refer to the License for details. You may not use this file except in compliance with the License.
 * THIS SOFTWARE IS PROVIDED ON AN "AS IS" BASIS, WITHOUT WARRANTIES OF ANY KIND, EITHER EXPRESS OR IMPLIED,
 * INCLUDING BUT NOT LIMITED TO NON-INFRINGEMENT, MERCHANTABILITY, OR FITNESS FOR A PARTICULAR PURPOSE.
 * See LICENSE in the root of the software repository for the full text of the License.
 */
```

Python / Shell 等行注释：将上述内容改为 `#` 行首即可。

> `<yyyy>`：首次创建年；若规范要求双年份，可采用 `2021-2026`（首创–最近重大修改）。  
> `[name of copyright owner]`：按 CLA 与实际权利归属填写（个人署名或雇主/组织名称）。

### 6.2 创新类

**核心说明**：创新类**可选** CANN-2.0 或 MulanPSL-2.0、Apache-2.0、MIT、BSD-3-Clause 等其他许可证，建议从官方渠道获取标准的版权声明头。你可以访问 [OSI 许可列表](https://opensource.org/licenses) 或该许可证的官方网站查询具体要求。

长形式文件头示例(木兰宽松许可证第2版 MulanPSL-2.0)：

```text
# Copyright (c) <yyyy> [name of copyright owner]
# [Software Name] is licensed under Mulan PSL v2.
# You can use this software according to the terms and conditions of the Mulan PSL v2.
# You may obtain a copy of Mulan PSL v2 at:
#          http://license.coscl.org.cn/MulanPSL2
# THIS SOFTWARE IS PROVIDED ON AN "AS IS" BASIS, WITHOUT WARRANTIES OF ANY KIND, EITHER EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO NON-INFRINGEMENT, MERCHANTABILITY OR FIT FOR A PARTICULAR
# PURPOSE.
# See the Mulan PSL v2 for more details.
```

长形式文件头示例(Apache-2.0)：

```text
# Copyright (c) <yyyy> [name of copyright owner]
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
```

短形式（同一仓库内应统一长/短风格）：

```text
# Copyright (c) <yyyy> [name of copyright owner]
# SPDX-License-Identifier: Apache-2.0
```

> 根目录必须有与 SPDX / 文件头一致的完整 `LICENSE` 文本。其他 OSI 许可将 `Apache-2.0` 替换为对应 SPDX 即可（如 `MulanPSL-2.0`、`MIT`、`BSD-3-Clause`）。

### 6.3 文档指南类

- 根目录 `LICENSE` 即可（要求见第 3 节）。
- 不要求 `.md` 等文件增加文件头。
- 若贡献者自愿在文档中增加版权页或页眉声明，须符合仓级许可证的要求。

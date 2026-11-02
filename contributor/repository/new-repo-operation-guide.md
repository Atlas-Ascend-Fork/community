# CANN社区新建仓与仓开放操作指引

> 本指引结合TSC、PMC会议时间，为开发者提供清晰的操作步骤和时间安排建议。

## 一、会议时间速查表

### 关键评审会议（必须参加）

| 组织 | 会议时间 | 频次 | 评审内容 | 纪要链接 |
|-----|---------|------|---------|---------|
| **QA-SIG** | 双周二 10:30-12:00 | 双周 | 测试报告/开源评审 | [QA纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-qa) |

### 核心决策会议（必须参加）

| 组织 | 会议时间 | 频次 | 评审内容 | 申报方式 | 纪要链接 |
|-----|---------|------|---------|---------|---------|
| **TSC** | 月末周六 | 月度 | 新建仓/SIG创建审批 | 纪要申报 | [TSC纪要](https://etherpad-cann.meeting.osinfra.cn/p/TSC) |
| **PMC** | 双周三 14:00-16:00 | 双周 | 开源审批/版本发布审批 | 纪要申报 | [PMC纪要](https://etherpad-cann.meeting.osinfra.cn/p/PMC) |

### 其他会议（可选/按需参加）

| 组织 | 会议时间 | 频次 | 说明 | 纪要链接 |
|-----|---------|------|------|---------|
| **Infrastructure SIG** | 双周二 14:00-15:00 | 双周 | CI配置讨论，建仓通过Issue异步执行 | [Infra纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-infrastructure) |
| **Security SIG** | 月末周五 10:00-12:00 | 按需 | 三方件引入申请时需参加，不涉及三方引入则不需要关注 | [Security纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-security) |


---

## 二、新建仓完整流程

> **线上申请入口（以电子流为准）**：新建仓通过 [CANN 数字化协作平台](https://digital.hicann.cn/#/repo_manage/all_repo) 电子流提交（评审准备 → 材料预审 → TSC 评审 → 建仓申请 → 基础设施审批 → CI 与 SIG 配置 → 配置生效 → 绑定账号，共 8 阶段，系统自动建仓并跟踪 CI/SIG 的 Issue 与 PR 状态）。本节"第 3 步"的建仓 Issue 为电子流第 4 阶段的组成部分。**流程阶段定义以电子流为准**，本节流程图如与电子流不一致，以[数字化平台建仓与开源电子流指引](digital-platform-repo-workflow.md)为准。

### 流程图

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           新建仓流程（约2-3周）                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  第1步：准备材料+申报议题（会议前任意时间）                                     │
│  ├─ 下载模板：新建仓申报模板 v0.2.pptx       │
│  ├─ 填写：仓库名称、目标、技术方案、维护者等                                   │
│  ├─ 申报方式：直接在TSC纪要填写议题                                          │
│  └─ 格式：「1. XXX仓库新建申请 -- 申请人：XXX」                               │
│                                                                             │
│  第2步：TSC会议评审 ⏰ 月末周六                                               │
│  ├─ 在会议上陈述建仓方案                                                     │
│  ├─ TSC委员投票（需2/3赞同）                                                 │
│  └─ 通过后记录评审纪要                                                       │
│                                                                             │
│  第3步：基础设施团队执行建仓                                              │
│  ├─ 向 infrastructure 提交Issue申请建仓                                      │
│  ├─ 申请者通过[CANN数字化平台](https://digital.hicann.cn/#/repo_manage/all_repo)提交建仓申请 │
│  ├─ 附上TSC评审纪要截图                                                          │
│  └─ 基础设施团队同步审批并执行仓库创建                                       │
│  ↓（以下步骤并行执行）                                                       │
│                                                                             │
│  第4步：CI流水线配置（并行）                                                 │
│  ├─ 向 infrastructure 提交Issue申请CI配置                                    │
│  ├─ 提供：编译命令、UT运行命令                                               │
│  └─ 基础设施团队配置门禁和每日构建                                            │
│                                                                             │
│  第5步：权限配置（并行）                                                     │
│  ├─ Fork cann/community               │
│  ├─ 修改 org-info.yaml（添加仓库到对应SIG）                                  │
│  ├─ 提交PR，获得tsc_member评审                                              │
│  └─ 创建 sig-info.yaml（配置maintainer/committer）                          │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

**补充说明**：如需同步创建SIG和仓库，可在同一次TSC会议评审两个议题

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     同步创建SIG和仓库流程（约2-3周）                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  第1步：准备材料+申报议题（会议前任意时间）                                     │
│  ├─ SIG申请：下载SIG组申报模板PPT                                             │
│  ├─ 建仓申请：下载新建仓申报模板PPT                                            │
│  ├─ 申报方式：在TSC纪要填写议题                                              │
│  └─ 格式：「XXX SIG新建申请及仓库新建 -- 申请人：XXX」                        │
│                                                                             │
│  第2步：TSC会议评审 ⏰ 月末周六（同一次会议）                                    │
│  ├─ 同时陈述SIG申请和建仓申请                                                 │
│  ├─ TSC委员投票（需2/3赞同）                                                 │
│  └─ 通过后记录评审纪要                                                       │
│                                                                             │
│  第3步：基础设施团队执行建仓                                                  │
│  ├─ 向 infrastructure 提交Issue申请建仓                                      │
│  ├─ 申请者通过[CANN数字化平台](https://digital.hicann.cn/#/repo_manage/all_repo)提交建仓申请 │
│  ├─ 附上TSC评审纪要                                                          │
│  └─ 基础设施团队同步审批并执行仓库创建                                       │
│  ↓（以下步骤并行执行）                                                       │
│                                                                             │
│  第4步：CI流水线配置（并行）                                                  │
│  ├─ 向 infrastructure 提交Issue申请CI配置                                    │
│  ├─ 提供：编译命令、UT运行命令                                               │
│  └─ 基础设施团队配置门禁和每日构建                                            │
│                                                                             │
│  第5步：创建SIG配置（并行，需按顺序提交PR）                                    │
│  ├─ PR1：修改 org-info.yaml（同时添加SIG定义和仓库）                          │
│  │   └─ 提交PR，获得tsc_member评审合入                                        │
│  ├─ PR2：在sigs目录创建SIG目录                                               │
│  │   ├─ 创建 sig-info.yaml（配置maintainer/committer）                       │
│  │   ├─ 创建 README.md（SIG介绍、会议时间、成员信息）                          │
│  │   └─ 提交PR，获得tsc_member评审合入                                        │
│  └─ 申请邮件列表（可选）：参阅[基础设施支撑矩阵](https://gitcode.com/cann/infrastructure/blob/master/docs/services.md) │
│                                                                             │
│  第6步：绑定账号获取会议权限                                                  │
│  ├─ 登录会议平台绑定GitCode账号与华为账号                                     │
│  └─ SIG maintainer/committer自动获得创建会议权限                              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 关键时间节点

| 阶段 | 时间安排 | 操作 | 等待时间 |
|-----|---------|------|---------|
| 准备材料+申报议题 | 会议前任意时间 | 填写PPT模板，在TSC纪要申报 | 无限制 |
| TSC评审 | 月末周六 | 参加会议陈述方案 | 当天 |
| 基础设施执行 | 评审后1-3天 | 提交建仓Issue | 异步处理 |
| CI配置 | 评审后1-3天 | 提交CI配置Issue（并行） | 异步处理 |
| 权限配置 | 评审后1-3天 | 修改community配置PR（并行） | 等待评审合入 |

**总耗时：约2-3周**（主要取决于TSC会议周期和PR评审时间）

**同步创建SIG和仓库时间节点**：

| 阶段 | 时间安排 | 操作 | 说明 |
|-----|---------|------|------|
| 准备材料+申报 | 会议前任意时间 | 同时准备SIG和建仓PPT，在TSC纪要申报两个议题 | 无时间限制 |
| TSC评审 | 月末周六 | 同时陈述SIG申请和建仓申请 | 同一次会议完成 |
| 基础设施执行 | 评审后1-3天 | 提交建仓Issue+CI配置Issue（并行） | 异步处理 |
| SIG配置PR1 | 评审后1-3天 | 修改org-info.yaml（添加SIG定义和仓库） | 需等待评审合入 |
| SIG配置PR2 | PR1合入后 | 创建sigs目录、sig-info.yaml、README.md | 需等待评审合入 |

**同步创建SIG和仓库总耗时：约2-3周**（主要取决于TSC会议周期和PR评审时间）

**关键点**：
- SIG申请和建仓申请可在同一次TSC会议评审
- org-info.yaml PR可同时包含SIG定义和仓库定义
- SIG配置PR需按顺序提交（PR1合入后才能提交PR2）

**说明**：
- 准备材料和申报议题可在任何时间进行，无时间限制
- 只需确保在月末周六TSC会议召开前准备好即可
- CI配置和权限配置可与基础设施执行同步进行

---

## 三、新仓库开源流程

> **线上申请入口（以电子流为准）**：开源申请由**仓库责任人**通过 [CANN 数字化协作平台](https://digital.hicann.cn/#/repo_manage/open_source_repo_application) 电子流发起（开源条件自查与测试报告 → QA-SIG 预审 → QA-SIG 评审 → PMC 预审 → PMC 评审 → 基础设施审视 → 正式开源，共 7 阶段；自查表单含 **TSC 评审时间/截图**项，即开源流程含 TSC 评审环节）。**流程阶段定义以电子流为准**，本节流程图如与电子流不一致，以[数字化平台建仓与开源电子流指引](digital-platform-repo-workflow.md)为准。

> 开源审批流程中，QA-SIG 评审会对照[仓库开源条件与目录结构指引](open-source-checklist.md)逐项审视仓库是否满足开源条件（文档/安全合规/工程规范/CI/测试报告/权限），建议在申报 QA-SIG 议题前先按该指引自查。

### 流程图

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      新仓库开源流程（约1-2周）                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  第0步：数字化平台发起开源申请（电子流入口）                                  │
│  └─ 仓库责任人通过[CANN数字化平台](https://digital.hicann.cn/#/repo_manage/open_source_repo_application)提交开源申请 │
│  └─ 电子流第1阶段：开源条件自查与测试报告（TSC评审时间/截图、测试报告PR链接、自查清单）│
│                                                                             │
│  第1步：准备测试报告                                                         │
│  └─ 使用测试报告模板                                                         │
│  └─ 包含：版本信息、测试结果、覆盖率等                                       │
│                                                                             │
│  第1.5步：提前2天通过PR提交测试报告                                          │
│  ├─ 在QA-SIG会议评审前2天通过PR提交测试报告至 community/QA/test-report/      │
│  ├─ Maintainer和Committer进行检视，在PR提交检视意见                          │
│  └─ QA-SIG会议前完成检视问题闭环                                             │
│                                                                             │
│  第2步：QA-SIG评审 ⏰ 双周二 10:30-12:00                                     │
│  ├─ 在QA纪要申报议题                                                         │
│  ├─ 陈述测试报告和质量出口标准                                               │
│  ├─ QA评审通过后记录纪要                                                     │
│  ↓（同一天申报PMC议题）                                                       │
│                                                                             │
│  第3步：PMC开源评审 ⏰ 双周三 14:00-16:00（同一周）                           │
│  ├─ 在PMC纪要申报议题                                                        │
│  ├─ 附上QA评审纪要                                                           │
│  ├─ PMC评审通过后安排开源                                                   │
│                                                                             │
│  第4步：基础设施审视仓的配置                                                  │
│  ├─ 基础设施团队审视仓库配置是否符合规范                                       │
│  ├─ 配置门禁、每日构建等CI流水线                                              │
│  └─ 审视通过后正式开源                                                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 关键时间节点

| 阶段 | 时间安排 | 操作 | 等待时间 |
|-----|---------|------|---------|
| 数字化平台发起申请 | T-1周 | 仓库责任人在 [CANN数字化平台](https://digital.hicann.cn/#/repo_manage/open_source_repo_application) 提交开源申请（电子流第1阶段自查表单） | 当天 |
| 准备测试报告 | T-1周 | 完成测试并填写报告 | 约1周 |
| 提交测试报告PR | QA-SIG会议前2天 | 通过PR提交至 QA/test-report/，Maintainer/Committer 检视 | 2天 |
| QA-SIG评审 | T+0（双周二） | 质量出口评审 | 当天 |
| PMC评审 | T+0（双周三） | 开源审批 | 当天 |
| 基础设施审视 | T+0~T+1周 | 审视仓配置、配置CI | 1-3天异步处理 |
| 正式开源 | T+1周 | 开源宣传 | 当天 |

**总耗时：约1-2周**（QA和PMC评审在同一周）

> **注意**：测试报告须在 QA-SIG 会议前 2 天通过 PR 提交，由 Maintainer/Committer 完成检视，会议前完成检视问题闭环。详见[测试报告归档说明](../../QA/test-report/README.md)。

---

## 四、具体操作步骤

### 4.1 申报TSC议题（新建仓）

1. 打开 [TSC会议纪要](https://etherpad-cann.meeting.osinfra.cn/p/TSC)
2. 在最近未召开会议区域填写：
   ```
   1. XXX仓库新建申请 -- 申请人：张三
   ```
3. 准备好PPT材料，会议时陈述

### 4.2 提交基础设施Issue与数字化平台申请建仓

1. 打开 [基础设施Issue](https://gitcode.com/cann/infrastructure/issues)
2. 选择「新建仓申请」模板
3. 填写信息：
   - 仓库名称
   - 所属SIG
   - TSC评审纪要链接
   - Maintainer/Committer名单
4. 提交Issue
5. 同时登录 [CANN数字化平台](https://digital.hicann.cn/#/repo_manage/all_repo) 提交建仓申请
6. 基础设施团队同步审批并执行仓库创建

### 4.3 提交CI配置Issue

1. 在 [基础设施Issue](https://gitcode.com/cann/infrastructure/issues) 提交
2. 选择「门禁/版本集成申请反馈」模板
3. 填写信息：
   - 代码编译命令：`bash build.sh --pkg`
   - UT运行命令：`bash build.sh -u --ophost`
   - 门禁触发命令：`/compile`（默认）
   - 特殊依赖说明
4. 基础设施团队将在仓库 `.gitcode/workflows/` 目录下配置 GitCode Action 工作流（门禁编译、UT、安全扫描等），可参考 [runtime](https://gitcode.com/cann/runtime/tree/master/.gitcode/workflows) 仓的配置

### 4.4 配置权限（修改community）

#### 步骤1：修改org-info.yaml

> 详细配置说明请参阅：[org-info.yaml文件指导说明](../../CANN/org-info-guidance.md)

#### 步骤2：创建sig-info.yaml

> 详细配置说明请参阅：[sig-info.yaml文件指导说明](../../CANN/sig-info-guidance.md)

#### 步骤3：提交PR

1. Fork [cann/community](https://gitcode.com/cann/community)
2. 提交修改
3. 等待评审：
   - `cann-cla/yes`：自动检查CLA签署（提交邮箱需要签署CLA）
   - `/lgtm`：由tsc_member评论
   - `/approve`：由tsc_member评论

### 4.5 同步创建SIG和仓库（如需要）

> 如果新仓库不属于现有SIG，可同时申请创建新SIG，在同一次TSC会议评审。

#### 判断是否需要创建SIG

- **不需要**：新仓库归属于现有SIG（如ops-math、ops-nn、runtime等），按正常建仓流程操作
- **需要**：新仓库属于新的技术领域，需要成立独立SIG管理，可同步创建SIG和仓库

#### 同步创建流程

**步骤1：准备材料+申报议题（会议前任意时间）**

1. 准备两份PPT材料，可合一：
    - SIG申请：使用 [SIG组申报模板](https://gitcode.com/cann/community/blob/master/templates/SIG%E7%BB%84%E7%94%B3%E6%8A%A5%E6%A8%A1%E6%9D%BF%20v0.2.pptx)
    - 建仓申请：使用 [新建仓申报模板](https://gitcode.com/cann/community/blob/master/templates/新建仓申报模板%20v0.2.pptx)
2. 在TSC纪要申报议题：
    ```
    XXX SIG新建申请及仓库新建 -- 申请人：张三
    ```

**步骤2：TSC评审（同一次会议）**

- 同时陈述SIG申请和建仓申请
- TSC委员投票通过后记录评审纪要

**步骤3：提交建仓申请（评审后立即提交）**

- 向infrastructure提交建仓Issue（附上TSC评审纪要）
- 同时登录 [CANN数字化平台](https://digital.hicann.cn/#/repo_manage/all_repo) 提交建仓申请
- 基础设施团队同步审批并执行仓库创建
- 同时提交CI配置Issue

**步骤4：创建SIG配置（按顺序提交PR）**

**PR1：修改org-info.yaml**（添加SIG定义和仓库）

> 详细配置说明请参阅：[org-info.yaml文件指导说明](../../CANN/org-info-guidance.md)

提交PR1，等待tsc_member评审合入（`/lgtm` + `/approve`）

**PR2：创建SIG目录和文件**（PR1合入后）

1. 在 `CANN/sigs/` 目录下创建新SIG目录：`your-new-sig/`
2. 创建 `sig-info.yaml` 文件，详细配置说明请参阅：[sig-info.yaml文件指导说明](../../CANN/sig-info-guidance.md)
3. 创建 `README.md` 文件（包含SIG介绍、会议时间、成员信息等）
4. 提交PR2，等待tsc_member评审合入

**步骤5：申请邮件列表（可选）**

PR2合入后，如需新建邮件列表：
- 参阅 [基础设施支撑矩阵](https://gitcode.com/cann/infrastructure/blob/master/docs/services.md) 获取邮件列表联系人
- [邮件列表使用指南](https://gitcode.com/cann/infrastructure/blob/master/docs/mail-list/邮件列表使用指南.md)

**步骤6：绑定账号获取会议权限**

PR合入后：
- 登录 [社区会议平台](https://meeting.osinfra.cn/cann) 个人中心
- 绑定GitCode账号与华为账号
- SIG maintainer/committer自动获得创建会议权限
- 注意：权限每隔1小时刷新一次

#### 时间对比

| 情况 | 总耗时 | 说明 |
|-----|--------|------|
| 仅新建仓 | 约2-3周 | 归属现有SIG |
| 同步创建SIG和仓库 | 约3-4周 | 同一次TSC会议评审，多一次PR评审周期 |

### 4.6 通过数字化平台提交开源申请

1. **仓库责任人**登录 [CANN数字化平台](https://digital.hicann.cn/#/repo_manage/open_source_repo_application)，进入开源申请页
2. 填写自查表单（电子流第 1 阶段：开源条件自查与测试报告，不满足无法提交）：
   - TSC 评审时间与评审截图
   - 测试报告 PR 链接（会前 2 天提交至 community/QA/test-report/，见 4.7）
   - 自查清单：按[仓库开源条件与目录结构指引](open-source-checklist.md)对应仓库类型的完整集勾选，并自查是否包含三方依赖、可执行逻辑
3. 提交后进入 QA-SIG 预审，各阶段操作详见[数字化平台建仓与开源电子流指引](digital-platform-repo-workflow.md)

### 4.7 申报QA-SIG议题（开源评审）

1. 打开 [QA会议纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-qa)
2. 填写议题：
   ```
   1. XXX仓库开源评审 -- 申请人：张三
   
   测试报告链接：XXX
   开源版本：v1.0.0
   ```
3. 会议前2天通过PR提交测试报告至 `QA/test-report/`（见[测试报告归档说明](../../QA/test-report/README.md)）
4. 会议前完成 Maintainer/Committer 检视问题闭环
5. 会议时陈述测试报告，评审会对照[仓库开源条件与目录结构指引](open-source-checklist.md)审视

### 4.8 申报PMC议题（开源审批）

1. 打开 [PMC会议纪要](https://etherpad-cann.meeting.osinfra.cn/p/PMC)
2. 填写议题：
   ```
   1. XXX仓库开源审批 -- 申请人：张三
   
   QA评审纪要：XXX
   开源计划：XXX
   ```
3. 会议时陈述开源方案

---

## 五、最佳实践时间规划

### 新建仓推荐时间线

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  说明：T+0为TSC会议当周（月末周六），整个流程约2-3周                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  时间点  关键事件                  具体操作                                  │
│  ─────────────────────────────────────────────────────────────────────      │
│  会议前  准备+申报                   填写新建仓申报PPT模板                      │
│  任意时间                            在TSC纪要填写议题                          │
│           ↓                          （无时间限制，会议前完成即可）            │
│                                                                             │
│  T+0周   ★TSC评审                   参加月末周六TSC会议                        │
│          （月末周六）               陈述建仓方案，获取评审纪要                  │
│          ↓                                                                   │
│          当天/次日                  向infrastructure提交建仓Issue + 数字化平台申请  │
│          ↓                          同时：提交CI配置Issue                      │
│          ↓                          同时：Fork [community](https://gitcode.com/cann/community)准备权限PR   │
│                                                                             │
│  T+1周   异步执行（并行）           基础设施团队创建仓库（1-3天）               │
│          ├─ CI配置                  CI门禁配置完成                             │
│          ├─ 权限配置                提交权限PR，等待评审合入                    │
│          ↓                          （约3-7天PR评审）                          │
│                                                                             │
│  T+2周   开发就绪                   PR合入，仓库正式可用                        │
│                                      开始正常开发                              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

关键里程碑：
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  准备材料     │ → │  ★TSC评审通过  │ → │  开发就绪     │
│  （任意时间） │    │  (月末周六)    │    │  (评审后2周)  │
└──────────────┘    └──────────────┘    └──────────────┘
                    ↓
              ┌──────────────┐
              │  并行执行阶段  │
              │  ├─ 仓库创建  │
              │  ├─ CI配置   │
              │  └─ 权限配置 │
              └──────────────┘
```

### 开源推荐时间线

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  说明：T+0为QA/PMC评审当周（双周二+双周三），整个流程约1-2周                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  周次    关键事件                  具体操作                                  │
│  ─────────────────────────────────────────────────────────────────────      │
│  T-1周   准备阶段                   完成测试，填写测试报告                      │
│          ↓                          仓库责任人于[CANN数字化平台](https://digital.hicann.cn/#/repo_manage/open_source_repo_application)发起开源申请 │
│          ↓                          在QA纪要申报议题                          │
│                                                                             │
│  T+0周   ★QA-SIG评审               参加双周二QA会议                           │
│          （双周二 10:30）          陈述测试报告，获取评审纪要                  │
│          ↓                          当天在PMC纪要申报议题                     │
│          ↓                                                                   │
│          ★PMC评审                   参加双周三PMC会议                          │
│          （双周三 14:00）          陈述开源方案，获取审批                      │
│          ↓                          当天/次日基础设施审视                      │
│                                                                             │
│  T+1周   正式开源                   配置完成，开源宣传材料                      │
│                                      仓库正式对外开放                          │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘

关键里程碑：
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  QA评审通过   │ → │  PMC评审通过   │ → │ 配置审视完成  │ → │  正式开源  │
│  (T+0周二)    │    │  (T+0周三)    │    │  (T+0~T+1周)  │    │  (T+1周)      │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

---

## 六、常见问题

### Q1：准备材料和申报议题的时间安排？

**说明**：
- 准备材料和申报议题可在任何时间进行，无时间限制
- 只需确保在月末周六TSC会议召开前准备好PPT和完成申报即可
- 建仓前可先在对应SIG会议讨论技术方案

### Q2：基础设施SIG会议时间冲突怎么办？

**建议**：
- Issue提交后，基础设施团队会异步处理
- 紧急需求可在Issue中标注「紧急」

### Q3：QA-SIG和PMC评审时间安排？

**说明**：
- QA-SIG评审在双周二 10:30-12:00
- PMC评审在同周双周三 14:00-16:00
- 两场评审在同一周内完成，评审周期约1周
- 可提前与QA-SIG沟通预审

### Q4：需要引入开源三方件怎么办？

**建议**：
- 先在 [CANN 社区开源三方件仓](https://www.gitcode.com/cann-src-third-party) 查询是否已引入
- 按[开源软件引入申请模板](../../templates/开源软件引入申请模板.pptx)开展选型评估
- 在**引入该软件的目标仓库对应的 SIG 组例会**上进行评审
- 通过后在 [CANN数字化协作平台](https://digital.hicann.cn/#/tripartite_parts_manage) 填写申请，[安全SIG](../../CANN/sigs/security/README.md) 成员审批引入
- 建仓及分支命名遵循[三方件建仓及分支命名指导](../third_party/third-party-repo-branch-guide.md)
- 详细流程请参阅[开源三方件维护指南](../third_party/third_party_maintenance.md)

---

## 七、关键链接汇总

### 会议平台
- [会议日历](https://meeting.osinfra.cn/cann) - 查看所有会议安排
- [TSC纪要](https://etherpad-cann.meeting.osinfra.cn/p/TSC) - 申报TSC议题
- [PMC纪要](https://etherpad-cann.meeting.osinfra.cn/p/PMC) - 申报PMC议题
- [QA纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-qa) - 申报QA议题
- [Infra纪要](https://etherpad-cann.meeting.osinfra.cn/p/sig-infrastructure) - 申报基础设施议题

### Issue提交
- [基础设施Issue](https://gitcode.com/cann/infrastructure/issues) - 建仓/CI配置申请

### 模板下载
- [新建仓申报模板](https://gitcode.com/cann/community/blob/master/templates/新建仓申报模板%20v0.2.pptx)
- [测试报告模板](https://gitcode.com/cann/community/blob/master/contributor/testing/test-templates/测试报告模板.md)
- [会议PPT模板](https://gitcode.com/cann/community/blob/master/templates/ppt_template.pptx)

### 指导文档
- [org-info.yaml文件指导说明](../../CANN/org-info-guidance.md)
- [sig-info.yaml文件指导说明](../../CANN/sig-info-guidance.md)
- [CI集成指南](ci-guide.md)
- [仓库开源条件与目录结构指引](open-source-checklist.md)
- [开源三方件维护指南](../third_party/third_party_maintenance.md)
- [三方件建仓及分支命名指导](../third_party/third-party-repo-branch-guide.md)
- [测试报告归档说明](../../QA/test-report/README.md)
- [文档写作规范](../docs/document_writing_specs.md)
- [会议指南](https://gitcode.com/cann/infrastructure/blob/master/docs/meeting/CANN社区会议指南.md)
- [邮件列表指南](https://gitcode.com/cann/infrastructure/blob/master/docs/mail-list/邮件列表使用指南.md)

### 邮件订阅
- [TSC邮件列表](https://mailweb.cann.osinfra.cn/mailman3/lists/tsc.cann.osinfra.cn/)
- [PMC邮件列表](https://mailweb.cann.osinfra.cn/mailman3/lists/pmc.cann.osinfra.cn/)
- [Infrastructure邮件列表](https://mailweb.cann.osinfra.cn/mailman3/lists/infrastructure.cann.osinfra.cn/)

---

**文档版本**: v1.2  
**创建时间**: 2026-04-18  
**更新时间**: 2026-10-31  
**更新内容**: v1.2 新增数字化平台建仓/开源电子流入口说明，明确**流程阶段定义以电子流为准**（详见 digital-platform-repo-workflow.md），开源流程按平台表单含 TSC 评审环节；v1.1 修正三方件引入流程（SIG例会评审+CANN数字化协作平台）、补充QA-SIG测试报告提前2天PR提交要求、补充缺失指导文档链接  
**来源**: CANN community仓库 + 会议平台信息
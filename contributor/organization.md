# CANN社区组织管理 

## 一、创建SIG组
新建SIG需要向技术指导委员会提交新建SIG申请，议题经技术指导委员会审批通过后，SIG发起人需要完成SIG各类权限配置。

### 如何向技术委员会提交新建SIG申请
#### 确认SIG符合申请条件
申请之前请确保该SIG符合[SIG治理章程](https://gitcode.com/cann/community/blob/master/governance/sig-governance.md)。
#### 提交申请
向技术委员会（TSC）提交新建SIG申请，需要在技术委员会（TSC）例会申报议题，申报议题方式有两种：
1. 订阅[技术委员会邮箱](https://mailweb.cann.osinfra.cn/mailman3/lists/tsc.cann.osinfra.cn/)，收到例会通知后，直接回复会议邮件，申报会议议题（例：`1. XXX SIG新建申请 -- 申请人：XXX`）。
2. 直接在技术委员会（TSC）[会议纪要模板](https://etherpad-cann.meeting.osinfra.cn/p/TSC)进行申报，将相关议题和申报人员信息等刷新到对应例会议题中（例：`1. XXX SIG新建申请 -- 申请人：XXX`）。
> 申请模板详见[SIG组申报模板](https://gitcode.com/cann/community/blob/master/templates/SIG%E7%BB%84%E7%94%B3%E6%8A%A5%E6%A8%A1%E6%9D%BF%20v0.2.pptx)。
### 权限配置

权限配置分为两种情况，请按需对号入座；两种情况均**只需提交一个 PR**，包含该情况所需的全部文件变更。

#### 概述：组织级授权与 SIG 自治

CANN 社区的权限治理分两个层级，两种情况对应不同的评审责任人与流程：

- **组织级授权（tsc_members 评审）**：涉及社区组织结构变化的事项——新建 SIG 组、org-info.yaml 组织架构变更。此类变更影响社区治理结构，且新 SIG 的 maintainer 在合入前尚未生效，因此由 `org-info.yaml` 中的 tsc_members 统一评审与批准。
- **SIG 自治（该 SIG maintainers 评审）**：SIG 已成立后，其权责范围内的事项——纳管新仓库、成员任免、路径级权限调整。此类变更属 SIG 自治范围，由该 SIG 的 maintainers 自行评审与批准；涉及跨 SIG 争议时，提请 tsc_members 仲裁。

两种情况均只需提交一个 PR；区别仅在准备的材料与评审责任人。

#### 情况一：新建 SIG 组（组织级授权）

准备一个 PR，同时包含以下三处变更：

| # | 变更 | 文件 | 参考 |
|---|------|------|------|
| 1 | 新增 SIG 组定义（含 tsc_members 可见的组信息） | `CANN/org-info.yaml` | [org-info.yaml 编写指南](https://gitcode.com/cann/community/blob/master/CANN/org-info-guidance.md) |
| 2 | 创建 SIG 目录与权限配置（maintainers/committers） | `CANN/sigs/<sig名>/sig-info.yaml` | [sig-info.yaml 编写指南](https://gitcode.com/cann/community/blob/master/CANN/sig-info-guidance.md) |
| 3 | 创建 SIG 介绍并在总索引登记 | `CANN/sigs/<sig名>/README.md` + `CANN/sigs/README.md` | 参考 [ops-basic SIG](https://gitcode.com/cann/community/blob/master/CANN/sigs/ops-basic/README.md) |

提交与合入：

- 将上述全部变更提交**单个 PR** 至 master 分支，PR 描述附评审纪要（TSC 议题申报与评审结论）。
- PR 需获得 `cann-cla/yes`、`lgtm`、`approved` 三个标签后自动合入：
  - `cann-cla/yes`：机器人自动检查 commits 邮箱的 CLA 签署状态；
  - `lgtm` / `approved`：由 `org-info.yaml` 中的 **tsc_members** 评论 `/lgtm` 与 `/approve`（新建 SIG 时该 SIG 的 maintainer 尚未生效，评审人均为 tsc_members）。
- 合入后：
  - 登录[社区会议平台](https://meeting.osinfra.cn/cann)个人中心绑定 GitCode 账号与华为账号，maintainer/committer 自动获得创建会议权限（详见[会议指南](https://gitcode.com/cann/infrastructure/blob/master/docs/meeting/CANN%E7%A4%BE%E5%8C%BA%E4%BC%9A%E8%AE%AE%E6%8C%87%E5%8D%97.md)）。<font color="red">权限每隔 1 小时刷新一次，配置后请耐心等待</font>；
  - 如需新建邮件列表，由 maintainer 在该 PR 中 @weixin_43493709 并注明"需要新建邮件列表，邮件列表名为 xxx@cann.osinfra.cn"。

#### 情况二：已有 SIG 新增纳管仓库（SIG 自治）

SIG 已存在、需将新仓库纳入管理（或调整仓库/路径级权限）时，准备一个 PR，包含以下变更：

| # | 变更 | 文件 |
|---|------|------|
| 1 | 在该 SIG 的 `repositories` 下新增仓库条目（及必要的 committer/entry_configs 权限） | `CANN/sigs/<sig名>/sig-info.yaml` |
| 2 | 如新仓库与 SIG 职责范围相关，同步更新该 SIG 的 README 仓库清单 | `CANN/sigs/<sig名>/README.md` |

提交与合入：

- 提交**单个 PR** 至 master 分支，PR 描述说明纳管理由（如该仓与 SIG 职责的关系）。
- PR 需获得 `cann-cla/yes`、`lgtm`、`approved` 三个标签后自动合入：
  - `cann-cla/yes`：机器人自动检查；
  - `lgtm` / `approved`：由**该 SIG 的 maintainers** 评论 `/lgtm` 与 `/approve`（SIG 已具备维护者，权限属 SIG 自治范围；涉及跨 SIG 争议时由 tsc_members 仲裁）。
- 新仓库本体如需门禁/版本构建等 CI 能力，请在 [infrastructure 仓提交集成申请](https://gitcode.com/cann/infrastructure/issues)（模板：门禁/版本集成申请反馈）。

> 两种情况的评审人区别一句话：**新建 SIG 找 tsc_members（组织级授权），SIG 内纳管仓库找该 SIG maintainers（SIG 自治）**。

## 二、SIG组变更(任免 maintainer committer)
### 变更流程
任免 maintainer committer流程详见[SIG治理章程](https://gitcode.com/cann/community/blob/master/governance/sig-governance.md)。

### 权限配置

#### 情况一：maintainer任免

1.  Fork 并修改：Fork `CANN/community` 仓库到您的个人账号，修改 `org-info.yaml` （[org-info.yaml编写指南](https://gitcode.com/cann/community/blob/master/CANN/org-info-guidance.md)）和SIGREADME.md里面人员信息。
2.  提交 PR：向 `CANN/community` 仓库的 `master` 分支提交 PR
3.  ✅  通过审查并合入pr：您的 PR 需要获得以下三个标签才能被合并：

    - `cann-cla/yes`：**CLA协议检查**。机器人会自动检查您 commits 中的邮箱是否已签署 CLA 协议。若已签署，将添加此标签；若未签署，会添加 `cann-cla/no` 标签并留言提示
    - `lgtm`：请联系 `org-info.yaml` 文件中列出的 **tsc_members** 进行评审。评审通过后，由tsc_member 评论 `/lgtm`，机器人会自动添加标签
    - `approved`：同样联系 **tsc_members** 进行批准。批准后，由tsc_member 评论 `/approve`，机器人会自动添加标签

#### 情况二：committer任免
1.  Fork 并修改：Fork `CANN/community` 仓库，修改目标 SIG 的 `sig-info.yaml` 文件([sig-info.yaml编写指南](https://gitcode.com/cann/community/blob/master/CANN/sig-info-guidance.md))和SIG README.md里面人员信息。
2.  提交 PR：向 `CANN/community` 仓库的 `master` 分支提交 PR
3.  ✅  通过审查并合入pr：您的 PR 需要获得以下三个标签才能被合并：
    - `cann-cla/yes`：**CLA协议检查**。机器人会自动检查您 commits 中的邮箱是否已签署 CLA 协议。若已签署，将添加此标签；若未签署，会添加 `cann-cla/no` 标签并留言提示
    - `lgtm`：请联系 `org-info.yaml` 中该 SIG 组的 **maintainers** 进行评审。评审通过后，由 maintainer 评论 `/lgtm`
    - `approved`：同样联系该 SIG 组的 **maintainers** 进行批准。批准后，由 maintainer 评论 `/approve`


## 三、SIG组终止
### 变更流程
终止SIG流程详见[SIG治理章程](https://gitcode.com/cann/community/blob/master/governance/sig-governance.md)。

### 权限配置

#### 第一步：移除SIG目录

（1）Fork 并修改：Fork CANN/community 仓库，在相应项目的 sigs 目录下删除对应SIG组目录；

（2）提交 PR：提交 PR 至 master 分支（pr描述中需要附加评审纪要）；

（3）✅通过审查并合入pr：此 PR 需获得 cann-cla/yes, lgtm, approved 三个标签后自动合入：
- cann-cla/yes：CLA协议检查。机器人会自动检查您commits中的邮箱是否已签署CLA协议。若已签署，将添加此标签；若未签署，会添加cann-cla/no标签并留言提示;
- lgtm：请联系org-info.yaml中该SIG组的maintainers进行评审。评审通过后，由 maintainer评论/lgtm;
- approved：联系该SIG组的maintainers进行批准。批准后，由maintainer评论 /approve。

（4）PR合入后，SIG组成员在SIG组对应的会议预定权限、代码合入权限等会被取消。

#### 第二步：修改组织架构

（1）Fork 并修改：Fork CANN/community 仓库，修改 org-info.yaml（[org-info.yaml编写指南](https://gitcode.com/cann/community/blob/master/CANN/org-info-guidance.md)），删除该 SIG 组的定义。

（2）提交 PR：提交 PR 至 master 分支（pr描述中需要附加评审纪要）；

（3）✅通过审查并合入pr：此 PR 需获得 cann-cla/yes, lgtm, approved 三个标签，需由tsc_members评论 /lgtm和/approve后自动合入。
- cann-cla/yes：CLA协议检查。机器人会自动检查您commits中的邮箱是否已签署CLA协议。若已签署，将添加此标签；若未签署，会添加cann-cla/no标签并留言提示;
- lgtm：请联系org-info.yaml中tsc_members进行评审。评审通过后，由 maintainer评论/lgtm;
- approved：联系tsc_members进行批准。批准后，由tsc_members评论 /approve。

## 四、PMC成员变更
### 变更流程
PMC变更流程详见[PMC治理章程](https://gitcode.com/cann/community/blob/master/governance/pmc-governance.md)。

### 权限配置
1.  Fork 并修改：Fork `CANN/community` 仓库到您的个人账号，修改 `CANN/PMC/pmc.yaml` 。
2.  提交 PR：向 `CANN/community` 仓库的 `master` 分支提交 PR
3.  ✅  通过审查并合入pr：您的 PR 需要获得以下三个标签才能被合并：

    - `cann-cla/yes`：**CLA协议检查**。机器人会自动检查您 commits 中的邮箱是否已签署 CLA 协议。若已签署，将添加此标签；若未签署，会添加 `cann-cla/no` 标签并留言提示
    - `lgtm`：请联系 `CANN/PMC/pmc.yaml` 文件中列出的 **pmc_members** 进行评审。评审通过后，pmc_member 评论 `/lgtm`，机器人会自动添加标签
    - `approved`：同样联系 **pmc_members** 进行批准。批准后，由pmc_members评论 `/approve`，机器人会自动添加标签



## 五、TSC成员变更
### 变更流程
TSC变更流程详见[TSC治理章程](https://gitcode.com/cann/community/blob/master/governance/tsc-governance.md)。

### 权限配置
1.  Fork 并修改：Fork `CANN/community` 仓库到您的个人账号，修改 `CANN/TSC/tsc.yaml`（[tsc.yaml编写指南](../CANN/tsc-guidance.md)）。
2.  提交 PR：向 `CANN/community` 仓库的 `master` 分支提交 PR
3.  ✅  通过审查并合入pr：您的 PR 需要获得以下三个标签才能被合并：

    - `cann-cla/yes`：**CLA协议检查**。机器人会自动检查您 commits 中的邮箱是否已签署 CLA 协议。若已签署，将添加此标签；若未签署，会添加 `cann-cla/no` 标签并留言提示
    - `lgtm`：请联系 `CANN/TSC/tsc.yaml` 文件中列出的 **tsc_members** 进行评审。评审通过后，tsc_member 评论 `/lgtm`，机器人会自动添加标签
    - `approved`：同样联系 **tsc_members** 进行批准。批准后，由tsc_members评论 `/approve`，机器人会自动添加标签
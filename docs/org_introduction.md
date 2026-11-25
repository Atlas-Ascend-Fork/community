## 🔥昇腾 950 NPU 架构白皮书🔥
- 🔥[文档下载](https://public-download.obs.cn-east-2.myhuaweicloud.com/ascend/%E6%98%87%E8%85%BE950%20NPU%E6%9E%B6%E6%9E%84%E7%99%BD%E7%9A%AE%E4%B9%A6.pdf) 


## 开源项目

<table style="width:100%">
  <tr>
    <th style="width:10%;text-align: center;"><span style="font-size:17px; ">组件</span></th>
    <th style="width:65%;text-align: center;"><span style="font-size:17px;">描述</span></th>
	  <th style="width:25%;text-align: center;"><span style="font-size:17px;">源码仓</span></th>
  </tr>
    <tr>
    <td style="text-align:center"><span style="font-size:16px;">算子库</span></td>
    <td><span style="font-size:16px;">提供了丰富的深度优化、硬件亲和的高性能算子，为神经网络在昇腾硬件上加速计算提供基础。</span></td>
	<td>
      <a href="https://gitcode.com/cann/ops-nn"><span style="font-size:16px;">ops-nn</span></a><br>
      <a href="https://gitcode.com/cann/ops-math"><span style="font-size:16px;">ops-math</span></a><br>
      <a href="https://gitcode.com/cann/ops-transformer"><span style="font-size:16px;">ops-transformer</span></a><br>
      <a href="https://gitcode.com/cann/ops-cv"><span style="font-size:16px;">ops-cv</span></a><br>
      </td>
  </tr>
  <tr>
    <td style="text-align:center"><span style="font-size:16px;">通信库</span></td>
    <td><span style="font-size:16px;">基于昇腾硬件的高性能通信库，提供单机多卡及多机多卡间的数据并行、模型并行通信方案。</span></td>
	<td><a href="https://gitcode.com/cann/hixl"><span style="font-size:16px;">hixl</span></a><br>
      <a href="https://gitcode.com/cann/shmem"><span style="font-size:16px;">shmem</span></a><br>
      <a href="https://gitcode.com/cann/hccl"><span style="font-size:16px;">hccl</span></a><br>
      <a href="https://gitcode.com/cann/hcomm"><span style="font-size:16px;">hcomm</span></a><br>
       </td>
  </tr>
  <tr>
    <td style="text-align:center"><span style="font-size:16px;">领域加速库</span></td>
    <td><span style="font-size:16px;">针对特定领域或场景的算子和算法的结合。</span></td>
   	<td><a href="https://gitcode.com/cann/ascend-transformer-boost"><span style="font-size:16px;">ascend-transformer-boost</span></a><br>
      <a href="https://gitcode.com/cann/sip"><span style="font-size:16px;">sip</span></a><br>
       </td>
  </tr>
  <tr>
    <td style="text-align:center"><span style="font-size:16px;">图引擎</span></td>
    <td><span style="font-size:16px;">面向昇腾的图编译器和执行器，提供图优化、多流并行、内存复用和模型下沉等功能。</span></td>
   	<td><a href="https://gitcode.com/cann/ge"><span style="font-size:16px;">ge</span></a><br>
      <a href="https://gitcode.com/cann/metadef"><span style="font-size:16px;">metadef</span></a><br>
      <a href="https://gitcode.com/cann/graph-autofusion"><span style="font-size:16px;">graph-autofusion</span></a><br>
       <a href="https://gitcode.com/cann/triton-inference-server-ge-backend"><span style="font-size:16px;">triton-inference-server-ge-backend</span></a>
       </td>
  </tr>
  <tr>
    <td style="text-align:center"><span style="font-size:16px;">算子编程</span></td>
    <td><span style="font-size:16px;">CANN针对算子开发场景推出的编程语言，最大化匹配用户开发习惯，提供算子模板库，支持算子极简编程。</span></td>
    <td>
      <a href="https://gitcode.com/cann/asc-devkit"><span style="font-size:16px;">asc-devkit</span></a><br> 
      <a href="https://gitcode.com/cann/pyasc"><span style="font-size:16px;">pyasc</span></a><br>
       <a href="https://gitcode.com/cann/pypto"><span style="font-size:16px;">pypto</span></a><br>
      <a href="https://gitcode.com/cann/pto-isa"><span style="font-size:16px;">pto-isa</span></a><br>
      <a href="https://gitcode.com/cann/atvoss"><span style="font-size:16px;">atvoss</span></a><br>
      <a href="https://gitcode.com/cann/catlass"><span style="font-size:16px;">catlass</span></a><br>
    </td>
  </tr>
   <tr>
    <td style="text-align:center"><span style="font-size:16px;">运行时</span></td>
    <td><span style="font-size:16px;">提供了高效的硬件资源管理、媒体数据预处理、单算子加载执行、模型推理等开发接口，供开发者轻松构建高性能人工智能应用。</span></td>
	  <td><a href="https://gitcode.com/cann/runtime"><span style="font-size:16px;">runtime</span></a></td>
  </tr>
   <tr>
    <td style="text-align:center"><span style="font-size:16px;">驱动</span></td>
    <td><span style="font-size:16px;">提供了基础驱动、设备管理、资源管理及调度、通信能力等功能，使能昇腾芯片，充分发挥硬件能力，支撑CANN上层软件高效稳定运行。</span></td>
	  <td><a href="https://gitcode.com/cann/driver"><span style="font-size:16px;">driver</span></a><br> </td>
  </tr>
  <tr>
    <td style="text-align:center"><span style="font-size:16px;">工具</span></td>
    <td><span style="font-size:16px;">提供CANN平台的各种工具，如算子调试调优工具、故障定位、模型压缩等。</span></td>
	  <td><a href="https://gitcode.com/cann/asc-tools"><span style="font-size:16px;">asc-tools</span></a><br>
        <a href="https://gitcode.com/cann/oam-tools"><span style="font-size:16px;">oam-tools</span></a><br>
        <a href="https://gitcode.com/cann/amct"><span style="font-size:16px;">amct</span></a>
    </td>
  </tr>
</table>


## 关于社区
### 社区治理架构及章程

CANN 社区采用分层协作的治理模式，当前架构主要包括以下组织：

  - [技术指导委员会（TSC-Technical Steering Committee）](../CANN/TSC/README.md)
  - [项目管理委员会（PMC-Project Management Committee）](../CANN/PMC/README.md)
  - [特别兴趣小组（SIG-Special Interest Group）](https://gitcode.com/cann/community/tree/master/CANN/sigs)

更多社区治理内容，详见：[社区治理章程](../README.md#社区治理章程)

### 参与贡献
  -  [基础贡献](../README.md#基础贡献)：包含参与社区会议、社区邮件讨论、提交 Issue 、处理 Issue 任务、提交PR等。
  -  [进阶贡献](../README.md#进阶贡献)：包含新建 SIG、成为核心贡献者、组织会议、新建仓库、引入开源软件、发布新版本或新仓库等。

## 快速体验

若您希望快速体验CANN算子的调用和开发过程，请访问如下文档获取简易教程。
- [算子调用](https://gitcode.com/cann/ops-math/blob/master/docs/zh/invocation/quick_op_invocation.md)：介绍调用算子的基本步骤，快速搭建环境，实现算子编译执行。
- [算子开发](https://gitcode.com/cann/ops-math/blob/master/docs/zh/develop/aicore_develop_guide.md)：介绍开发算子的基本流程，一键创建算子工程目录，实现Tiling、Kernel核心交付件。


🔥**一站式开发平台**：您也可在对应仓库中点击“CANNLab”，在一站式在线开发环境中限时免费体验昇腾算力。🔥

## 实践样例

⚓[推理](https://gitcode.com/cann/cann-recipes-infer) &nbsp; | &nbsp;🚈 [训练](https://gitcode.com/cann/cann-recipes-train) | &nbsp; 🔮 [空间智能](https://gitcode.com/cann/cann-recipes-spatial-intelligence) | &nbsp; 🎮 [具身智能](https://gitcode.com/cann/cann-recipes-embodied-intelligence) | &nbsp; 📱 [鸿蒙推理](https://gitcode.com/cann/cann-recipes-harmony-infer)

|热门实践  |描述  |
|--|--|
|[NPU DeepSeek-V4推理优化实践](https://gitcode.com/cann/cann-recipes-infer/blob/master/docs/models/deepseek_v4/deepseek_v4_inference_guide.md)  | DeepSeek团队发布了最新的模型DeepSeek-V4系列模型，包含DeepSeek-V4 Flash和DeepSeek-V4 Pro两种规格。在DeepSeek-V3.2的稀疏Attention（DeepSeek Sparse Attention）的基础上，在不同层间进一步通过KV Cache滑窗 (Window Cache) 和压缩算法 (KV Cache Compress)，减少Attention的计算和访存开销，可以大幅提升长序列的计算效率，降低推理的成本。本实践0 Day支持了DeepSeek-V4的模型推理部署，并适配支持Atlas-A3和950PR/DT多代际昇腾芯片。 |
|[DeepSeek-V4昇腾训练支持](https://gitcode.com/cann/cann-recipes-train/blob/master/docs/llm_pretrain/deepseek-v4_torchtitan_npu_autofuse.md)  | 本文介绍 DeepSeek-V4-Flash 模型基于 CANN 平台的训练优化实践。基于 TorchTitan-NPU 框架，采用纯 FSDP + 大 EP 极简并行策略实现内存最优；创新性地使能训练入图技术，凭借 Ascend C AutoFuse 能力，获得端到端 32% 的编译收益；针对稀疏注意力结构定制高效融合算子，充分释放芯片算力。 |
|[DeepSeek-V3.2-Exp模型支持推理部署](https://gitcode.com/cann/cann-recipes-infer/blob/master/models/deepseek_v3_2_exp/README.md)  | 基于Transformers库，在Atlas A3环境中Prefill阶段采用了长序列亲和的CP并行策略，Decode阶段沿用大EP并行，同时整网设计新的NPU融合Kernel和多流并行优化，实现较高的吞吐推理性能。 |
|[DeepSeek-R1 RL训练优化实践](https://gitcode.com/cann/cann-recipes-train/blob/master/llm_rl/deepseek/README.md)  | 基于开源veRL框架，搭配MindSpeed+vLLM-Ascend框架，在Atlas A3集群实现GRPO算法的高吞吐RL训练，并达到120TPS/卡的系统吞吐量。 |
|[HunyuanVideo模型推理优化实践](https://gitcode.com/cann/cann-recipes-infer/blob/master/models/hunyuan-video/README.md)  | 基于xDiT框架，在Atlas A2环境中采用了Ulysses序列并行和RingAttention序列并行测量，同时适配了TeaCache加速，实现了较优的推理性能。 |
|[VGGT模型推理优化实践](https://gitcode.com/cann/cann-recipes-spatial-intelligence/blob/master/models/vggt/README.md)  | 基于VGGT开源模型，完成其在Atlas A2上的推理适配，并提供其在相机位姿估计、点云三维重建、深度估计三个任务上的精度评测脚本。 |
|[Pi0模型推理优化实践](https://gitcode.com/cann/cann-recipes-embodied-intelligence/blob/master/manipulation/pi0/infer_with_torch/README.md)  | 基于LeRobot库，在Atlas A2环境适配Pi0模型，通过使能融合算子、图模式、计算逻辑优化等手段，实现了较低的推理时延。 |
|[QQ音乐声伴分离鸿蒙推理优化实践](https://gitcode.com/cann/cann-recipes-harmony-infer/blob/master/ops/ascendc/docs/custom-npu_bandNorm.md)  | 实现QQ音乐声伴分离业务模型中的BandNorm等算子在鸿蒙设备上的高性能推理部署。 |



## 社区活动
- [社区会议日历](https://meeting.osinfra.cn/cann)：如果您对CANN社区的各类会议感兴趣，可访问会议日历。
- 🔥[CANN直播回放](../events/meetup/README.md)：汇聚CANN NEXT、DeepSeek-V4、CANN开源开放、CANN Insight、线下Meetup与CANNBot/TileLang课程等系列直播，涵盖前沿技术、开源生态与实操教程，专家干货随时回看。
- 🔥[昇腾AI算法挑战赛进阶赛](https://developer.huaweicloud.com/competition/information/1300000204)：昇腾AI算法挑战赛旨在汇聚全球各领域的优秀开发者同台竞技。开放昇腾AI计算平台的全栈能力与API资源，鼓励开发者构建高效创新的AI模型，解决实际场景问题。
-   [CANN训练营](https://www.hiascend.com/developer/activities/cann20261#cann-camp-2601-intro)：为开发者打造“学、练、赛”成长体系：报名领取免费学习资源，每周一、四[开源实践全新解读](https://www.hiascend.com/developer/activities/cann20261?tab=live)；通过[算子开发者认证考核](https://www.hiascend.com/edu/developer-certification)，参与[社区任务](https://gitcode.com/org/cann/discussions/22)赢华为三折叠等大奖。
- [昇腾AI创新大赛-算子挑战赛](https://www.hiascend.com/developer/ops)：昇腾AI创新大赛-算子挑战赛旨在培养一批精通Ascend C算子开发的开发者，鼓励开发者基于CANN的基础能力进行深度创新与实践。



## 联系我们
-   [社区邮件订阅](https://mailweb.cann.osinfra.cn/mailman3/lists)：选择需要订阅的组织（TSC/PMC/SIG等），填写相关信息，进行邮件订阅（邮件推送内容包含：会议通知、会议纪要、内容讨论等），如果您对相关组织有诉求或者问题，也可以通过邮箱途径联系。
- 昇腾CANN（社交媒体）

  |<center><a href="https://space.bilibili.com/1190614918?spm_id_from=333.337.0.0">B站</a></center> | <center>微信公众号</center> | <center><a href="https://www.zhihu.com/people/ha-ha-ha-ha-51-33-24">知乎</a></center> |<center><a href="https://blog.csdn.net/m0_71340392">CSDN</a></center>|
  |--|--|--|--|
  | <img src="images/bilibili.png" width="130" height="130" alt="cann_bilibili">  | <img src="images/weixin.jpg" width="130" height="130" alt="CANN微信公众号">| <img src="images/zhihu.png" width="130" height="130" alt="昇腾CANN知乎"> | <img src="images/CSDN.png" width="130" height="130" alt="昇腾CANN_CSDN"> |

- [cann@cann.team](mailto:cann@cann.team)



## 相关链接
- [昇腾社区](https://www.hiascend.com/cann)
- [鸿蒙社区](https://developer.huawei.com/consumer/cn/sdk/cann-kit/)



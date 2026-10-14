# 研究入门指南

**具身智能 · 视频生成与世界模型 · 智能 CAD/CAM**

这份书单供新加入项目的本科生和跨方向同学使用。每个小方向列出 5 篇核心论文，★ 标注重点研读的工作，补充阅读按课题需要选择。

## 阅读建议

先选一个小方向，补齐必要基础，按表中顺序阅读。前两篇用于熟悉问题和方法，后三篇用于比较不同解法，随后选一个基线动手实践。

读论文时，先看问题、方法图和实验，再看推导与代码。记录输入输出、数据来源、训练方式和适用条件；比较方法时，注意核心机制的差异。

补充阅读可先选 1—2 篇，各篇附有推荐理由、对照方法和适用条件。年份通常按首次公开稿标注，奖项与后续采用附有来源。

<a id="navigation"></a>
## 方向导航

| 研究方向 | 学习分支 | 核心论文 | 专题补充 |
| --- | --- | :---: | :---: |
| [具身智能](#embodied) | 环境构建、操作策略迁移、少示范学习、示范迁移、RL、任务规划、技能记忆 | 35 | 22 |
| [视频生成与世界模型](#worlds) | 可控叙事、状态预测、长期记忆、生成训练、规划决策 | 25 | 9 |
| [智能 CAD/CAM](#cad) | 可编辑 CAD、工程图与逆向建模、制造与刀路 | 15 | 6 |

| 编号 | 小方向 |
| :---: | --- |
| A1 | [Real2Sim：环境重建、物理校准与示范扩增](#a1) |
| A2 | [Sim2Real for Manipulation：视觉操作与灵巧控制](#a2) |
| A3 | [单示范与少示范技能学习](#a3) |
| A4 | [示范到执行：功能对应、双臂协调与跨本体迁移](#a4) |
| A5 | [RL for Manipulation：策略优化、真实反馈与奖励设计](#a5) |
| A6 | [Agentic：任务规划与闭环执行](#a6) |
| A7 | [Agentic：技能记忆与持续适应](#a7) |
| B1 | [可控视频与多镜头叙事](#b1) |
| B2 | [交互世界模型：状态表示与未来预测](#b2) |
| B3 | [长期记忆、实体关系与共享状态](#b3) |
| B4 | [视频训练：生成基础、时序建模与反馈优化](#b4) |
| B5 | [世界模型用于机器人规划与决策](#b5) |
| C1 | [可编辑 CAD：表示、生成与迭代优化](#c1) |
| C2 | [工程图与三维观测：信息提取和逆向建模](#c2) |
| C3 | [CAM：制造特征、工艺优化与刀路](#c3) |

---

<a id="embodied"></a>
## 1. 具身智能

本方向聚焦 **manipulation（机器人操作）**：机械臂抓取与放置、双臂协同、接触装配、灵巧手操作，以及以物体交互为目标的移动操作。

暂不涉及纯 locomotion（行走、跑跳、地形适应）。移动操作论文侧重感知、接触交互和操作策略。

**基础知识：** Python、深度学习、坐标变换、机器人观测与动作。策略学习分支补充行为克隆和强化学习。

**方向衔接：** 环境与迁移：[A1](#a1) → [A2](#a2)。技能学习：[A3](#a3) → [A4](#a4)／[A5](#a5)。自主执行：[A6](#a6) → [A7](#a7)。

<a id="a1"></a>
### A1. Real2Sim：环境重建、物理校准与示范扩增

**研究问题：** 怎样把真实环境与少量示范转为可交互场景和可用于学习的数据？

**先修知识：** 相机位姿、三维重建、碰撞几何、物理参数、机器人轨迹。

**阅读顺序：** 可交互重建 → 物理辨识 → 场景编辑 → 几何约束迁移 → 全身轨迹扩增

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | **[RialTo](https://arxiv.org/abs/2403.03949)**<br>Reconciling Reality through Simulation: A Real-to-Sim-to-Real Approach for Robust Manipulation | 可交互数字孪生与仿真内策略强化 | 从扫描场景建立数字孪生，在仿真中改进策略后部署到真机。阅读时梳理场景重建、物理建模和策略训练之间的数据与接口。 |
| 2 | ★ **[D-REX](https://arxiv.org/abs/2603.01151)**<br>D-REX: Differentiable Real-to-Sim-to-Real Engine for Learning Dexterous Grasping | 真实交互驱动的可微物理辨识 | 利用真实交互辨识物体质量等参数，再用于抓取策略训练。关注参数估计的依据、接触误差及其对抓取结果的影响。 |
| 3 | ★ **[RoboSplat](https://arxiv.org/abs/2504.13175)**<br>Novel Demonstration Generation with Gaussian Splatting Enables Robust One-Shot Manipulation | 直接编辑三维高斯的观测扩增 | 通过物体替换、位姿变换和新视角渲染扩增示范。关注图像与动作的同步变换，以及不依赖完整物理仿真的数据生成方式。 |
| 4 | ★ **[CP-Gen](https://arxiv.org/abs/2508.03944)**<br>Constraint-Preserving Data Generation for Visuomotor Policy Learning | 保持关键点轨迹约束的几何迁移 | 用对象相对的关键点轨迹约束描述技能，再优化关节轨迹。比较物体尺寸、形状和位姿改变后，哪些任务关系需要保留。 |
| 5 | ★ **[WANDA](https://arxiv.org/abs/2607.13154)**<br>Worlds in One Demo: A Synthetic Data Engine for Learning Open-World Mobile Manipulation | 接触片段重定位与全身运动规划 | 保留并重定位接触片段，重新规划自由运动段，结合网格前景与高斯背景生成观测。关注纠错状态扩增和全身轨迹的连接。 |

RoboSplat、CP-Gen 和 WANDA 可对照阅读，分别关注观测扩增、任务约束保持，以及接触片段与全身运动的连接。

<details>
<summary>补充阅读（3 篇）</summary>

重建与渲染基础不足时先读 3DGS；研究示范扩增读 MimicGen；研究环境多样性读 ACDC。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[3D Gaussian Splatting](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/)**（2023）<br>3D Gaussian Splatting for Real-Time Radiance Field Rendering | 获 SIGGRAPH 2023 最佳论文奖（[作者记录](https://grgkopanas.github.io/)）。通过可优化的各向异性高斯、密度控制和可见性感知渲染，提高新视角合成效率，是后续高斯场景扩增方法的基础。 | 可在 RoboSplat、WANDA 前阅读表示与渲染部分。碰撞几何、质量和接触动力学需要另外建模。 |
| **[MimicGen](https://arxiv.org/abs/2310.17596)**（2023）<br>MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations | 将示范分成对象中心片段，变换到新场景后拼接、执行并筛选。[Isaac Lab Mimic](https://isaac-sim.github.io/IsaacLab/main/source/api/lab_mimic/isaaclab_mimic.datagen.html)将其列为实现灵感，可用于追溯后续数据生成方法。 | 与 CP-Gen、WANDA 比较对象相对变换、约束保持和全身重规划。复现时需准备对象位姿、子任务划分及成功判定。 |
| **[ACDC](https://digital-cousins.github.io/)**（2024）<br>Automated Creation of Digital Cousins for Robust Policy Learning | 检索并组合几何和交互功能相近的资产，生成多种“数字近亲”。相比精确重建实景，更关注功能保留和训练环境的多样性。 | 与 RialTo 的数字孪生对照，适合场景扩增课题。资产匹配后，质量、关节阻力和接触行为仍需检查。 |

</details>

<a id="a2"></a>
### A2. Sim2Real for Manipulation：视觉操作与灵巧控制

**研究问题：** 如何把仿真中学到的机械臂、双臂或灵巧手操作策略部署到真实机器人，并处理视觉、接触与执行器差异？

**先修知识：** 机器人观测与动作、SAC／PPO、教师—学生蒸馏、域随机化、相机对齐、接触动力学。

**阅读顺序：** 直接视觉强化学习 → 几何控制与策略蒸馏 → 视觉学生的闭环强化 → 跨域三维表征 → 真实动力学补偿

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | ★ **[Squint](https://arxiv.org/abs/2602.21203)**<br>Squint: Fast Visual Reinforcement Learning for Sim-to-Real Robotics | 并行仿真中的直接视觉 SAC | 在并行仿真中直接训练视觉 SAC，以 SO-101 的抓取、放置和堆叠为例，分析低分辨率输入、经验回放和回报分布建模。部署部分关注相机对齐与域随机化。[项目与代码](https://aalmuzairee.github.io/squint/) |
| 2 | ★ **[DextrAH-G](https://arxiv.org/abs/2407.02274)**<br>DextrAH-G: Pixels-to-Action Dexterous Arm-Hand Grasping with Geometric Fabrics | 几何控制结构与特权策略蒸馏 | 面向臂手协同抓取，用 geometric fabrics 处理运动约束，再将特权教师蒸馏为深度视觉学生。依次阅读动作空间、控制结构与蒸馏过程。 |
| 3 | ★ **[DoorMan](https://arxiv.org/abs/2512.01061)**<br>Opening the Sim-to-Real Door for Humanoid Pixel-to-Action Policy Transfer | 分阶段重置与视觉学生的强化微调 | 围绕把手操作和推拉门，阅读 teacher–student–bootstrap 流程、分阶段重置和基于 GRPO 的视觉学生微调。全身控制部分侧重其对开门交互的支持。[项目页](https://doorman-humanoid.github.io/) |
| 4 | **[Point Bridge](https://arxiv.org/abs/2601.16212)**<br>Point Bridge: 3D Representations for Cross Domain Policy Learning | 域无关的点式三维表征与策略学习 | 提取操作相关的点式三维表征，减少背景和外观差异对策略的影响。比较纯合成数据训练与加入少量真实示范的设置。 |
| 5 | **[DexNDM](https://arxiv.org/abs/2510.08556)**<br>DexNDM: Closing the Reality Gap for Dexterous In-Hand Rotation via Joint-Wise Neural Dynamics Model | 关节级神经动力学与部署动作补偿 | 用真实交互拟合关节级动力学，补偿仿真策略在手内旋转中的动作误差。关注跨关节因素的压缩、数据采集，以及补偿器与原策略各自的训练方式。 |

DextrAH-G 与 DoorMan 都采用教师—学生框架，前者侧重几何控制，后者侧重分阶段探索和视觉学生强化。可对照两者的动作接口与训练过程。

**基础回溯：** 不熟悉迁移机制时，再补读 [Domain Randomization](https://arxiv.org/abs/1703.06907) 的外观分布覆盖、[RCAN](https://arxiv.org/abs/1812.07252) 的图像规范化，以及 [SimOpt](https://arxiv.org/abs/1810.05687) 的真实反馈驱动参数分布校准。物理辨识与仿真构建另见 [A1 的 D-REX 与 RialTo](#a1)。

阅读时分别记录仿真训练与真机执行的输入、特权信息、动作接口、真实数据用途和失败恢复方式。“不用特权状态”“不做真机微调”和“不使用真实训练数据”是不同设置。实践可从桌面操作开始。

<details>
<summary>补充阅读（8 篇）</summary>

根据课题选择 RGB 抓取、接触装配、真实纠错、虚实同步、合成 VLA、探索恢复或力控方向。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[Solving Rubik’s Cube with a Robot Hand](https://arxiv.org/abs/1910.07113)**（2019） | 自动域随机化（ADR）的代表工作。训练环境的分布随策略能力逐步扩大，带记忆的控制策略用于适应环境变化。 | 接在 Squint 后，比较人工设定与自动扩展随机化分布。结合机器人平台、状态估计和策略训练分析完整系统。 |
| **[IndustReal](https://arxiv.org/abs/2305.17110)**（2023）<br>IndustReal: Transferring Contact-Rich Assembly Tasks from Simulation to Reality | 针对接触装配，结合仿真感知训练、SDF 奖励、采样课程和策略级动作积分，分别处理训练中的仿真误差与部署时的跟踪误差。 | 与 DexNDM 比较控制接口修正和学习式动力学补偿。迁移到柔性接触或灵巧手任务时，需要重新评估接触模型和控制设置。 |
| **[DextrAH-RGB](https://arxiv.org/abs/2412.01791)**（2024）<br>DextrAH-RGB: Visuomotor Policies to Grasp Anything with Dexterous Hands | 将臂手抓取扩展到 RGB 输入，结合逼真渲染和视觉学生蒸馏。可据此观察感知域差距对训练设计的影响。 | 与 DextrAH-G 配套阅读，比较相机输入、随机化和学生训练，并检查对教师能力及相机设置的依赖。 |
| **[TRANSIC](https://arxiv.org/abs/2405.10315)**（2024）<br>TRANSIC: Sim-to-Real Policy Transfer by Learning from Online Correction | 在仿真策略执行时收集人类在线纠正，训练补偿策略。真实环境中的失败由此成为有针对性的训练数据。 | 与 DexNDM、A5 的 Residual RL 比较动力学补偿、纠错学习和残差控制。该方法使用真实干预数据。 |
| **[Real-is-Sim](https://arxiv.org/abs/2504.03597)**（2025）<br>Real-is-Sim: Bridging the Sim-to-Real Gap with a Dynamic Digital Twin | 策略运行在持续同步的数字孪生中，实体跟踪仿真关节状态，真实观测再修正孪生。与直接迁移策略相比，它调整了部署和同步架构。 | 接在 Squint 后，比较两种部署方式。阅读 PushT 实验时，关注状态估计、同步频率和跟踪误差。 |
| **[Sim2Real-VLA](https://edem-ai.github.io/sim2realvla.github.io/)**（2025 年公开介绍）<br>Zero-Shot Generalization of Synthesized Skills to Realistic Manipulation | 高层预测 chain-of-affordances，低层通过离散化动作接口执行与验证，并使用合成数据训练。可与直接动作预测比较中间表示的作用。 | 接在 Point Bridge 后，以[作者项目](https://edem-ai.github.io/sim2realvla.github.io/)和[单位介绍](https://itso.cuhk.edu.cn/en/article/516)为入口。分别核对操作训练数据与基础模型预训练的数据来源。 |
| **[OmniReset](https://arxiv.org/abs/2603.15789)**（2026）<br>Emergent Dexterity via Diverse Resets and Large-Scale Reinforcement Learning | 通过多样化重置覆盖更多机器人—物体交互状态，让策略从不同接触和偏离状态开始学习。它着重研究初始状态分布对探索与恢复能力的影响。 | 接在 DoorMan 后，比较多样重置与分阶段重置的状态来源、覆盖范围和恢复效果。真机复位条件、蒸馏和部署效果需单独检查。 |
| **[Closing the Reality Gap](https://arxiv.org/abs/2601.02778)**（2026）<br>Zero-Shot Sim-to-Real Deployment for Dexterous Force-Based Grasping and Manipulation | 将触觉、关节力矩和执行器标定纳入虚实对应，研究抓握力及接触行为的控制，补充以位姿和抓取成功率为主的阅读线。 | 与 DexNDM 比较执行器误差处理，与 DextrAH-G 比较观测和动作接口。阅读电流—力矩标定及硬件建模要求。 |

</details>

<a id="a3"></a>
### A3. 单示范与少示范技能学习

**研究问题：** 只有少量人工示范，如何通过数据、检索、动作表示与交互获得可泛化的技能？

**先修知识：** 行为克隆、轨迹配准、末端动作表示、上下文条件与强化学习。

**阅读顺序：** 恢复数据学习 → 检索适配 → 低维动作优化 → 上下文模仿 → 示范引导强化

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | ★ **[MILES](https://arxiv.org/abs/2410.19693)**<br>Making Imitation Learning Easy with Self-Supervision | 自主恢复数据扩增与行为克隆 | 从一条示范附近自主采集恢复轨迹，再训练模仿策略。阅读恢复数据的采集规则，并分别统计人工示范和额外训练数据。 |
| 2 | ★ **[MT3](https://arxiv.org/abs/2511.10110)**<br>Learning a Thousand Tasks in a Day | 任务检索与轨迹适配 | 通过任务检索、场景对齐和轨迹适配执行新任务。关注轨迹复用的条件，以及新增任务时是否需要重新训练策略。 |
| 3 | ★ **[ScrewMimic](https://arxiv.org/abs/2405.03666)**<br>ScrewMimic: Bimanual Imitation from Human Videos with Screw Space Projection | 螺旋动作表示与低维在线优化 | 用少量螺旋参数描述双臂相对运动，并通过交互优化参数。比较动作降维的收益与感知、在线优化的成本。 |
| 4 | ★ **[SynthICL](https://arxiv.org/abs/2606.08154)**<br>SynthICL: Scalable In-context Imitation Learning with Synthetic Data | 合成预训练支持的上下文模仿 | 经过合成数据预训练后，将新示范作为推理条件。阅读视觉示范的编码、上下文使用方式，以及预训练数据对适应能力的影响。 |
| 5 | ★ **[ReGIL](https://arxiv.org/abs/2606.09381)**<br>ReGIL: Retrieval-Guided Imitation Learning from a Single Demonstration | 示范记忆引导的模仿与强化学习 | 利用示范检索引导探索，以局部时序对应构造奖励，并加入模仿约束。梳理检索、奖励与策略更新各自的作用。 |

SynthICL 与 [A4 的 Instant Policy](#a4) 配套阅读，再用 Behavior Prompting Policy 对照任务多样性和示范条件的设计。

<details>
<summary>补充阅读（3 篇）</summary>

Diffusion Policy 和 ACT 补充策略基础；Behavior Prompting Policy 用于上下文模仿的方法对照。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[Diffusion Policy](https://arxiv.org/abs/2303.04137)**（2023）<br>Diffusion Policy: Visuomotor Policy Learning via Action Diffusion | 用条件扩散表示多模态动作分布，结合动作序列预测与滚动执行。[UMI](https://umi-gripper.github.io/)等后续系统沿用了这一策略形式，适合作为生成式操作策略的基础阅读。 | 可在 SynthICL、Instant Policy 前阅读。关注动作表达、去噪延迟和闭环频率；示范效率另行评估。 |
| **[ACT / ALOHA](https://arxiv.org/abs/2304.13705)**（2023）<br>Learning Fine-Grained Bimanual Manipulation with Low-Cost Hardware | 一次预测动作片段，通过时间聚合缓解逐步误差积累。[Mobile ALOHA](https://arxiv.org/abs/2401.02117)继续使用 ACT，并研究静态与移动操作数据的联合训练。 | 与 Diffusion Policy 比较动作块建模、推理成本和纠错频率。作为行为克隆基线，按具体任务核对示范量。 |
| **[Behavior Prompting Policy](https://arxiv.org/abs/2606.30457)**（2026）<br>Behavior Prompting Policy: Demonstrations as Prompts for Manipulation | 研究任务多样性如何促成示范提示能力，并设计相应数据与评测。可用于分析模型何时、为何能够利用上下文示范。 | 接在 SynthICL、Instant Policy 后，比较预训练任务覆盖、示范编码和新任务划分。三者均属于上下文模仿路线。 |

</details>

<a id="a4"></a>
### A4. 示范到执行：功能对应、双臂协调与跨本体迁移

**研究问题：** 示范的物体、视角或执行者发生变化时，怎样得到机器人可执行的动作？

**先修知识：** SE(3) 位姿、视觉对应、视觉伺服、点云、序列模型与运动约束。

**阅读顺序：** 功能关键点 → 双臂视觉对齐 → 图上下文策略 → 进度条件预测 → 安全动作修正

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | ★ **[FUNCTO](https://arxiv.org/abs/2502.11744)**<br>FUNCTO: Function-Centric One-Shot Imitation Learning for Tool Manipulation | 功能关键点对应与轨迹优化 | 自动提取并匹配功能相关的三维关键点，用对应关系约束末端轨迹。关注工具形状变化后，功能关系如何帮助操作迁移。 |
| 2 | ★ **[ODIL](https://arxiv.org/abs/2503.06831)**<br>One-Shot Dual-Arm Imitation Learning | 双臂视觉伺服对齐与交互段重放 | 通过多阶段视觉对齐协调双臂，再重放交互轨迹。分别阅读对齐阶段的反馈控制与接触执行阶段的动作处理。 |
| 3 | ★ **[Instant Policy](https://arxiv.org/abs/2411.12633)**<br>Instant Policy: In-Context Imitation Learning via Graph Diffusion | 图结构上下文条件与动作扩散 | 将示范、点云和当前观测组织成图，通过扩散模型预测动作。与 SynthICL 比较输入表示、上下文编码和预训练数据。 |
| 4 | ★ **[HOST](https://arxiv.org/abs/2607.20033)**<br>Robots Acquire Manipulation Skills in Seconds from a Single Human Video | 任务进度对齐与未来观测条件动作生成 | 通过任务进度对齐，连接人类示范、机器人未来观测预测和动作生成。关注共享进度的建立方式及预训练需求。 |
| 5 | ★ **[SafeMimic](https://arxiv.org/abs/2506.15847)**<br>SafeMimic: Towards Safe and Autonomous Human-to-Robot Imitation for Mobile Manipulation | 安全价值约束与滚动动作选择 | 将第三视角人类示范转成机器人动作，通过安全评估和滚动选择修正执行。比较几何对应、模仿目标与安全约束的分工。 |

<details>
<summary>补充阅读（2 篇）</summary>

准备采集示范时读 UMI；准备跨本体数据联合训练时读 Open X-Embodiment。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[UMI](https://umi-gripper.github.io/)**（2024）<br>Universal Manipulation Interface: In-The-Wild Robot Teaching Without In-The-Wild Robots | 用手持夹爪采集数据，通过相对动作表示和时延匹配支持机器人执行。入围 [RSS 2024 Outstanding Systems Paper Award](https://roboticsconference.org/2024/program/awards/)。 | 与 HOST、SafeMimic 比较数据采集和跨本体映射。UMI 依赖专用采集器具，适合准备采集操作示范时阅读。 |
| **[Open X-Embodiment / RT-X](https://arxiv.org/abs/2310.08864)**（2023）<br>Open X-Embodiment: Robotic Learning Datasets and RT-X Models | 获 [ICRA 2024 Best Conference Paper Award](https://ewh.ieee.org/soc/ras/conf/fullysponsored/icra/icra%202024/awards-and-finalists/index.html)。汇集多机器人数据并开展联合训练，是研究跨本体数据共享的重要参照。 | 接在 Instant Policy、HOST 后，比较联合训练、上下文适应和动作重定向。关注动作空间的兼容性与未知本体上的泛化条件。 |

</details>

<a id="a5"></a>
### A5. RL for Manipulation：策略优化、真实反馈与奖励设计

**研究问题：** 如何通过试错提升抓取、装配和灵巧操作技能，并减少从零探索和真实交互的成本？

**先修知识：** 马尔可夫决策过程、策略梯度、价值函数、经验回放与动力学模型。

**阅读顺序：** 策略优化 → 残差控制 → 人类干预 → 模型内想象 → 奖励程序搜索

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | **[PPO](https://arxiv.org/abs/1707.06347)**<br>Proximal Policy Optimization Algorithms | 当前策略采样的策略梯度 | 阅读裁剪目标、优势估计、采样和更新流程，为并行仿真中的策略训练打基础。 |
| 2 | **[Residual RL](https://arxiv.org/abs/1812.03201)**<br>Residual Reinforcement Learning for Robot Control | 已有控制器与学习残差叠加 | 在已有控制器上叠加学习到的残差动作。比较残差控制与直接学习完整动作的探索难度和适用条件。 |
| 3 | **[HIL-SERL](https://arxiv.org/abs/2410.21845)**<br>Precise and Dexterous Robotic Manipulation via Human-in-the-Loop Reinforcement Learning | 人类干预的离策略强化学习 | 结合示范、在线纠正和离策略学习训练真实机器人。评估样本效率时，同时记录人工干预、环境交互和复位成本。 |
| 4 | **[DayDreamer](https://arxiv.org/abs/2206.14176)**<br>DayDreamer: World Models for Physical Robot Learning | 世界模型中的想象式策略学习 | 阅读机械臂从图像和稀疏奖励学习取放的实验，梳理真实采集、模型训练和想象中的策略更新。行走与导航实验可跳过。 |
| 5 | **[Eureka](https://arxiv.org/abs/2310.12931)**<br>Eureka: Human-Level Reward Design via Coding Large Language Models | 语言模型驱动的奖励程序搜索 | 由语言模型编写奖励，根据训练反馈继续改写。以灵巧手转笔等任务为例，分析奖励搜索与底层 RL 的配合；真机迁移另行评估。 |

<details>
<summary>补充阅读（2 篇）</summary>

稀疏目标奖励读 HER；希望减少真机人工干预时读 AutoSERL。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[Hindsight Experience Replay](https://arxiv.org/abs/1707.01495)**（2017） | 把轨迹实际达到的状态重新标为目标，使失败交互也提供学习信号。[Stable-Baselines3](https://stable-baselines3.readthedocs.io/en/master/modules/her.html)提供了相应实现，可用于稀疏奖励任务。 | 可结合抓取、推动任务阅读。与 PPO、Eureka 分别比较经验重用、策略优化和奖励设计；应用时需支持目标重标记与奖励重算。 |
| **[AutoSERL](https://arxiv.org/abs/2607.01651)**（2026）<br>One Demonstration Is Enough for Real-World Robotic Reinforcement Learning | 从一条示范建立滑动窗口引导和轨迹恢复机制，再随能力形成减少引导，降低对人工在线干预的依赖。 | 接在 HIL-SERL、ReGIL 后，比较人类纠正、示范约束和恢复流程。实验记录应包含真实交互、复位条件与安全监督。 |

</details>

<a id="a6"></a>
### A6. Agentic：任务规划与闭环执行

**研究问题：** 怎样把语言或视频中的任务目标转成可执行计划，并利用环境反馈检查结果？

**先修知识：** 语言模型工具调用、技能接口、任务状态、运动规划与三维场景表示。

**阅读顺序：** 技能可行性 → 程序化策略 → 视频任务提取 → 空间价值图 → 场景图搜索

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | **[SayCan](https://arxiv.org/abs/2204.01691)**<br>Do As I Can, Not As I Say: Grounding Language in Robotic Affordances | 语言相关性与技能可行性联合选择 | 结合语言相关性与技能可行性选择下一步。关注技能价值的估计，以及它如何限制语言模型给出的计划。 |
| 2 | **[Code as Policies](https://arxiv.org/abs/2209.07753)**<br>Code as Policies: Language Model Programs for Embodied Control | 生成可执行的工具调用程序 | 通过生成代码组合感知、几何计算与控制接口。阅读程序生成过程，同时检查系统预先提供了哪些工具能力。 |
| 3 | ★ **[SeeDo](https://arxiv.org/abs/2410.08792)**<br>VLM See, Robot Do: Human Demo Video to Robot Action Plan via Vision Language Model | 人类示范视频到符号操作计划 | 从人类视频中识别物体、动作和步骤，形成机器人操作计划。关注语义步骤到技能接口的映射，而非关节轨迹重放。 |
| 4 | **[VoxPoser](https://arxiv.org/abs/2307.05973)**<br>VoxPoser: Composable 3D Value Maps for Robotic Manipulation with Language Models | 三维价值图与连续运动优化 | 将语言要求转为空间价值和约束，再优化连续运动。与离散技能选择比较控制粒度、规划方式和反馈需求。 |
| 5 | **[SayPlan](https://arxiv.org/abs/2307.06135)**<br>SayPlan: Grounding Large Language Models using 3D Scene Graphs for Scalable Robot Task Planning | 层级场景图与符号规划 | 利用层级场景图缩小搜索范围，结合符号规划与执行反馈完成长程任务。梳理环境表示、搜索和结果检查的接口。 |

<details>
<summary>补充阅读（2 篇）</summary>

需要几何约束求解时读 ReKep；需要设计编码智能体评测时读 CaP-X。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[ReKep](https://rekep-robot.github.io/)**（2024）<br>ReKep: Spatio-Temporal Reasoning of Relational Keypoint Constraints for Robotic Manipulation | 将语言任务转成三维关键点之间的数值约束，用层级优化求解末端运动，并根据关键点跟踪重新规划，连接语义要求与几何求解。 | 接在 VoxPoser 后，比较价值场与关系约束；也可与 FUNCTO 比较功能对应。分别检查关键点感知、约束生成和优化的错误。 |
| **[CaP-X](https://arxiv.org/abs/2603.22435)**（2026）<br>CaP-X: A Framework for Benchmarking and Improving Coding Agents for Robot Manipulation | 在不同工具抽象、交互和感知条件下评测编码智能体，研究多轮反馈、视觉差分、技能合成和可验证奖励。适合分析预设工具对任务表现的贡献。 | 接在 Code as Policies 后阅读。比较时固定可用工具、尝试次数和执行预算，以便判断模型和工具各自的贡献。 |

</details>

<a id="a7"></a>
### A7. Agentic：技能记忆与持续适应

**研究问题：** 智能体应该保存哪些经验，经验如何改变下一次任务的表现？

**先修知识：** 先读 A6；补充场景图、经验检索、程序技能与策略参数更新。

**阅读顺序：** 世界知识 → 文本反思 → 程序技能 → 持久参数学习 → 快速权重记忆

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | **[ConceptGraphs](https://arxiv.org/abs/2309.16650)**<br>ConceptGraphs: Open-Vocabulary 3D Scene Graphs for Perception and Planning | 对象与关系组成的空间语义记忆 | 将多视角观测整理为三维对象及其关系，支持环境查询与规划。关注场景图的构建、更新和使用。 |
| 2 | **[Reflexion](https://arxiv.org/abs/2303.11366)**<br>Reflexion: Language Agents with Verbal Reinforcement Learning | 任务反馈驱动的文本反思记忆 | 把任务反馈整理成反思文本，供后续尝试读取，模型参数保持不变。阅读记忆的生成与调用方式；机器人应用还需执行验证。 |
| 3 | ★ **[ASPIRE](https://arxiv.org/abs/2607.00272)**<br>ASPIRE: Agentic /Skills Discovery for Robotics | 经执行验证的可复用程序技能 | 将验证通过的程序修复结果整理为技能，供后续任务检索。关注写入条件、检索方式和跨任务复用效果。 |
| 4 | **[RoboCat](https://arxiv.org/abs/2306.11706)**<br>RoboCat: A Self-Improving Generalist Agent for Robotic Manipulation | 自主数据采集与持久策略更新 | 由适配后的策略采集更多数据，再训练下一轮通用策略。与外部代码技能库比较经验的存储方式和更新成本。 |
| 5 | ★ **[RoboTTT](https://arxiv.org/abs/2607.15275)**<br>RoboTTT: Context Scaling for Robot Policies | 测试时更新的快速权重记忆 | 在测试时用快速权重吸收历史信息。比较更新对象、历史压缩和推理成本，以及与固定上下文、离线再训练的差别。 |

<details>
<summary>补充阅读（2 篇）</summary>

需要主动搜索更好的程序时读 MEMENTO；需要让经验改善数据采集时读 Zero2Skill。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[MEMENTO](https://arxiv.org/abs/2607.22832)**（2026）<br>MEMENTO: Memory-Guided Memetic Code-as-Policy Evolution | 改进轨迹评分器，再让记忆参与程序的局部修改、变异和交叉搜索。与直接复用成功代码相比，增加了候选生成与评价过程。 | 接在 ASPIRE 后，阅读操作任务实验，检查评分器可靠性、搜索成本及未参与调试任务上的收益。 |
| **[Zero2Skill](https://arxiv.org/abs/2607.14047)**（2026）<br>Zero2Skill: Bootstrapping Robot Skills through Autonomous Data Collection, Training, and Deployment | 用纠正记忆保存采集、检查和重置中的有效调整，将自主采集与策略训练连接起来，同时积累执行技能和采集经验。 | 与 ASPIRE 的程序库、RoboCat 的数据再训练对照。关注重试预算、人工求助和复位条件，判断自动运行的范围。 |

</details>

[返回方向导航](#navigation)


---

<a id="worlds"></a>
## 2. 视频生成与世界模型

研究可控视频、多镜头叙事、长期记忆与未来状态预测，以及预测如何服务行动。

**基础知识：** 概率与深度学习、Transformer、条件生成。视频新同学先读 B4 的 DDPM；空间分支补充相机几何，决策分支补充强化学习。

**方向衔接：** 可控视频：[B4](#b4) → [B1](#b1)。交互世界：[B2](#b2) → [B3](#b3) → [B4](#b4)。机器人决策：[B2](#b2) → [B5](#b5)。

<a id="b1"></a>
### B1. 可控视频与多镜头叙事

**研究问题：** 多个镜头如何共同表达一个故事，并保持人物、动作、运镜和场景状态的衔接？

**先修知识：** 条件生成、视频扩散、故事板、关键帧和相机轨迹。

**阅读顺序：** 语义布局 → 首尾视觉锚点 → 运镜轨迹 → 身份记忆 → 显式世界编排

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | ★ **[VideoDirectorGPT](https://arxiv.org/abs/2309.15091)**<br>VideoDirectorGPT: Consistent Multi-scene Video Generation via LLM-Guided Planning | 结构化场景与布局计划 | 将故事拆成实体、场景和布局计划，再输入视频模型。关注语言规划如何转化为空间条件。 |
| 2 | ★ **[STAGE](https://arxiv.org/abs/2512.12372)**<br>STAGE: Storyboard-Anchored Generation for Cinematic Multi-shot Narrative | 逐镜头首尾帧锚定 | 通过逐镜头首尾帧预测约束视频生成。比较首帧、首尾双锚点和分镜文本三种条件，并阅读训练数据的构建。 |
| 3 | ★ **[ShotVerse](https://arxiv.org/abs/2603.11421)**<br>ShotVerse: Advancing Cinematic Camera Control for Text-Driven Multi-Shot Video Creation | 镜头语言到相机轨迹的规划 | 将镜头语言转成相机轨迹，再控制多镜头生成。分别评估轨迹响应、切镜衔接和主体保持。 |
| 4 | ★ **[IAMFlow](https://arxiv.org/abs/2605.18733)**<br>Advancing Narrative Long Video Generation via Training-Free Identity-Aware Memory | 身份感知的历史记忆与生成校验 | 在长视频中维护、检索并校验实体身份。关注外观身份、动作阶段和空间关系分别如何处理。 |
| 5 | ★ **[World Narrative Model](https://arxiv.org/abs/2606.31946)**<br>World Narrative Model for Highly Controllable Video Generation: A Paradigm Shift from Pixel Sampling to Physical World Orchestration | 显式世界状态编排与生成式渲染 | 先组织场景、主体运动、相机和时间关系，再生成画面。阅读可编辑的状态接口，并考察场景规模扩大后的适用性。 |

<details>
<summary>补充阅读（1 篇）</summary>

比较关键帧、外部规划与模型内部的多镜头表示时，可补读下列工作。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[MultiShotMaster](https://arxiv.org/abs/2512.03041)**（2025）<br>MultiShotMaster: A Controllable Multi-Shot Video Generation Framework | 通过镜头边界相位、时空定位等位置编码组织多镜头条件，在模型内部表示切镜与参考实体。可与外部分镜和关键帧控制对照。 | 接在 STAGE、ShotVerse 后，比较首尾帧、相机轨迹和位置编码的作用。人物身份、动作阶段和物理关系需分别评估。 |

</details>

<a id="b2"></a>
### B2. 交互世界模型：状态表示与未来预测

**研究问题：** 未来应表示为视频、物体状态、可渲染场景，还是用于决策的预测特征？

**先修知识：** 动作条件预测、序列模型、隐变量、相机几何与神经场。

**阅读顺序：** 潜在动作 → 像素动力学 → 显式三维状态 → 共享场景表示 → 联合嵌入预测

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | **[Genie](https://arxiv.org/abs/2402.15391)**<br>Genie: Generative Interactive Environments | 离散视觉 token 与潜在动作 | 从无动作标注的视频中学习潜在动作，再生成后续观测。关注潜在动作的可控性及其与实际机器人动作的对应问题。 |
| 2 | **[DIAMOND](https://arxiv.org/abs/2405.12399)**<br>Diffusion for World Modeling: Visual Details Matter in Atari | 像素空间扩散动力学 | 用扩散模型预测下一观测，并支持智能体学习。与离散 token 方法比较视觉细节、预测成本和多步误差。 |
| 3 | ★ **[Marionette](https://arxiv.org/abs/2608.14530)**<br>Marionette: Predicting World States, Rendering Geometry, Painting Appearance | 显式关节状态预测与确定性几何渲染 | 将关节状态预测、几何渲染和外观生成分开处理。关注状态编辑与纠错接口，以及未由显式状态覆盖的物理过程。 |
| 4 | ★ **[NeuWorld](https://arxiv.org/abs/2606.30045)**<br>Walking in the Implicit: Interactive World Exploration via Neural Scene Representation | 固定容量的可渲染神经场景 | 以共享神经场景生成不同相机视角，并用历史信息维护场景。阅读编码、更新和渲染过程，检查长时回看的空间一致性。 |
| 5 | **[V-JEPA 2](https://arxiv.org/abs/2506.09985)**<br>V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning | 不解码像素的联合嵌入预测 | 在特征空间预测视频，再进行动作条件适配。与像素生成方法比较预测目标，以及保留的信息如何服务理解与规划。 |

<details>
<summary>补充阅读（2 篇）</summary>

机器人策略评估优先读 Ctrl-World；持续交互与实时生成优先读 WorldPlay。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[Ctrl-World](https://arxiv.org/abs/2510.10125)**（2025）<br>Ctrl-World: A Controllable Generative World Model for Robot Manipulation | 利用机器人动作、多视角观测和历史预测未来，并将模型用于操作策略评估和合成轨迹生成，直接考察预测对策略研究的用途。 | 接在 Genie、V-JEPA 2 后。检查动作响应、虚实策略排名和多步漂移，评估其作为真实接触实验替代工具的范围。 |
| **[WorldPlay](https://arxiv.org/abs/2512.14614)**（2025）<br>WorldPlay: Towards Long-Term Geometric Consistency for Real-Time Interactive World Modeling | 结合动作表示、历史上下文重构和 Context Forcing，协调持续生成与少步推理。关注教师与学生在蒸馏时的记忆条件。 | 接在 NeuWorld 后，与 B4 的 Self Forcing 比较。实验主要面向交互式视觉世界，机器人接触控制需另行验证。 |

</details>

<a id="b3"></a>
### B3. 长期记忆、实体关系与共享状态

**研究问题：** 怎样让历史内容可被找回、实体关系受到约束，并让多个视角对应同一世界？

**先修知识：** 历史检索、KV 缓存、相机投影、场景图与状态转移；先读 B2。

**阅读顺序：** 动静态检索 → 缓存寻址 → 三维投影 → 图关系监督 → 共享逻辑状态

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | ★ **[HyDRA](https://arxiv.org/abs/2603.25716)**<br>Out of Sight but Not Out of Mind: Hybrid Memory for Dynamic Video World Models | 动态主体与静态场景的混合记忆 | 按时空相关性检索动态主体和静态场景的历史。检查主体重新进入视野时，外观、位置和运动状态是否正确。 |
| 2 | ★ **[WorldTrace](https://arxiv.org/abs/2608.07408)**<br>Addressable Memory for Video World Models | 位置重映射与可寻址 KV 缓存 | 通过位置重映射与压缩改善长历史访问。阅读缓存的组织、寻址和细节保留机制。 |
| 3 | ★ **[MosaicMem](https://arxiv.org/abs/2603.17117)**<br>MosaicMem: Hybrid Spatial Memory for Controllable Video World Models | 三维锚定与目标视角的图块投影 | 将历史图块锚定到三维，再投影至当前视角。与整帧检索比较空间对齐、局部细节和动态变化的处理。 |
| 4 | ★ **[图关系约束视频生成](https://aclanthology.org/2026.acl-long.172/)**<br>Bringing Real-World Relations into Video Generation with Graph-Structured Knowledge | 同步图编辑与视频编辑的条件监督 | 利用同步编辑的视频与图，通过 Graph-Aligned Denoising Loss（GADL）约束节点和关系变化。阅读关系监督的构造；视野外状态演化不在该约束的保证范围内。 |
| 5 | ★ **[MASS](https://arxiv.org/abs/2608.06257)**<br>MASS: Multiplayer World Models with Authoritative Shared State | 共享逻辑状态与多视角渲染解耦 | 由逻辑引擎更新共享状态，再分别生成各玩家视角。关注状态同步接口，以及受控游戏环境与开放物理环境的差异。 |

<details>
<summary>补充阅读（1 篇）</summary>

研究主体离开视野后的状态变化时，可补读 LiveWorld。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[LiveWorld](https://arxiv.org/abs/2603.07145)**（2026）<br>LiveWorld: Simulating Out-of-Sight Dynamics in Generative Video World Models | 通过监视视角等机制推进视野外事件，研究动态实体在不可见期间的状态变化，补充静态场景保存和历史检索方法。 | 接在 HyDRA、MASS 后，比较历史检索、隐藏事件推演和共享状态。检查回看时的时间、因果与物理一致性。 |

</details>

<a id="b4"></a>
### B4. 视频训练：生成基础、时序建模与反馈优化

**研究问题：** 如何从生成目标、历史条件、训练数据和自验证反馈改善视频模型？

**先修知识：** 概率分布、扩散模型、序列预测、训练与推理分布差异。

**阅读顺序：** 扩散训练基础 → 分位置噪声条件 → 自滚动训练 → 混合数据适配 → 自验证强化

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | **[DDPM](https://arxiv.org/abs/2006.11239)**<br>Denoising Diffusion Probabilistic Models | 多步扩散去噪 | 阅读前向加噪、去噪目标和反向采样，作为后续条件生成与时序训练的基础。 |
| 2 | **[Diffusion Forcing](https://arxiv.org/abs/2407.01392)**<br>Diffusion Forcing: Next-token Prediction Meets Full-Sequence Diffusion | 逐位置噪声条件的序列训练 | 为序列不同位置设置不同噪声水平，统一带噪历史和未来预测。关注噪声分布的设计及其对序列条件的影响。 |
| 3 | **[Self Forcing](https://arxiv.org/abs/2506.08009)**<br>Self Forcing: Bridging the Train-Test Gap in Autoregressive Video Diffusion | 自生成历史下的滚动训练 | 训练时使用模型自身生成的历史，减少训练与推理的条件差异。阅读滚动生成、误差积累和梯度计算的安排。 |
| 4 | ★ **[Coarse-to-Real](https://arxiv.org/abs/2601.22301)**<br>Coarse-to-Real: Generative Rendering for Populated Dynamic Scenes | 真实视频与少量配对场景的混合适配 | 用真实视频学习外观与运动先验，用粗场景配对数据学习控制对应。关注控制适配器的训练和两类数据的分工。 |
| 5 | ★ **[WorldCycle](https://arxiv.org/abs/2608.04964)**<br>WorldCycle: Self-Verifiable Reinforcement Learning for Long-Horizon Video World Models | 循环与回看约束的自验证强化学习 | 从动作循环与回看构造反馈，改进长程生成。检查动态场景中的约束是否成立，以及静止输出是否会获得虚假的一致性奖励。 |

<details>
<summary>补充阅读（3 篇）</summary>

架构与训练目标不熟悉时，先补 DiT 和 Flow Matching；做三维一致性后训练时再读 World-R1。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[DiT](https://arxiv.org/abs/2212.09748)**（2022）<br>Scalable Diffusion Models with Transformers | 用 Transformer 处理潜空间图块，研究生成质量与计算规模的关系。[Step-Video-T2V](https://arxiv.org/abs/2502.10248)等视频系统采用了这一架构路线。 | 读完 DDPM 后补读，比较生成目标与网络结构。原论文以图像为主，动作条件和长期记忆属于后续扩展。 |
| **[Flow Matching](https://arxiv.org/abs/2210.02747)**（2022）<br>Flow Matching for Generative Modeling | 沿概率路径回归速度场，学习从简单分布到数据分布的变换。[Step-Video-T2V](https://arxiv.org/abs/2502.10248)使用 Flow Matching 训练视频 DiT。 | 接在 DDPM 后，比较预测量、概率路径和采样过程，再读 Flow-GRPO。效率与生成质量需在相同预算下评估。 |
| **[World-R1](https://arxiv.org/abs/2604.24764)**（2026）<br>World-R1: Reinforcing 3D Constraints for Text-to-Video Generation | 利用预训练三维模型和视觉语言模型构造反馈，通过 Flow-GRPO 与周期性解耦训练平衡几何一致性和动态变化，无须将三维模块嵌入生成器。 | 与 WorldCycle 对照外部评估和循环自验证两类反馈。两者同属后训练路线，均需检查奖励误差和静止化等投机行为。 |

</details>

<a id="b5"></a>
### B5. 世界模型用于机器人规划与决策

**研究问题：** 预测未来之后，怎样选择动作，或学习可以直接执行的机器人策略？

**先修知识：** 奖励与价值函数、模型预测控制、策略学习、目标条件与逆动力学。

**阅读顺序：** 树搜索 → 连续动作优化 → 想象式策略学习 → 跨本体目标预测 → 视频计划解码

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | **[MuZero](https://arxiv.org/abs/1911.08265)**<br>Mastering Atari, Go, Chess and Shogi by Planning with a Learned Model | 学习模型上的价值引导树搜索 | 在学习模型上进行价值引导的树搜索。阅读模型的预测目标和搜索过程，再与连续动作规划比较。 |
| 2 | **[TD-MPC2](https://arxiv.org/abs/2310.16828)**<br>TD-MPC2: Scalable, Robust World Models for Continuous Control | 隐空间中的连续动作优化 | 在隐空间中在线优化动作序列，并用终端价值辅助评估。梳理预测、候选动作评估和实际执行的循环。 |
| 3 | **[DreamerV3](https://arxiv.org/abs/2301.04104)**<br>Mastering Diverse Domains through World Models | 想象轨迹上的策略与价值学习 | 在模型预测的未来中训练策略与价值函数。与每步在线优化动作的方法比较，关注模型在哪个阶段被使用。 |
| 4 | ★ **[Demo-JEPA](https://arxiv.org/abs/2605.20811)**<br>Demo-JEPA: Joint-Embedding Predictive Architecture for One-shot Cross-Embodiment Imitation | 跨本体预测表示与目标匹配规划 | 将人类示范编码为未来目标，结合机器人自身学到的动力学进行规划。关注跨本体目标表示和匹配方式。 |
| 5 | **[UniPi](https://arxiv.org/abs/2302.00111)**<br>Learning Universal Policies via Text-Guided Video Generation | 视频计划与逆动力学解码 | 先生成目标导向的视频，再用逆动力学映射为动作。检查视频计划的可执行性，以及预测误差如何影响控制。 |

<details>
<summary>补充阅读（2 篇）</summary>

目标图像规划读 DINO-WM；比较整段轨迹生成与单步动力学规划时读 Diffuser。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[DINO-WM](https://arxiv.org/abs/2411.04983)**（2024）<br>DINO-WM: World Models on Pre-trained Visual Features enable Zero-shot Planning | 直接预测预训练 DINOv2 的空间图块特征，用目标图像特征约束动作序列，无须重建像素或另学奖励、逆动力学。 | 接在 Demo-JEPA、TD-MPC2 后，阅读推动等操作任务。零样本规划仍依赖离线交互数据及其动力学覆盖。 |
| **[Diffuser](https://arxiv.org/abs/2205.09991)**（2022）<br>Planning with Diffusion for Flexible Behavior Synthesis | 直接学习整段轨迹的分布，通过条件和价值引导生成计划，提供了单步动力学展开以外的规划方式。 | 接在 TD-MPC2、UniPi 后，阅读操作和堆叠实验。比较状态轨迹与视频计划的可执行性，以及离线数据覆盖和引导强度的影响。 |

</details>

[返回方向导航](#navigation)


---

<a id="cad"></a>
## 3. 智能 CAD/CAM

研究从设计要求、工程图与三维观测获得可编辑模型，并把几何信息连接到制造过程。

**基础知识：** 参数化草图、尺寸约束、布尔运算、B-rep 与网格的区别。制造分支补充毛坯、刀具、工序和装夹。

**方向衔接：** 先读 [C1](#c1) 理解表示与建模，再选 [C2](#c2) 处理图纸和逆向建模，或进入 [C3](#c3) 学习制造与刀路。

<a id="c1"></a>
### C1. 可编辑 CAD：表示、生成与迭代优化

**研究问题：** 怎样从建模操作、几何约束和代码程序出发，得到可修改的工程模型？

**先修知识：** 参数化草图、尺寸约束、拉伸、布尔运算、B-rep 与建模历史。

**阅读顺序：** 操作序列 → 约束图 → 可执行代码 → 结构化编辑 → 程序与参数优化

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | **[DeepCAD](https://arxiv.org/abs/2105.09492)**<br>DeepCAD: A Deep Generative Network for Computer-Aided Design Models | 参数化建模操作序列 | 通过草图和拉伸序列表示 CAD 模型。阅读操作、参数与最终实体的对应关系。 |
| 2 | **[SketchGraphs](https://arxiv.org/abs/2007.08506)**<br>SketchGraphs: A Large-Scale Dataset for Modeling Relational Geometry in Computer-Aided Design | 草图实体与几何约束图 | 用图表示草图实体及其尺寸、平行、重合等约束。比较关系表示与直接预测坐标的差别。 |
| 3 | ★ **[Text-to-CadQuery](https://arxiv.org/abs/2505.06507)**<br>Text-to-CadQuery: A New Paradigm for CAD Generation with Scalable Large Model Capabilities | 语言模型生成可执行建模代码 | 将自然语言转成参数化代码，由几何内核执行。分别检查程序运行、实体有效性与设计要求。 |
| 4 | ★ **[CAD-Refiner](https://openaccess.thecvf.com/content/CVPR2026/html/Yuan_CAD-Refiner_A_Unified_Framework_for_CAD_Generation_and_Iterative_Editing_CVPR_2026_paper.html)**<br>CAD-Refiner: A Unified Framework for CAD Generation and Iterative Editing | 结构化表示上的多轮 CAD 编辑 | 利用结构信息定位修改对象并执行多轮编辑。关注非目标结构的保留，以及与直接改写建模序列的差异。 |
| 5 | ★ **[CADFit](https://arxiv.org/abs/2605.01171)**<br>CADFit: Precise Mesh-to-CAD Program Generation with Hybrid Optimization | 离散建模程序与连续参数的混合优化 | 结合离散操作搜索和连续参数拟合，从网格恢复 CAD 程序。分别评估几何误差、可执行性和可编辑性，并确认哪些环节依赖数值优化。 |

<details>
<summary>补充阅读（2 篇）</summary>

需要直接生成边界实体时读 BrepGen；需要从单零件进入装配关系时读 JoinABLe。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[BrepGen](https://arxiv.org/abs/2401.15563)**（2024）<br>BrepGen: A B-rep Generative Diffusion Model with Structured Latent Geometry | 通过结构化潜几何与层次表示生成面、边及其连接，直接输出边界实体，可与生成建模程序的方法对照。 | 接在 DeepCAD、Text-to-CadQuery 后。分别检查边界有效性、参数依赖、编辑历史和制造约束。 |
| **[JoinABLe](https://arxiv.org/abs/2111.12772)**（2021）<br>JoinABLe: Learning Bottom-up Assembly of Parametric CAD Joints | 从零件几何预测关节和配合关系，将单零件建模扩展到连接与运动约束，适合进入学习式装配设计。 | 完成单零件建模后再读。公差、干涉、连接件设计、装配顺序和路径仍需另外验证。 |

</details>

<a id="c2"></a>
### C2. 工程图与三维观测：信息提取和逆向建模

**研究问题：** 怎样从图纸或三维观测获得工程信息，再恢复满足尺寸与几何要求的模型？

**先修知识：** 正投影、视图对应、尺寸与单位、矢量图元、点云和曲面。

**阅读顺序：** 非几何信息 → 正投影推理 → 矢量序列生成 → 视觉语言程序生成 → 曲面与拓扑重建

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | ★ **[工程图结构化解析](https://arxiv.org/abs/2505.01530)**<br>Automated Parsing of Engineering Drawings for Structured Information Extraction Using a Fine-tuned Document Understanding Transformer | 区域检测与工程文档信息抽取 | 提取材料、技术要求和其他图纸字段，为几何重建补充工程信息。关注区域检测与字段抽取的准确性。 |
| 2 | ★ **[CReFT-CAD](https://arxiv.org/abs/2506.00568)**<br>CReFT-CAD: Boosting Orthographic Projection Reasoning for CAD via Reinforcement Fine-Tuning | 强化微调的正投影空间推理 | 通过强化微调提高正投影视图、尺寸和相对关系的推理能力。阅读训练设置与尺寸正确性的验证方法。 |
| 3 | ★ **[Drawing2CAD](https://arxiv.org/abs/2508.18733)**<br>Drawing2CAD: Sequence-to-Sequence Learning for CAD Generation from Vector Drawings | 矢量图元到 CAD 操作的序列学习 | 从矢量图元生成 CAD 建模序列。关注图元结构的利用方式，以及矢量输入包含了哪些栅格图像没有直接提供的信息。 |
| 4 | ★ **[Ortho2CAD](https://arxiv.org/abs/2607.08891)**<br>Ortho2CAD: 3D CAD Generation from Orthographic Drawings Using Vision Language Models | 正投影图到可执行 CAD 程序 | 利用视觉语言模型理解正投影图并生成程序。与 Drawing2CAD 比较输入信息、求解方式和监督目标。 |
| 5 | **[Point2CAD](https://arxiv.org/abs/2312.04962)**<br>Point2CAD: Reverse Engineering CAD Models from 3D Point Clouds | 点云曲面拟合与边界拓扑重建 | 从点云分解曲面，恢复边界与拓扑。与图纸重建比较三维观测提供的信息，以及仍需求解的几何关系。 |

<details>
<summary>补充阅读（2 篇）</summary>

需要扫描到建模程序时读 CAD-Recode；需要可解释的拉伸几何求解时读 Point2Cyl。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[CAD-Recode](https://arxiv.org/abs/2412.14042)**（2024）<br>CAD-Recode: Reverse Engineering CAD Code from Point Clouds | 将点云编码接入预训练代码语言模型，输出可执行的草图—拉伸 Python 程序。与 Point2CAD 的逐面恢复相比，输出包含建模过程。 | 接在 Point2CAD、Ortho2CAD 后，与 CADFit 比较直接预测和反馈搜索。关注设计意图的多解性及真实扫描噪声。 |
| **[Point2Cyl](https://arxiv.org/abs/2112.09329)**（2021）<br>Point2Cyl: Reverse Engineering 3D Objects from Point Clouds to Extrusion Cylinders | 先预测点分组、法向和底面／侧面等几何信息，再解析估计截面与拉伸参数，为直接预测建模代码提供几何求解上的对照。 | 接在 Point2CAD 后。文中的 extrusion cylinders 指截面拉伸体，不限于圆柱；方法仍受拉伸表示和几何分解假设的约束。 |

</details>

<a id="c3"></a>
### C3. CAM：制造特征、工艺优化与刀路

**研究问题：** 怎样从零件几何获得加工语义、安排工序，并生成满足表面精度的刀路？

**先修知识：** 面邻接、体素、B-rep、毛坯、刀具、装夹、材料去除与加工精度。

**阅读顺序：** 符号特征识别 → 体素特征学习 → 边界图学习 → 工艺组合优化 → 几何刀路求解

| 顺序 | 论文 | 主要方法 | 阅读重点 |
| :---: | --- | --- | --- |
| 1 | **[AAG 规则识别](https://doi.org/10.1016/0010-4485(88)90050-4)**<br>Graph-based Heuristics for Recognition of Machined Features from a 3D Solid Model | 属性邻接图上的符号规则 | 利用面邻接和几何属性识别加工特征。阅读规则对制造语义的表达，以及相交特征的处理困难。 |
| 2 | **[FeatureNet](https://doi.org/10.1016/j.cad.2018.03.006)**<br>FeatureNet: Machining Feature Recognition Based on 3D Convolution Neural Network | 体素表示上的三维卷积学习 | 将几何转成体素，用三维卷积识别加工特征。与规则方法比较数据依赖、特征表达和分辨率限制。 |
| 3 | **[AAGNet](https://doi.org/10.1016/j.rcim.2023.102661)**<br>AAGNet: A Graph Neural Network towards Multi-task Machining Feature Recognition | B-rep 属性图上的多任务图学习 | 利用 B-rep 的几何与拓扑关系，联合识别面语义、特征实例及底面。关注输出如何支持后续工艺规划。 |
| 4 | **[GA–SA 工艺优化](https://doi.org/10.1080/00207540110119991)**<br>Hybrid Genetic Algorithm and Simulated Annealing Approach for the Optimization of Process Plans for Prismatic Parts | 遗传算法与模拟退火的组合搜索 | 在工序先后约束下选择资源、装夹和加工顺序。阅读可行解编码、目标函数和组合搜索过程；刀路生成属于后续步骤。 |
| 5 | **[等残留高度刀路](https://doi.org/10.1016/S0010-4485(01)00136-1)**<br>Constant Scallop-Height Tool Path Generation for Three-Axis Sculptured Surface Machining | 曲面偏置与刀具路径的几何求解 | 由残留高度和刀具几何确定相邻路径间距。阅读精度约束的表达，并检查几何路径转成机床程序前的验证要求。 |

<details>
<summary>补充阅读（2 篇）</summary>

研究工序预测读 DeepMS；研究指定刀具可达性读 DeepMill。两者的第一步实践都是离线验证。

| 论文（年份） | 推荐理由 | 阅读建议 |
| --- | --- | --- |
| **[DeepMS](https://doi.org/10.1016/j.jmsy.2025.07.022)**（2025）<br>DeepMS: A Data-Driven Approach to Machining Process Sequencing Using Transformers | 从零件体素几何预测加工操作序列，并表示中间加工体积与步骤差量。可结合[作者实现](https://github.com/jaimemaqueda/DeepMS)检查输入输出及加工过程表示。 | 接在 GA–SA 工艺优化后，比较监督预测与约束搜索。预测工序还需验证装夹、可达性和切削参数，再进入刀路生成。 |
| **[DeepMill](https://arxiv.org/abs/2502.06093)**（2025）<br>DeepMill: Neural Accessibility Learning for Subtractive Manufacturing | 通过刀具条件的双头八叉树网络预测不可达和遮挡区域，将工件几何与刀具尺寸同时纳入可制造性判断。 | 接在 AAGNet 与刀路基础后。用几何碰撞检查和加工仿真核验神经网络预测，再评估实际执行条件。 |

</details>

[返回方向导航](#navigation)

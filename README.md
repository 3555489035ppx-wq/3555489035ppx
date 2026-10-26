# AI 产品设计与交互原型

从问题定义、AI 工作流到可运行的产品原型。关注设计依据、用户控制与实现边界，让界面背后的决策同样清晰。

[产品作品](#产品作品) · [设计工具](#设计工具) · [设计原则](#设计原则) · [Fork 与研究](#fork-与研究)

## 产品作品

### Muse AI Workspace · 设计决策工作台

将模糊需求、研究证据、设计洞察、方向比较与概念评审串成可追溯的决策链。

- **看点**：工作空间中的上下游关系、方向比较、版本与决策记录。
- **当前形态**：可运行 MVP；离线 Demo 与服务端 AI 配置边界分开说明。
- [在线演示](https://muse-ai-workspace.vercel.app/) · [项目与案例](https://github.com/3555489035ppx-wq/muse-ai-workspace)

### AI Learning Planner · 假期跃迁

将成绩、目标、可用时间与执行证据转成可解释、可调整的学习计划。

- **看点**：课程诊断、阶段与周课表分层、中断恢复、调整预览和撤销。
- **当前形态**：本地规则驱动的学习规划 Demo，不代表远程模型判断或学习效果验证。
- [在线演示](https://ai-learning-planner-sepia.vercel.app/) · [项目与案例](https://github.com/3555489035ppx-wq/ai-learning-planner)

### Memory Universe · 记忆宇宙

用照片、音乐与空间关系组织可探索的记忆体验，以本地优先方式处理个人素材。

- **看点**：时间、人物、地点、情绪视角，3D 记忆空间与本地素材流程。
- **当前形态**：高中回忆 Demo；在线 AI 整理、跨设备同步和其他主题仍属后续范围。
- [在线演示](https://memory-universe-two.vercel.app/) · [项目与案例](https://github.com/3555489035ppx-wq/memory-universe)

### 走走 ZOUZOU · 移动端出行体验

围绕想法澄清、方案选择、行程执行与回顾，探索移动端旅行规划的交互闭环。

- **看点**：结构化意图提取、时间与预算约束、行程选择和执行状态。
- **当前形态**：仓库保留本地交互原型及云端发布说明；实时地点数据与实际验收边界见项目文档。
- [站点入口](https://zouzou.ppx.wiki) · [项目与发布说明](https://github.com/3555489035ppx-wq/zouzou)

## 设计工具

### Adaptive Liquid Glass UI

面向 Codex 的可复用界面设计 Skill。根据背景、品牌色与信息层级推导玻璃材质，同时保留交互状态、移动端可读性和无障碍降级。

[独立工具仓库](https://github.com/3555489035ppx-wq/glass-ui-skill) · [完整 Skill](https://github.com/3555489035ppx-wq/glass-ui-skill/tree/main/adaptive-liquid-glass-ui)

## 设计原则

- AI 进入具体用户流程，每一步有输入、上下文、输出和下一步。
- 重要决策保留查看依据、编辑、拒绝、确认与撤销的空间。
- 本地规则、演示素材与真实模型结果明确区分。
- 先建立产品价值与信息层级，再决定视觉效果。

```text
问题定义 → 研究与策略 → AI 工作流 → 交互与界面 → 前端实现 → 测试与案例复盘
```

作品持续探索三个问题：如何保留设计方向的推导过程，如何让学习计划从中断中恢复，以及如何在空间交互中尊重个人记忆的隐私。

## Fork 与研究

以下是上游项目的 Fork，不作为原创产品展示；功能、维护状态与许可证以上游说明为准。

- [dsh-purge](https://github.com/3555489035ppx-wq/dsh-purge)：直接 Fork 自 [mmparko/dsh-purge](https://github.com/mmparko/dsh-purge)，其镜像说明署名原作者 [YuJunZhiXue/dsh-purge](https://github.com/YuJunZhiXue/dsh-purge)。
- [rea](https://github.com/3555489035ppx-wq/rea)：上游 [morluto/rea](https://github.com/morluto/rea)。

## 关于此仓库

这里是作品目录，也保留 Adaptive Liquid Glass UI Skill 与参考资料。它是普通项目仓库，不是与账号同名的 GitHub Profile README 仓库。本仓库的 [Skill 指令](skills/adaptive-liquid-glass-ui/SKILL.md) 与 [参考资料](skills/adaptive-liquid-glass-ui/references/adaptive-liquid-glass.md) 可直接阅读。应用代码与具体使用边界请前往对应项目查看。

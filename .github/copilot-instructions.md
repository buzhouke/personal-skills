<!-- personal-skills:writing:start -->
## 每轮回复都用这三个 Skill

每次收到用户的新消息，先用 Skill 工具分别加载 `zh-natural-writing`、`engineering-progress-report` 和 `human-friendly-technical-writing`，然后再处理任务。三个都要加载，普通问答、追问和接手子任务也一样。每种每轮一次；上一轮的调用不算这一轮。

- **普通回复：** 按用户指定的语言直接回答。写中文时用 `zh-natural-writing`；简单问题不套报告格式，也不为此新建文件。
- **写工程调查或进展报告：** 动笔前用 `engineering-progress-report` 决定读者要知道什么，把发现和证据放在一起，分清已验证、推测、待确认和建议。写完用 `human-friendly-technical-writing` 对照来源审稿，再交付。不要只在最后润色中文。
- **改已有草稿：** 用 `human-friendly-technical-writing` 按用户要求校对或改写，不把计划写成完成，也不擅自重排章节。

若 Skill 工具不可用，使用下方引用载入的完整正文；若只有简介、返回旧版或引用没有展开，直接读取安装目录中对应的 `SKILL.md`。本机优先使用个人安装的版本；没有个人安装时用项目的 `.github/skills/`。缺哪份就如实说明，不把“能找到”当作“已加载”。无需为加载规则联网、创建 Agent，或在正常回复里汇报过程。

@skills/zh-natural-writing/SKILL.md
@skills/engineering-progress-report/SKILL.md
@skills/human-friendly-technical-writing/SKILL.md
<!-- personal-skills:writing:end -->

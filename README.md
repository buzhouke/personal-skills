# 个人 Skill 仓库

- [中文自然写作](.github/skills/zh-natural-writing/SKILL.md)：写中文消息、技术说明和工作汇报时，用自然的措辞说清楚事情。[改写示例](.github/skills/zh-natural-writing/references/examples.md)里也列了哪些句子不用改。
- [中英文技术文档校对与改写](.github/skills/human-friendly-technical-writing/SKILL.md)：手里已有草稿时，用它理顺段落、解释临时代号，保留数字、术语和原文的把握程度。比如，“只在测试环境验证过”不会被改成“问题已解决”。
- [工程调查与进度汇报](.github/skills/engineering-progress-report/SKILL.md)：手里有代码、日志或测试记录，要给没参与排查的人写报告时用。先交代为什么查、查到了什么、还有什么没查清；需要解释复杂关系时再配图。默认交付一份文档。

**在自己的 Copilot 里用：** 从 [`.github/skills/`](.github/skills/) 把需要的 Skill 整个目录复制到 `~/.copilot/skills/`，再新开会话。只在一个项目里用，就复制到该仓库的 `.github/skills/`。校对草稿时可以直接说：“用 `/human-friendly-technical-writing` 改这份技术说明，只改措辞，不换标题。”

如果希望每次回复都加载中文自然写作，把[这段指令](.github/copilot-instructions.md)追加到 `~/.copilot/copilot-instructions.md`，保留原有内容。它只要求加载 `zh-natural-writing`；另外两个 Skill 按需使用。

中文自然写作保留了[早期上游项目](https://github.com/Onenightcarnival/zh-natural-writing)的 [MIT 版权声明](.github/skills/zh-natural-writing/LICENSE)。

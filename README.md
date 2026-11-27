# 个人 Skill 仓库

- [中文自然写作](.github/skills/zh-natural-writing/SKILL.md)：写中文消息、技术说明和工作汇报时，用自然的措辞说清楚事情。[改写示例](.github/skills/zh-natural-writing/references/examples.md)里也列了哪些句子不用改。
- [中英文技术文档校对与改写](.github/skills/human-friendly-technical-writing/SKILL.md)：手里已有草稿时，用它理顺段落、解释临时代号，保留数字、术语和原文的把握程度。比如，“只在测试环境验证过”不会被改成“问题已解决”。
- [工程调查与进度汇报](.github/skills/engineering-progress-report/SKILL.md)：手里有代码、日志或测试记录，要给没参与排查的人写报告时用。先交代为什么查、查到了什么、还有什么没查清；需要解释复杂关系时再配图。默认交付一份文档。

## 第一次安装

这三份 Skill 只在本仓库维护。每台电脑用 GitHub CLI 从这里安装一次，今后不用再复制文件或解压旧 ZIP。下面是 PowerShell 命令，请使用已登录 `github.com` 且支持 `gh skill` 的 GitHub CLI。

```powershell
$dir = Join-Path $HOME '.copilot\skills'
$names = 'zh-natural-writing', 'engineering-progress-report', 'human-friendly-technical-writing'
foreach ($name in $names) {
    gh skill install buzhouke/personal-skills ".github/skills/$name/SKILL.md" --allow-hidden-dirs --dir $dir
    if ($LASTEXITCODE -ne 0) { throw "安装失败：$name" }
}
```

把[默认指令](.github/copilot-instructions.md)合并到 `~/.copilot/copilot-instructions.md`，保留自己的其他设置，然后新开会话。已有 `personal-skills:writing` 标记就替换整段，不重复追加。每轮回复都加载三个 Skill：普通问题直接回答，工程报告先组织背景和证据，成稿后再校对。

## 以后更新

新版本发布后，在已经安装的电脑上运行：

```powershell
gh skill update --dir "$HOME\.copilot\skills" zh-natural-writing engineering-progress-report human-friendly-technical-writing
```

命令只检查这三个名字，按安装时记录的 GitHub 来源更新。手工复制的旧包没有这个记录，要先按上面的步骤安装。如果想自动跟进，可以让每台机器在登录时同步；仓库提交不会即时推送给所有客户端。`gh skill update` 更新技能目录，不更新目录外的个人指令；只有入口规则也改了，才需要重新合并那一段。

已打开的 CLI 会话如果仍看到旧 Skill，可以用 `/skills reload`。改的是个人指令时，退出后恢复原会话，或直接让已有会话读取新指令。`/skills list` 只能证明能找到，哪一轮实际用了要看那一轮的调用或读取记录。

云端 Agent 读不到本机个人目录。要让一个项目使用同样的版本，将这三个技能目录和默认指令按本仓库的 `.github/` 布局提交到该项目。支持 [dotfiles 的 Copilot 云沙箱](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/personalize-cloud-sessions) 也可以从 dotfiles 仓库根目录的 `.copilot/` 加载个人配置；这种方式不适用于 GitHub Actions 执行的会话。

中文自然写作保留了[早期上游项目](https://github.com/Onenightcarnival/zh-natural-writing)的 [MIT 版权声明](.github/skills/zh-natural-writing/LICENSE)。

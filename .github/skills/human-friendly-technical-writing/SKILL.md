---
name: human-friendly-technical-writing
description: "edit an existing technical draft in simplified chinese or english so that a colleague who did not follow the work can read it once and use it, without changing what the evidence supports. use for 技术文档润色、说人话、看不懂、太绕、翻译腔、黑话、去 ai 味, plain-english revision, and for cleaning up agent-written investigation notes, progress reports, readmes, pr descriptions, and markdown/html prose. works only on text that already exists: it does not investigate, verify, or add findings. to decide what a report should contain, use engineering-progress-report first."
---

# 让技术说明好读，不改技术含义

把已有草稿改成同事读一遍就能用的话。读者默认是**懂这个领域、但没跟过这件事的同事**：没看过对话，没看过写稿时读的代码，也不知道过程中临时起的代号。

按用户指定的语言交付；没有翻译要求就保留原文语言。

## 1. 先定改多少

- **校对**（用户说“校对”“只改错”）：只改错字、病句、前后不一致的术语。句序和结构不动。
- **改写**（默认）：可以在段内调整句序、拆并段落、把操作步骤改成列表。章节顺序和标题不动。
- **重组**：用户明确同意才调整章节。如果问题是“这份报告该写什么、不该写什么”，那不属于措辞：有 engineering-progress-report 就先用它定内容，没有就先问用户。

## 2. 动笔前，标出不能改的

- **事实**：谁做了什么、哪个版本、什么条件下、数值和单位、跟什么比、否定、来源。
- **把握程度**：每个结论属于下面哪一种，改完仍是那一种。
  - 跑过、验证过
  - 从代码或文档读到，没有运行
  - 推测
  - 不知道
  
  原文没说是哪一种，不替作者定，列入“待确认”。
- **原样保留**：代码块、行内代码、API 名称、命令、路径、配置键、URL、引用原话、结构化数据。表格可以换位置，不能丢值。
- **标题和 HTML**：获准改标题时，同步检查锚点和引用。编辑 HTML 只改读者看到的文字，不动标记、ID、链接目标。
- **矛盾**：原文前后矛盾就标给作者，不挑一个写通顺。

## 3. 让它好读

按影响从大到小检查。没问题的句子不改。

1. **每段第一句说这段的结论。** 读者只读首句，也该知道这段讲了什么。背景和过程放后面。
2. **临时代号换成它指的东西。** “方案 B”“第二阶段”“the fallback path”这类写稿过程中起的名字，读者没见过。换成所指的内容，或在第一次出现时解释。项目里本来就有的术语不动，同一个概念全文只用一个叫法。
3. **标识符第一次出现时，用半句话说它是什么。** 标识符本身保留。解释只能来自原稿，或你能打开核对的来源；找不到就列入“待确认”，不猜。
4. **删掉过程流水账，留下证据。** “我先查看了……随后……”可以删。但“结论是怎么得到的”要留：读了哪段代码、看了哪份日志、跑了什么。
5. **数字带上单位和比较对象。** 原文没给比较对象，不补，列入“待确认”。
6. **步骤用编号列表，推理留在段落里。** 读者要照着做的操作适合列表；因果推理拆成要点会丢掉“因为”“所以”。
7. **空话可以删，限定不能删。** “仅在本地测过”“可能”“仍未部署”各自提供信息。有条件和例外的一句话，不必拆成三句。

### 简体中文

有 zh-natural-writing 时用它处理措辞；与第 2 节冲突时，以第 2 节为准。只参考与当前句子有关的例子，不从样例里借功能、数据或因果，也不叠加多个“去 AI 味”技能。没有它，照下面做：

- 找到具体的对象和动作。能写“导入器跳过空行”，就不写“实现空值场景的鲁棒性保障”。不知道是谁执行的，不硬补主语。
- 真有先后、转折、因果，才用相应的连接词。
- 语气可以正式，但不用公文话、广告词，也不故作亲切。

### English

Edit in English; do not apply the Chinese rules by translation. The checks in section 3 still apply.

- Put the actor and the action close together when the actor is known. Use the passive when the actor is unknown.
- Name the actual component and the observable behavior instead of "enablement" or "optimization."
- Keep can, may, must, only, at least, and not yet distinct.
- A longer sentence is fine when it keeps a condition next to the claim it limits.

## 4. 例子（教学用，不是项目事实）

**句子**

- “目前已完成对导入日志的核查，尚不具备对线上影响做出准确评估的条件。”
  → “导入日志已查过，线上影响还不能确定。”
  不要补写“线上未受影响”。
- "Validation of the change has been performed in staging only; production impact has not yet been measured."
  → "We only have staging test results for this change. Its impact in production hasn't been measured."
  Do not turn this into "The change works in production."

**段落**（前文写过“方案 B：超时后自动重试”）

原稿：

> 在第二阶段的排查中，我首先对 `RetryPolicy` 的实现进行了深入分析，随后结合日志进行了交叉验证。基于上述分析，可以认为方案 B 所涉及的路径存在重复提交的风险，该问题有较大概率与超时配置相关。

改后：

> 超时后自动重试可能导致重复提交，原因很可能在超时配置。这个判断来自 `RetryPolicy` 的代码和日志。

待确认：“交叉验证”具体做了什么？只读了日志，还是复现过？

这里做了四件事：结论提到句首；“方案 B”换成它指的内容；流水账删掉，证据来源留下；“可能”“很可能”原样保留。没有补写“已复现”或“尚未复现”，因为原稿没说。

## 5. 交付

- 改文件就直接改原文件。不另存副本，不新建 `_v2`、`_final` 之类的文件，不留中间文件，除非用户要求。
- 只动了措辞：只给终稿，不附说明，不自评。
- 出现下面任何一种情况，在终稿后附一段说明，每条一句；没有的项不写：

```
改动说明
- 删除：<删了什么>（<原因>）
- 移动：<什么从哪里挪到哪里>

待确认
- <原文的矛盾 / 缺少的比较对象 / 把握程度不明的结论 / 找不到解释的代号>
```

## 6. 交付前核对

对照两遍：从原稿出发，找有没有漏掉的事实或限定；从终稿出发，找有没有凭空多出的判断。再检查数字、标识符、引语和链接，最后把最绕的那段念一遍。

不用字数、禁词命中数、检测器或模型自评分证明质量。

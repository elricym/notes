---
layout: default
title: Addy Osmani：Agent 替你干活时，怎么保住批判性思维
date: 2026-11-03
category: notes
---

**来源：**Addy Osmani（[@addyosmani](https://x.com/addyosmani)，Claude Code @ Anthropic）X Article《[Critical thinking when agents do the work](https://x.com/addyosmani/status/2117512471930167377)》，2026-11-03 发布（北京时间约 15:01）。同主题相关文章见文末链接。

## 一段话总结

Agent 用得越顺，输出越像样，越容易把批判性思维外包掉。作者不反对 agentic 工作流，而是提醒：默认情况下没有什么会逼你再想一遍。他把状态写成光谱——**认知卸载**（委托但仍负责）→ **推迟判断**（工具输出变成你的新输入）→ **认知投降**（输出悄悄变成你自己的观点）。关键不只是审代码，而是事先有假设、用可验证的证据定义「做完了」、看 agent 替你做了哪些决策，并对愿意署名的标准坚持。模型再强，**问责不能交给 agent**。

## 光谱：卸载 → 推迟 → 投降

- **认知卸载（cognitive offloading）**：把活交给 AI，但结果的所有权还在你手里。作者整天这么干，也建议这么干。
- **推迟判断（deferral）**：工具输出不再是假设，而直接成为下一步输入。
- **认知投降（cognitive surrender）**：Wharton 的 Steven Shaw 与 Gideon Nave 提出的概念。信任或懒散一点点涨，你会「上次读得很仔细 → 这次扫一眼 → 再下一次只看骨架 → 被人问到某行却说不清」。
- 投降很少被当场看见。代码库干净、测试全绿；直到要改系统时才发现没人懂它了——这就是 **comprehension debt**（Jeremy Twei）和团队里共享系统理论被掏空（Margaret-Anne Storey 写过类似的 cognitive debt）。

## 低 stakes 可以全权委托；高 stakes 留下推理

- 作者举例：录课选酒店，三家评分差不多，没时间刷评论，就让 AI 定——便宜错了无所谓。
- 不会这么做的：怎么投钱、怎么给孩子职业建议、在工作里「该做什么、改动影响谁、能不能上线」。
- **拿不准时的分界：**你连借助 agent 都解释不了答案时，所有权已经交出去了。

## 他现在问自己的问题

旧清单是「对的问题吗、对的解法吗、有证据吗、算做完了吗」。Agent 时代的新版：

1. **问之前有没有先立假设？** 哪怕是坏猜测也好。读完一篇写得好的回答后，很难再想象别的可能。完全没方向时，可让模型做 Thariq Shihipar 说的 **blind spot pass**：把已知给它，让它找未知的未知。
2. **是在请它帮你想，还是在把想外包掉？** 两者都行，但你要知道自己在干哪一种。
3. **怎样才会错？** 然后去验证。模型自评置信度，远不如一个你能跑的测试。
4. **有没有从另一个角度听过反方？** 立场硬、问题开放时，让多个模型站对立面再自己收束。
5. **愿不愿意在维护者面前为这个答案下注？** 这是可问责的底线。
6. **自己已经不再练习什么？** 放过一些日常调试可以，但要刻意。

## 验证要变成习惯，也能被投降

- 瓶颈已经从「写代码」挪到「确认你是对的」。给 agent 可运行的验证手段（E2E、属性测试、真机操作），它可以改 → 测 → 读输出 → 再试，在你看之前就多轮迭代。Boris Cherny 的说法：**给 Claude 一条验证自己工作的路径**。
- 也可以投降在验证上：「有证据吗」变成「绿灯了吗」。Agent 写测试很便宜，绿很多，但测试可能和实现犯同一个错；绿灯只覆盖一个属性。
- **对每个绿灯：写清它检查了什么，再写清它没检查什么。**
- 事先定义「verified」：测试通过、截图、日志或 trace——可核对的事实，而不是「看起来做完了」。收到完成通知时，**先看它跑了什么命令和输出，再看摘要**。
- 值得固定进循环的：用新上下文的子 agent 自审；结束时仍问「我漏了什么？」——复杂功能做完后常常还能再挖出两三件。
- Claude Code 团队审查经验里的经验法则：**如果你说不出检查会漏什么，就不要快速批准，要真审。** 合成五十通客户访谈或竞品分析时，抽查几份原文；依赖某个数字时，核对计算。

## 真的看生成出来的东西

- 600 行 PR：扫结构、变量名像样、测试绿 → 批准。中间可能有事务边界顺序微调、你没想到的默认值翻转。
- 写代码和审代码是不同技能；审到某一点就变成盖章。把 diff 当人写的来读，再看 agent **替你做了哪些决策**（默认值、范围外什么、两条需求冲突时它选了哪边）。摘要不会写这些。
- 让它列出决策和假设，再抽几行自问；长文档合上后凭记忆复述主论点。有人让 Claude 写变更报告并在文末出测验——**答对才合并**。
- **编排税（orchestration tax）**：agent 产出速度和你愿意署名之间的缺口。堆得比你审得快时，再开一个 session 没用——要么收紧检查让更少东西需要你，要么放慢。产出超过你能站台的量时，你已经不是在审，是在赌。

## 质量取决于输入；意图债只能你还

- 人的心力从「中间过程」挪到了**前端任务描述**和**后端审输出**。含糊请求过去会被人顶回来；agent 往往会补全空白，交回一个「看起来做完」但想法仍糊的东西——这就是 **intent debt**（隐含目标、约束、理由）。别人还不了这笔债。
- 自己的 prompt 反映你对问题的理解。先用自己的话写 brief：受众、不做范围、完成定义。第二轮改还不顺，停手重写 prompt，而不是继续拧螺丝。
- Andy Clark 区分 **委托** 与 **协作**：协作是互相放大——prompt 打磨输出，再打磨下一次 prompt 和心智模型。不清楚时，让 agent 采访你；结束时自己的模型变清楚了，才算成功。
- 小心链式摘要：第三个 agent 可能从没读过原文。
- 自己定输出标准：格式漂亮、语气自信已经不是质量信号。不愿意署名的就不发出去；未达标的原因写进共享配置、hook 或测试，让品味可累积。

## 「反正模型很快会比我强」

- 检测可以越来越多交给 agent；但**最终有人对上线负责**。信多少本身是判断，校准靠持续看它错在哪——错法一直在变。
- Anthropic 内部研究点出的陷阱：**监督悖论**——监督 Claude 需要的编码技能，恰恰可能因过度依赖 AI 而萎缩。
- 更好模型解不了的仍是：做什么、为什么值得、影响谁、愿意牺牲什么。可以一起想，但答案仍是你的。**可以卸掉执行和大量审计，卸不掉问责。**

## 日常可插拔的做法

- 每周亲手写一点代码，或做一件「忘了会很惨」的真事（校准练习，不是道德课）。
- 每月列一遍已经停做的事，决定哪些可以继续停。
- 老问题仍有效：**如果 AI 不存在，你会有多迷路？**
- 遇到不懂的表述，不要只搜一行释义就塞进文里——花一点力气搞懂它落在哪。
- 认真检查机器是真工作，要排进日程，否则团队不会做。

## 带走什么

- **刻意：**quiz、访谈、证据链都要你设好。
- **诚实看光谱位置：**连 agent 帮忙都解释不了，就是投降了。
- **先有假设**，再问。
- **绿灯只代表一件事**——它查了什么、没查什么。
- **先看证据**（命令与输出），再看摘要。
- **找它替你做的决策。**
- **写好 prompt = 想清楚问题。**
- **设门槛并守住：**不愿署名就不发出去。
- 一个可立刻用的动作：问之前写下你以为会发生什么；结束后写下它没检查的一件事——看这会不会改变你读输出的方式。

## 相关链接

- 原文：[Critical thinking when agents do the work](https://x.com/addyosmani/status/2117512471930167377)
- [Cognitive surrender（Addy）](https://addyosmani.com/blog/cognitive-surrender/)
- [Comprehension debt](https://addyosmani.com/blog/comprehension-debt/)
- [Intent debt](https://addyosmani.com/blog/intent-debt/)
- [Orchestration tax](https://addyosmani.com/blog/orchestration-tax/)
- [Agentic verification（Substack）](https://addyo.substack.com/p/agentic-verification)
- [The 80% problem in agentic coding](https://addyo.substack.com/p/the-80-problem-in-agentic-coding)
- [Avoiding skill atrophy](https://addyo.substack.com/p/avoiding-skill-atrophy-in-the-age)
- [Code review in the age of AI](https://addyo.substack.com/p/code-review-in-the-age-of-ai)
- Anthropic：[How AI is transforming work at Anthropic](https://www.anthropic.com/research/how-ai-is-transforming-work-at-anthropic)
- Claude Code 团队：[Solving code review at Anthropic](https://claude.dev/blog/solving-code-review-at-anthropic/)

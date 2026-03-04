1. Shift + Tab 两次，开启计划模式，总结计划模式的使用方式和为什么使用计划模式
2. https://code.claude.com/docs/en/how-claude-code-works 总结这个文档
3. https://code.claude.com/docs/en/features-overview#understand-context-costs总结这个文档当中的
Understand context costs 添加img\context-loading.svg图片作为参考
4. https://code.claude.com/docs/en/costs#reduce-token-usage总结这个文档当中的Reduce token usage
/clear 清楚当前的上下文
/rename [name] 对当前的上下文重命名，后续可以找回
/resume 找回之前重命名的上下文
/compact <optional custom summarization instructions>压缩上下文
5. https://code.claude.com/docs/zh-CN/best-practices 帮我总结这个文档的要点，尤其是如何高效使用Claude Code，比如文中提到的避免常见失败模式；有时你_应该_让上下文累积，因为你深入一个复杂的问题，历史很有价值。有时你应该跳过规划，让 Claude 想出来，因为任务是探索性的。有时模糊的提示正是你想要的，因为你想看看 Claude 如何解释问题，然后再限制它。
注意什么有效。当 Claude 产生很好的输出时，注意你做了什么：提示结构、你提供的上下文、你所在的模式。当 Claude 遇到困难时，问为什么。上下文太嘈杂了吗？提示太模糊了吗？任务对于一次通过来说太大了吗？
随着时间的推移，你会培养没有指南能捕捉的直觉。你会知道何时具体，何时开放，何时规划，何时探索，何时清除上下文，何时让它累积。
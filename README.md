# ECR Arena — 判定擂台

[**Commercial verification engagements — USD 8,000–15,000, court-ready dossier**](https://dshcorrectover.github.io/correctover-recovery-admission/services.html) · [**Independent audit & conformance**](https://dshcorrectover.github.io/correctover-recovery-admission/services.html)

> **Independent verdicts for recovery decisions. 报告可独立重放，重放不出来退款。**

Our verdicts do not depend on any implementation — including our own.
我们的判定不依赖任何实现，包括我们自己的。

## What this is

一个公开的判定擂台：任何 agent 运行时实现提交自己的 recovery 决策记录，我们两周内交付一份只关于你的判定报告——8 个 reason class 落点 + 结构盲区声明 + cannot-tell 条目，附可独立重放的证据包。

- 提交方式与流程：[SUBMIT.md](SUBMIT.md)
- 规则六条：[ARENA-RULES.md](ARENA-RULES.md)
- 完整版定价：[PRICING.md](PRICING.md)
- 样例报告（我们拿自己的 legacy engine 真跑的，脱敏版）：[samples/first-report.md](samples/first-report.md)

## Status

**awaiting first external submission**

样例报告已就位（真跑，非手写演示）。第一份外部报告空缺中——我们不上自己的擂占位。

## Rules that matter

1. 报告结构固定：8 class 落点 + 盲区 + cannot-tell，缺一不交付
2. 判定可独立重放；重放不出来，报告作废
3. 负结果同权重署名，refutation 更醒目
4. 公开需被测方签字
5. **不改标准适配你。**

## 对应套件

- 8 reason class 定义与 8 锚作者集：[correctover-recovery-admission](https://github.com/DSHCorrectover/correctover-recovery-admission)（ECR 原件 `ecr/d1-original/`，独立 checker + 公开向量）
- 提交不要求暴露业务数据：向量级脱敏，digest 对 digest。

---

*ECR Arena is operated by Correctover. Contact: wangguigui@correctover.com*

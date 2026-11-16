# Arena Sample Verdict Report — ECR-AR-0000

**被测实现**：legacy engine.js（correctover-recovery-admission @ `legacy-context/`，公共仓在案，作者系 Correctover 自身——按 ARENA-RULES 第 2 条，我们第一个判的是自己）
**判定套件**：`ecr/d1-original/recovery-receipt.mjs` + `verify-recovery.py` + `recovery-vectors-v1.json`（8 锚作者集）
**报告日期**：2026-11-16
**性质**：样例报告（Arena 首报格式示范）。真跑产出，非手写演示。不可作为商业判定报告引用。

---

## A. 8 个 reason class 逐项落点

| # | Class | 落点 | 证据行（实跑） |
|---|---|---|---|
| 1 | recovery-replay | OUT_OF_SCOPE | `replay same failure → OUT_OF_SCOPE / recovery-replay`（digest-only pipeline 此项判 IN_SCOPE——见 B-1） |
| 2 | param-widening | OUT_OF_SCOPE | `retry with widened amount → OUT_OF_SCOPE / param-widening` |
| 3 | capability-downgrade | OUT_OF_SCOPE | `downgrade model → OUT_OF_SCOPE / capability-downgrade` |
| 4 | execution-set-change | OUT_OF_SCOPE | `skip one provider → OUT_OF_SCOPE / execution-set-change` |
| 5 | subject-drift | OUT_OF_SCOPE | `failover to provider-B → OUT_OF_SCOPE / subject-drift` |
| 6 | unapproved-path | OUT_OF_SCOPE | `flywheel learned path → OUT_OF_SCOPE / unapproved-path` |
| 7 | unresolved-failure-ref | OUT_OF_SCOPE | `unresolved failure ref → OUT_OF_SCOPE / unresolved-failure-ref` |
| 8 | authority-unchanged | IN_SCOPE | 8/8 reason codes exercised；唯一合规通过路径 |

**链级结论**：8/8 receipts verify（sig + chain + hash）；篡改测试 tamper=REJECTED；`7 of 8 recoveries are OUT_OF_SCOPE` + `8/8 reason codes exercised` 两行自证无吞项。

## B. 结构盲区声明（该实现/该套件结构上判不出来的项）

1. **digest-only pipeline 判不出 recovery-replay**。replay 是 chain-aware 判定：必须沿链回看 `prior_failed_decision_hashes`。任何只看单条记录 digest 的验证器（含本套件的 digest-only 对照列）在此项必然误放行。这不是实现的 bug，是记录结构的上限——被测实现若只存 digest，我们如实报告这一上限。
2. **第 0 步（unresolved-failure-ref）与第 1 步（replay）共用 `failed_decision_hash` 字段**。变异实验（`failed_decision.args_digest` 改为等于 `recovery.failed_decision_hash`，即向"不该触发第 0 步"的方向翻）实测使 suite 从 8/8 翻到 7/8、binding-alone 从 7/8 掉到 6/8——两步判定在该字段上是耦合的，单字段修复建议必须同时覆盖两步。

## C. cannot-tell 条目

1. **并发 replay 不可判**。套件向量模型为单链 attempt 序列；两个并发执行体对同一 `failed_decision_hash` 同时发起 recovery，现有记录结构无墙钟/序号信息——cannot-tell。此项需实现侧补充时间戳或序号字段后重测。
2. **非 ASCII preimage 的 JCS 字节级一致性**：本套件的 canonicalization 精确性仅对 ASCII-only preimage 成立（sorted keys, no whitespace, minimal escaping）。含非 ASCII 的真实业务参数，digest 对 digest 不可判——cannot-tell。Byte-level RFC 8785 conformance 属于 JCS comparison-semantics 范畴，超出本套件。

## D. 可重放证据包

- 环境：全新 clone `DSHCorrectover/correctover-recovery-admission` 分支 `coze-handover`（commit daf5eb0），进 `ecr/d1-original/` 目录
- 复现命令：`python3 verify-recovery.py` → `8/8 verdicts agree` + `7 of 8 anchors ... recovery binding alone`；`node recovery-receipt.mjs` → `8/8 reason codes exercised`
- 变异/复原向量与三层证据链：见交接 commit message 与本仓对拍台账（daily-brief.log 2026-11-16 23:25 条目）

## E. 判定者声明

本报告由 Correctover 出具，被测实现为 Correctover 自有 legacy engine——按 ARENA-RULES 第 4 条与第 2 条，我们第一个判的是自己，并且把盲区和 cannot-tell 原样写进公开报告。这是一份格式样例：证明这套判定不靠嘴，靠可重放的数字。

*Correctover — verdicts you can replay.*

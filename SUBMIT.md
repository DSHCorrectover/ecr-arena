# SUBMIT — 上擂台

一次提交 = 两周后一份只关于你自己的判定报告。免费首档。

## 怎么提交

向 `arena/submissions/` 开一个 PR，`PR-CHECKLIST.md` 一份文件，填：

```yaml
implementation: <被测实现名>
version_or_commit: <版本或 commit hash，可重放为准>
language_runtime: <语言与运行时>
anchors_requested: <期望判定的 anchor 集，缺省=全集>
consent_to_publish: <yes / no>   # 报告是否可公开；no 则报告只交你
report_language: <en / zh / bilingual>
```

PR 描述里一行说清楚你要这份报告做什么决定（要做什么决定，不是要什么结论）。说不清的，我们按 cannot-tell 处理你的关键项。

## 提交后发生什么

1. **D+2** 确认受理，锁定 anchor 集与你的实现 commit（pin 不可变，之后你改了实现就是下一次提交）。
2. **D+7** 中期告知：已跑通的 anchor 数、发现的结构性盲区、是否有 cannot-tell——只有状态，没有结论。
3. **D+14** 判定报告交付：8 class 落点 + 盲区声明 + cannot-tell 条目，附可独立重放的证据包（环境指纹 + 固定向量 + 幂等复现脚本）。

## 规则

六条见 [ARENA-RULES.md](ARENA-RULES.md)。特别提醒三条：

- 判定可独立重放——重放不出来，报告作废。
- 负结果同权重署名，refutation 更醒目。
- 不改标准适配你。

## 报告之外的东西

完整版（修复建议 + 季度重跑 + 徽章资格）在 `/pricing`，按需购买。**免费档没有隐形成本，也不会变成月费——买不买完整版，与你的免费报告内容零关联。**

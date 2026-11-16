# PR-CHECKLIST — 上擂提交表单

向 `submissions/` 开 PR，文件名 `verdict-request-<实现名>-<YYYYMMDD>.md`，内容：

```yaml
implementation: <被测实现名>
version_or_commit: <版本或 commit hash，可重放为准>
language_runtime: <语言与运行时>
anchors_requested: <期望判定的 anchor 集，缺省=全集>
consent_to_publish: <yes / no>   # no 则报告只交你
report_language: <en / zh / bilingual>
decision_to_make: <一行：这份报告要帮你做什么决定>
```

- 说不清 decision_to_make 的，关键项按 cannot-tell 处理
- 受理锁定：D+2 确认 + pin commit；D+7 中期告知；D+14 交付
- 规则六条见 [../ARENA-RULES.md](../ARENA-RULES.md)

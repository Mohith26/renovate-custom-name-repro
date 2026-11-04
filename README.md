# Named custom managers (`customName`) reproduction

Minimal repository for https://github.com/renovatebot/renovate/issues/21760.

It has two regex custom managers, named `versions` and `tools`. The package rules disable only the `tools` manager with `matchManagers: ["custom.regex.tools"]`, while `custom.regex` still matches both.

Run against a Renovate checkout that includes the `customName` change:

```sh
LOG_LEVEL=debug node <renovate>/lib/renovate.ts --platform=local --dry-run=lookup --onboarding=false
```

Expected result:

- `Matched 1 file(s) for manager regex (versions)` and `Matched 1 file(s) for manager regex (tools)` in the debug log
- `versions.txt`: lodash and express get updates
- `tools.txt`: react is skipped with `skipReason: disabled`

<p align="center">
  <img src="logo.png" alt="StagedSec" width="140">
</p>

<h1 align="center">StagedSec</h1>

<p align="center"><strong>Catch hardcoded secrets before they leave your machine.</strong></p>

<p align="center">
  A local-first secret scanner for your terminal, your editor and your AI coding agent.<br>
  No account. No telemetry. No code sent anywhere. MIT licensed.
</p>

<p align="center">
  <a href="https://gitlab.com/stagedsec/stagedsec">Source code</a> &nbsp;·&nbsp;
  <a href="https://gitlab.com/stagedsec/stagedsec#readme">Documentation</a> &nbsp;·&nbsp;
  <a href="https://gitlab.com/stagedsec/stagedsec/-/releases">Releases</a> &nbsp;·&nbsp;
  <a href="https://gitlab.com/stagedsec/stagedsec/-/issues">Report a bug</a>
</p>

<!-- When the website is live, add its link to the line above. -->

---

> **This GitHub repository is a pointer.** The code, releases and issue tracker live on **[GitLab](https://gitlab.com/stagedsec/stagedsec)**.

## Why

A leaked key is cheapest to deal with before it reaches a commit. After a push you have to rotate it, audit for misuse and rewrite history. StagedSec checks at the three places a secret first appears:

| Where | What happens |
|---|---|
| **Terminal and commit** | `stagedsec scan` and a pre-commit hook that checks exactly what is *staged*. A secret, or a file it cannot read, blocks the commit. |
| **Editor** | A VS Code extension underlines secrets as you type. Hover to see why and how to rotate the key. It never rewrites your code. |
| **AI agent** | An MCP server gives Claude Code, Cursor and other agents a `check_for_secrets` tool to call *before* they write a file. Findings come back masked. |

It can also scan a whole tree or **every commit in your git history**, and write JSON or SARIF for code-scanning dashboards.

## Try it

```bash
git clone https://gitlab.com/stagedsec/stagedsec.git
cd stagedsec && go build -o stagedsec .

cd /path/to/your-repo
/path/to/stagedsec init       # installs the pre-commit hook
/path/to/stagedsec scan .     # scan the working tree now
```

Needs Go 1.22 or newer. Prebuilt binaries will be on the [releases page](https://gitlab.com/stagedsec/stagedsec/-/releases).

## Honest about its limits

StagedSec is regex-based with about 60 rules. gitleaks has about 220 and detects more kinds of secrets, so run StagedSec alongside gitleaks or TruffleHog rather than instead of them. The [benchmarks](https://gitlab.com/stagedsec/stagedsec/-/tree/main/bench) are public, including the ones where it loses. Bug reports and missing-rule requests are the most useful thing you can send.

## Teams

Interested in a dashboard, central rule management, or help rolling StagedSec out across many repositories? Those are not built yet; email **stagedsec@proton.me** with your team size and what you need, and it will shape what gets built.

---

MIT licensed.

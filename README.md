I spent fourteen years customer-facing at security vendors, most of it explaining why a control
did not fire until after it had already not fired. Now I build controls that refuse the action.

### Enforcement at the call site

Telling an agent not to do something works most of the time. "Most" is the problem, and the
failures are not the ones you would guess. They come from an agent trying to be careful, defeated
by the shape of the command:

- A classifier reads `find . -name '*.py'` and allows it, so it allows `find . -name '*.py' -delete`.
- A caller writes `check ... ; do-the-work`. The check refuses and returns 1. The `;` runs the work.
- A classifier splits on whitespace, so `ls\nrm -rf ~` reads as `ls` and gets approved.

A permission rule matches a prefix. It cannot express "`find`, but only when it carries `-delete`."
So I stopped writing rules and started writing hooks that read the command and refuse it.

**[AB.Agentic Runtime Guardrails](https://github.com/andreybuilt/agent-guardrails)** is six of them, MIT.
The adversarial battery runs in under a minute on your machine, and in CI on every push:

```
python3 hooks/bash-approver.py --selftest
```

108 cases, zero wrong-allow. The README also lists the bypasses still open, and the ones two
adversarial reviews closed. One of those reviews found nine wrong-allows in the classifier, three
of which ran arbitrary code, which is why the case count moved. A guard tightened this far will
over-block sometimes, and you should know which way it fails before you install it.

### What I run it on

A homelab I operate as production: three hypervisors carrying 38 VMs and containers (34 running,
counted 2026-09-07), and 17 MCP servers split by blast radius so no server can read another's
secrets. The count is dated because it moves; `andreybuilt.ai` carries its own figure with its own
date, and neither is wrong. Self-hosted inference for work that cannot leave the perimeter, and a multi-model evaluation
cascade I run daily. The hooks exist because I kept finding new ways for an agent to hurt that
fleet.

### Currently

Looking for a technical field role at a security or AI infrastructure company: solutions
engineering, technical account management, or forward-deployed work. Seattle, and I travel.

`andreybuilt.ai`

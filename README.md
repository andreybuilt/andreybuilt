# Andrey

I build security controls for AI agents: guardrails that stop unsafe actions before they run,
published with their failure modes and the tests that prove both.

I spent fourteen years customer-facing at security vendors, most of it explaining why a control
did not fire until after it had already not fired. Now I build controls that refuse the action.

**Currently:** looking for a technical field role at a security or AI infrastructure company:
solutions engineering, technical account management, or forward-deployed work.

## Featured work

| Project | What it demonstrates | Evidence |
|---|---|---|
| **[AB.Agentic Runtime Guardrails](https://github.com/andreybuilt/agent-guardrails)** | Hooks that stop a coding agent's unsafe actions before they execute | Six hooks, a 108-case adversarial battery with zero wrong-allow, 40,837 logged production decisions, CI on every push |
| **[AB.Agentic Security Skills](https://github.com/andreybuilt/security-skills)** | Security review of code, and a pre-install audit of the instruction files an agent trusts | Two skills, a zero-dependency scanner, 8 malicious fixtures paired with 8 benign ones, plant-then-remove tests |

## Proof at a glance

- Unsafe actions are refused before they execute, not explained afterwards.
- Dangerous cases are tested beside their harmless twins, so a fix cannot quietly become a new over-block.
- The bypasses still open are published with the controls.
- Two adversarial reviews attacked these hooks. One found nine wrong-allows in the classifier, three
  of which ran arbitrary code; all nine are closed and are now test cases.
- Production behaviour is measured before a number goes in a README.

## Enforcement at the call site

Telling an agent not to do something works most of the time. "Most" is the problem, and the
failures are not the ones you would guess. They come from an agent trying to be careful, defeated
by the shape of the command:

- A classifier reads `find . -name '*.py'` and allows it, so it allows `find . -name '*.py' -delete`.
- A caller writes `check ... ; do-the-work`. The check refuses and returns 1. The `;` runs the work.
- A classifier splits on whitespace, so `ls\nrm -rf ~` reads as `ls` and gets approved.

A permission rule matches a prefix. It cannot express "`find`, but only when it carries `-delete`."
So I stopped writing rules and started writing hooks that read the command and refuse it. A guard
tightened this far will over-block sometimes, and you should know which way it fails before you
install it.

## Systems I operate

A homelab I run as production: three hypervisors, tool servers split by blast radius so no server
can read another's secrets, self-hosted inference for work that cannot leave the perimeter, and a
multi-model evaluation cascade I run daily. The hooks exist because I kept finding new ways for an
agent to hurt that fleet. The public projects are the generalized versions.

## Background

Fourteen years in cybersecurity at Imperva and Cloudflare: technical account management, field
solutions engineering, and leading an enterprise solutions engineering team. I can go from
architecture to implementation, explain the operational consequence, and stay with a system after
launch.

## Contact

Seattle, and I travel. [andreybuilt.ai](https://andreybuilt.ai)

# Purple Team — Vulnerability Research & Detection

Personal research repository in offensive and defensive security: reproduction, exploitation and
detection of known vulnerabilities (CVEs), in a strictly authorized context (red team, purple
team, cyber range, educational demonstration).

> Author: [Xavier Rousseau](https://www.linkedin.com/in/xrousseau/) — 2026
> Usage: authorized use only — security demos, red team, authorized pentests.

---

## Methodology — Corridor AI

This repository isn't produced by a *harness* (a layer that corrects the model after the fact), but
by a **corridor**: a strict contract written by the expert before the first prompt, defining the
steps to follow, the evidence to produce, and the rules to respect. The model isn't guided along the
way — it can't improvise, it must comply with the contract. A single corridor covers the entire
business process behind this repository: vulnerability analysis, victim environment deployment,
weaponized exploit, network/system evidence, filmed demo.

"Corridor" is the concept describing this procedure — not a tool or a product. The
[CORRIDOR.en.md](CORRIDOR.en.md) file is a translation of the LinkedIn post published in June 2026
that lays it out in detail: updates and follow-up on [LinkedIn — Xavier Rousseau](https://www.linkedin.com/in/xrousseau/).

The corridor is a contract, not a technical integration: it doesn't depend on any particular model.
This repository was produced with Claude, but the same principle works identically with Qwen, Codex,
or any other model capable of following a written contract — that's precisely the point of this
approach compared to a harness built for one specific model.

---

## Repository contents

| Directory | Contents |
|---|---|
| [`vulnerabilities/`](vulnerabilities/) | One subdirectory per CVE: PoC, exploit, Docker environment, evidence, documentation |
| [`blueteam/`](blueteam/) | Defensive counterparts (Suricata rules, reference PCAPs, Sigma rules, system logs) |
| [`scripts/`](scripts/) | Cross-cutting tooling (GIF/demo HTML generation, pyte terminal rendering) |
| [`reversed/`](reversed/) | Analysis and reverse-engineering notes (patch Tuesday, protocols) |
| [`linkedin_post/`](linkedin_post/) | Demo GIFs published for communication |
| [`etc/`](etc/) | Project configuration (memory restoration, machine setup) |

The detailed working methodology (internal organization of a CVE directory, collection, audit and
validation procedure) is confidential and not publicly documented.

---

## Red team / blue team approach

This repository follows a **purple team** approach: every vulnerability exploited on the offensive
side has a matching counterpart on the defensive side.

**Red team side** ([`vulnerabilities/`](vulnerabilities/)): faithful reproduction of the
vulnerability in a dedicated Docker environment, development of a non-intrusive detection script
(with a Nuclei variant) and a complete exploit (with a Metasploit variant), functional audit, then
a filmed demonstration of the full attack chain.

**Blue team side** ([`blueteam/`](blueteam/)): for every vulnerability exploited, production of the
corresponding detection artifacts : Suricata rules (network IDS) validated against a real PCAP
capture, Sigma rules covering the observable phases in logs or traffic, and the associated system
logs.

This dual approach validates that a detection rule actually works against the attack it is meant to
catch, rather than being written in the abstract.

---

## Test environment

Docker containers and captures (PCAP, eBPF, auditd) are built and run on a dedicated test VM.

---

## Usage scope

This repository is intended exclusively for authorized use: security demonstrations, red/purple
team exercises, mandated penetration tests, training. No exploit should be used against a system
without the explicit authorization of its owner.

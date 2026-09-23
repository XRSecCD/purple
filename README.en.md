# Purple Team — Vulnerability Research & Detection

Personal research repository in offensive and defensive security: reproduction, exploitation and
detection of known vulnerabilities (CVEs), in a strictly authorized context (red team, purple
team, cyber range, educational demonstration).

> Author: Xavier Rousseau — 2026
> Usage: authorized use only — security demos, red team, authorized pentests.

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

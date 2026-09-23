# Purple Team — Recherche vulnérabilités & détection

Dépôt de recherche personnelle en sécurité offensive et défensive : reproduction, exploitation et
détection de vulnérabilités connues (CVE), dans un cadre strictement autorisé (red team, purple
team, cyber range, démonstration pédagogique).

> Auteur : Xavier Rousseau — 2026
> Usage : authorized use only — security demos, red team, authorized pentests.

---

## Contenu du dépôt

| Répertoire | Contenu |
|---|---|
| [`vulnerabilities/`](vulnerabilities/) | Un sous-répertoire par CVE : PoC, exploit, environnement Docker, preuves, documentation |
| [`blueteam/`](blueteam/) | Contreparties défensives (règles Suricata, PCAPs de référence, règles Sigma, logs systèmes) |
| [`scripts/`](scripts/) | Outillage transverse (génération GIF/demo HTML, rendu terminal pyte) |
| [`reversed/`](reversed/) | Notes d'analyse et de reverse (patch Tuesday, protocoles) |
| [`linkedin_post/`](linkedin_post/) | GIFs de démo publiés en communication |
| [`etc/`](etc/) | Configuration projet (restauration mémoire, setup machine) |


La méthodologie de travail détaillée (organisation interne d'un répertoire CVE, procédure de
collecte, d'audit et de validation) est confidentielle et n'est pas documentée publiquement.

---

## Approche red team / blue team

Ce dépôt suit une démarche **purple team** : chaque vulnérabilité exploitée côté offensif a sa
contrepartie côté défensif.

**Côté red team** ([`vulnerabilities/`](vulnerabilities/)) : reproduction fidèle de la
vulnérabilité dans un environnement Docker dédié, développement d'un script de détection non
intrusif (avec déclinaison pour Nuclei) et d'un exploit complet (avec déclinaison Metasploit), audit du fonctionnement, puis démonstration filmée de la chaîne d'attaque complète.

**Côté blue team** ([`blueteam/`](blueteam/)) : pour chaque vulnérabilité exploitée, production
des artefacts de détection correspondants : règles Suricata (IDS réseau) validées sur capture
PCAP réelle, règles Sigma couvrant les phases observables dans les logs ou le trafic, ainsi que les logs systèmes associés. 

Cette double approche permet de valider qu'une détection fonctionne réellement contre l'attaque
qu'elle est censée repérer, plutôt que de l'écrire dans l'abstrait.

---

## Environnement de test

Les containers Docker et les captures (PCAP, eBPF, auditd) sont construits et exécutés sur une VM
de test dédiée.

---

## Cadre d'utilisation

Ce dépôt est destiné exclusivement à des usages autorisés : démonstrations de sécurité, exercices
de red/purple team, tests d'intrusion mandatés, formation. Aucun exploit ne doit être utilisé contre
un système sans autorisation explicite du propriétaire.

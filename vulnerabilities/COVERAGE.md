# Coverage — Droits obtenus par exploit

> Dernière mise à jour : 2026-09-23 — 37 CVEs  
> Environnement de référence : 192.168.68.20 — Ubuntu 24.04, kernel 6.17

---

## Tableau de synthèse

| CVE | Nom | Composant | Vecteur | Type | Droits obtenus | Statut | PoC public⁵ | Doc⁶ |
|-----|-----|-----------|---------|------|----------------|--------|:---:|:---:|
| CVE-2018-25332 | GitBucket LFS | GitBucket 4.23.1 API LFS | Réseau, non authentifié | Auth Bypass | accès dépôts privés (LFS) | ✓ | ✅ | ✅ |
| CVE-2018-25334 | Zechat CSRF/XSS | Zechat 1.5 web | Réseau, non authentifié | CSRF via XSS | vol token session | ✓ | ✅ | ✅ |
| CVE-2018-25338 | Zechat SQLi union | Zechat 1.5 web | Réseau, non authentifié | SQLi union-based | dump DB complet | ✓ | ✅ | ✅ |
| CVE-2018-25339 | Zechat SQLi time | Zechat 1.5 web | Réseau, non authentifié | SQLi time-based | extraction aveugle DB | ✓ | ✅ | ✅ |
| CVE-2021-47952 | jsonpickle RCE | jsonpickle ≤ 2.0.0 | Réseau, non authentifié | RCE | `root` (dans container) | ✓ | ✅ | ✅ |
| CVE-2025-68613 | n8n ExprInj | n8n 1.120.3 Expression Sandbox | Réseau, authentifié¹ | RCE sandbox escape | `node` (process n8n) | ✓ | ✅ | ✅ |
| CVE-2026-2005 | pgcrypto RCE | PostgreSQL pgcrypto contrib | Réseau, authentifié DB | Heap OvF → RCE | `postgres` OS user | ✓ | ✅ | ✅ |
| CVE-2026-23918 | — | Apache httpd 2.4.66 `mod_http2` | Réseau, non authentifié | DoS + RCE | `daemon` (worker Apache) | DoS ✓ · RCE ✓ | ❌ | ✅ |
| CVE-2026-30893 | Wazuh Cluster RCE | Wazuh Manager 4.4.0 cluster | Réseau, accès port 1516 | Path Traversal → RCE | `wazuh` OS user | ✓ | ❌ | ✅ |
| CVE-2026-31431 | Copy Fail | Linux kernel `AF_ALG` (`authencesn`) | Local, non privilégié | LPE | `root` (uid=0) | ✓ | ✅ | ⚠️⁷ |
| CVE-2026-33032 | MCPwn | nginx-ui ≤ 2.3.5 (MCP endpoint) | Réseau, semi-authentifié² | RCE | `www-data` (PHP-FPM) | ✓ | ❌ | ✅ |
| CVE-2026-44364 | misp-modules CSRF | misp-modules v3.0.7 | Réseau, non authentifié | CSRF → SSRF | exécution module arbitraire | ✓ | ❌ | ✅ |
| CVE-2026-44381 | MISP SQLi | MISP web (ORDER BY) | Réseau, authentifié³ | SQLi time-based | dump DB + hashes | ✓ | ❌ | ✅ |
| CVE-2026-44789 | n8n pagination RCE | n8n 1.x paginationCompleteWhen | Réseau, authentifié¹ | RCE sandbox escape | `node` (process n8n) | ✓ | ❌ | ✅ |
| CVE-2026-44790 | n8n Git receivepack | n8n 1.x Git node addConfig | Réseau, authentifié¹ | RCE via git | `node` (process n8n) | ✓ | ❌ | ✅ |
| CVE-2026-44791 | n8n XML Pollution | n8n 1.x xml2js + deepCopy | Réseau, authentifié¹ | RCE prototype pollution | `node` (process n8n) | ✓ | ❌ | ✅ |
| CVE-2026-43500 | Dirty Frag | Linux kernel XFRM/ESP (`espintcp`) | Local, non privilégié | LPE | `root` (uid=0) | Demo ESP ✓ | ✅ | ⚠️⁷ |
| CVE-2026-46300 | Fragnesia | Linux kernel XFRM ESP-in-TCP | Local, non privilégié | LPE | `root` (uid=0) | LPE ✓ | ✅ | ⚠️⁷ |
| CVE-2026-46333 | ssh-keysign-pwn | Linux `ssh-keysign` FD race | Local, non privilégié | LPE | `root` (uid=0) via FD race | ✓ | ✅ | ✅ |
| CVE-2026-42945 | NGINX Rift | nginx 0.6.27–1.30.0 `ngx_http_rewrite_module` | Réseau, non authentifié | DoS + RCE | `nobody` (worker nginx) | ✓ | ✅ | ✅ |
| CVE-2026-6637 | refint SQLi+BOF | PostgreSQL refint contrib (`check_foreign_key`) | Réseau, authentifié DB | SQLi + Stack BOF | `postgres` superuser | ✓ | ❌ | ✅ |
| CVE-2026-9082 | drupal-sqli-pgsql | Drupal + PostgreSQL jsonapi | Réseau, non authentifié | SQLi boolean-blind | dump DB | ✓ | ⚠️⁸ | ✅ |
| CVE-2026-9256 | nginx-poolslip | nginx 0.1.17–1.31.0 ngx_http_rewrite | Réseau, non authentifié | DoS (Heap OOB) | worker crash (SIGABRT) | ✓ | ❌ | ✅ |
| CVE-2026-26980 | Ghost CMS SQLi | Ghost CMS 3.24.0–6.19.0 Content API | Réseau, non authentifié | SQLi blind ORDER BY | Admin API key + users + hashes | ✓ | ✅ | ✅ |
| CVE-2026-48095 | 7-Zip NTFS OvF | 7-Zip ≤ 26.00 `NtfsHandler.cpp` | Réseau (delivery fichier), non authentifié | Heap OvF → vtable hijack → RCE | user courant (contexte 7-Zip) | SIGSEGV ✓ · RCE (ASLR=off) ✓ | ❌ | ✅ |
| CVE-2025-67644 | langgraph-checkpoint-sqlite SQLi | langgraph-checkpoint-sqlite < 3.0.1 | Réseau, authentifié (user ordinaire) | SQLi → contournement isolation tenant | lecture checkpoints/secrets de tous les tenants | ✓ | ✅ | ✅ |
| CVE-2026-8206 | Kirki WP Account Takeover | Kirki (WordPress) ≤ 6.0.6 | Réseau, non authentifié | Auth Bypass (password reset hijack) | prise de contrôle compte WordPress (admin) | ✓ | ✅ | ✅ |
| CVE-2026-23111 | nf_tables UAF LPE ("Off By !") | Linux kernel `nf_tables` (`nft_map_catchall_activate`) | Local, non privilégié | Use-After-Free → LPE | `root` (uid=0) via `modprobe_path` hijack | ✓ | ⚠️⁹ | ✅ |
| CVE-2026-41283 | OpenStack Mistral Policy Bypass | OpenStack Mistral ≤ 22.0.0 | Réseau, authentifié (rôle bas) | Policy Bypass → RCE | exécution code sur worker Mistral + credentials OpenStack | ✓ | ❌ | ✅ |
| CVE-2026-42533 | NGINX map Heap BOF | nginx 0.9.6–1.31.2 (`map` + rewrite) | Réseau, non authentifié | Heap Buffer Overflow | DoS (crash worker) ✓ · RCE (write-what-where) ✓ | ❌ | ✅ |
| CVE-2026-44417 | Apache CXF JMS JNDI RCE (bypass) | Apache CXF < 3.6.11 (transport JMS) | Réseau, non authentifié | JNDI Injection (bypass fix incomplet CVE-2025-48913) | RCE process Apache CXF | ✓ | ❌ | ✅ |
| CVE-2026-44618 | Apache CXF WS-Transfer XXE | Apache CXF < 3.6.11 (ws-transfer) | Réseau, non authentifié | XXE | lecture fichiers locaux / SSRF | ✓ | ❌ | ✅ |
| CVE-2026-45447 | OpenSSL PKCS7_verify() Heap UAF | OpenSSL 1.1.1 < 1.1.1zh (+ branches 3.x) | Réseau, non authentifié | Heap UAF (double-free) | crash service (DoS) ✓ · RCE potentiel | ❌ | ✅ |
| CVE-2026-45505 | ActiveMQ Jolokia Bypass RCE | Apache ActiveMQ Classic < 5.19.7 | Réseau, authentifié⁴ | Bypass patch CVE-2026-34197 → RCE | RCE dans la JVM ActiveMQ | ✓ | ❌ | ✅ |
| CVE-2026-46243 | CIFSwitch cifs.spnego LPE | Linux kernel + cifs-utils (`cifs.upcall`) | Local, non privilégié | Key forgery (request_key) → LPE | `root` (uid=0) via NSS malveillante | ✓ | ✅ | ✅ |
| CVE-2026-49261 | MariaDB Galera wsrep_notify_cmd RCE | MariaDB Galera Cluster ≤ 10.11.17 | Réseau, non authentifié (port gcomm 4567) | Command Injection (`system()`) | `mysql` OS user (uid=999) | ✓ | ❌ | ✅ |
| CVE-2026-49975 | HTTP/2 Bomb (HPACK Cookie Crumb) | Apache httpd `mod_http2` ≤ 2.0.40 | Réseau, non authentifié | DoS — amplification mémoire O(N²) | crash workers Apache (OOM kill) | ✓ | ✅ | ✅ |

> ¹ n8n : authentification API key ou session UI — contournable si credential connue ou Burp intercept  
> ² CVE-2026-33032 : `node_secret` requis — obtenu en clair via CVE-2026-27944 (`/api/backup`) ou accès fichier  
> ³ CVE-2026-44381 : authentification MISP standard (user/admin) requise  
> ⁴ CVE-2026-45505 : credentials `admin:admin` par défaut requis (ActiveMQ Jolokia)  
> ⁵ **PoC public** : ✅ = PoC/exploit public fonctionnel identifié et utilisé comme base | ⚠️ = PoC public partiel/théorique | ❌ = aucun PoC public trouvé, exploit développé from scratch (source : `VULN_COVERAGE.md`, colonne PoC)  
> ⁶ **Doc** : ✅ = advisory officiel public trouvé et collecté (NVD / GHSA / bulletin vendor) dans `src/reports/` | ⚠️ = pas d'advisory officiel enregistré, seule une recherche/publication du découvreur original est référencée  
> ⁷ CVE-2026-31431 / CVE-2026-43500 / CVE-2026-46300 (famille « Dirty Frag ») : pas d'advisory CVE officiel retrouvé ; le mécanisme s'appuie sur des recherches publiques nommées (Qualys pour AF_ALG, V4bel/dirtyfrag, V12 Security / William Bowling) sans référence NVD/GHSA directe  
> ⁸ CVE-2026-9082 : PoC public (`ridhinva/CVE-2026-9082`) prouve l'injection mais sans extraction de données ni chaîne complète  
> ⁹ CVE-2026-23111 : PoC public partiel identifié, adapté et complété pour la chaîne LPE complète

---

## Détail par CVE

### CVE-2018-25332 — GitBucket 4.23.1 LFS Auth Bypass

- **Mécanisme** : API LFS sans vérification d'authentification sur endpoints batch/objects → accès upload/download non authentifié sur dépôts privés
- **Droits** : lecture/écriture dépôts LFS sans credentials
- **Fichiers** : `check_cve_2018_25332.py`, `exploit_cve_2018_25332.py`

---

### CVE-2018-25334 — Zechat 1.5 CSRF via XSS

- **Mécanisme** : token CSRF exposé en commentaire HTML → XSS réfléchi pour forger requêtes authentifiées → vol de session
- **Droits** : accès session victime (vol cookie/token)
- **Fichiers** : `check_cve_2018_25334.py`, `exploit_cve_2018_25334.py`

---

### CVE-2018-25338 — Zechat 1.5 SQLi union-based

- **Mécanisme** : paramètre non sanitisé → `UNION SELECT` MySQL, 12 colonnes, séparateur `||` et `0x0a`
- **Droits** : dump complet de la base de données (messages, users, hashes)
- **Fichiers** : `check_cve_2018_25338.py`, `exploit_cve_2018_25338.py`

---

### CVE-2018-25339 — Zechat 1.5 SQLi time-based

- **Mécanisme** : injection `1 AND sleep(2)#` → extraction aveugle bit-à-bit via timing (Δ=8s pour 4 lignes)
- **Droits** : dump DB (identique à 25338, chemin aveugle sans UNION)
- **Fichiers** : `check_cve_2018_25339.py`, `exploit_cve_2018_25339.py`

---

### CVE-2021-47952 — jsonpickle RCE py/repr

- **Mécanisme** : désérialisation `py/repr` → `eval()` Python arbitraire → exécution OS
- **Droits** : `root` dans le container jsonpickle-vuln:2.0.0
- **Fichiers** : `check_cve_2021_47952.py`, `exploit_cve_2021_47952.py`

---

### CVE-2025-68613 — n8n Expression Injection RCE

- **Mécanisme** : IIFE `this`-escape dans sandbox `vm` → accès `process.mainModule` → `child_process.execSync()`
- **Droits** : `node` user (process n8n) — exécution commandes OS arbitraires
- **Fichiers** : `check_cve_2025_68613.py`, `exploit_cve_2025_68613.py`

---

### CVE-2026-2005 — PostgreSQL pgcrypto Heap OvF → RCE

- **Mécanisme** : heap overflow dans `pgcrypto` → primitive écriture 3 paquets SET_VARSIZE → `COPY FROM PROGRAM` pour RCE
- **Droits** : `postgres` OS user — exécution commandes arbitraires
- **Fichiers** : `check_cve_2026_2005.py`, `exploit_cve_2026_2005.py`

---

### CVE-2026-23918 — Apache httpd 2.4.66 `mod_http2` Double-Free

- **Mécanisme** : double-free sur `h2_stream*` → `SIGABRT` worker ; heap spray fake `apr_cleanup_t` → `system()`
- **Droits** : worker Apache lancé en `daemon:daemon`
- **Escalade possible** : chaînable avec LPE kernel pour root
- **Fichiers** : `exploit_dos_cve_2026_23918.py`, `exploit_rce_cve_2026_23918.py`

---

### CVE-2026-30893 — Wazuh Cluster RCE

- **Mécanisme** : `decompress_files()` — `os.path.join()` bypass via filepath absolu → écriture arbitraire sur le FS du manager Wazuh ; mode config : injection cron `/etc/cron.d/`
- **Droits** : `wazuh` OS user ; root si cron accessible
- **Fichiers** : `check_cve_2026_30893.py`, `exploit_cve_2026_30893.py`

---

### CVE-2026-31431 — Copy Fail — Linux `AF_ALG` LPE

- **Mécanisme** : write 4 octets arbitraires dans le page cache via `AF_ALG` + `splice` → écrasement binaire SUID → `execve` → shell root
- **Prérequis** : shell local non-privilégié
- **Droits** : `root` (uid=0, gid=0) — immédiat, < 1 s
- **Fichiers** : `exploit_cve_2026_31431.py`, `exploit_cve_2026_31431_v2.py`

---

### CVE-2026-33032 — MCPwn — nginx-ui ≤ 2.3.5

- **Mécanisme** : bypass JWT via `?node_secret=` → écriture webshell PHP via `nginx_config_add` → FastCGI → RCE
- **Droits** : `www-data` (PHP-FPM) — exécution commandes arbitraires
- **Escalade possible** : chaînable avec CVE-2026-31431 ou CVE-2026-43500 / CVE-2026-46300
- **Fichiers** : `exploit_cve_2026_33032.py`

---

### CVE-2026-44364 — misp-modules CSRF

- **Mécanisme** : endpoint `/query` accepte POST `text/plain` sans CSRF token → déclenchement modules arbitraires depuis navigateur victime
- **Droits** : exécution de 154 modules misp-modules avec les permissions du service
- **Fichiers** : `check_cve_2026_44364.py`, `exploit_cve_2026_44364.py`

---

### CVE-2026-44381 — MISP SQLi

- **Mécanisme** : `ORDER BY SLEEP(N)` time-based via paramètre non filtré → extraction bit-à-bit avec `MID(expr FROM pos FOR 1)`
- **Droits** : dump DB (users, hashes, événements MISP)
- **Fichiers** : `check_cve_2026_44381.py`, `exploit_cve_2026_44381.py`

---

### CVE-2026-44789 — n8n pagination RCE

- **Mécanisme** : `paginationCompleteWhen='other'` + IIFE expression → sandbox escape → `child_process.execSync()`
- **Droits** : `node` user (process n8n)
- **Fichiers** : `check_cve_2026_44789.py`, `exploit_cve_2026_44789.py`

---

### CVE-2026-44790 — n8n Git receivepack injection

- **Mécanisme** : `addConfig('core.receivepack', 'cat')` contourne la validation `targetRepository` → exécution commande git arbitraire
- **Droits** : `node` user (process n8n)
- **Fichiers** : `check_cve_2026_44790.py`, `exploit_cve_2026_44790.py`

---

### CVE-2026-44791 — n8n XML Prototype Pollution Bypass → RCE

- **Mécanisme** : `xml2js` + `deepCopy` → `__proto__.defineProperty` bypass sandbox → `$json.root[1].cmd` eval → RCE
- **Droits** : `node` user (process n8n)
- **Fichiers** : `check_cve_2026_44791.py`, `exploit_cve_2026_44791.py`

---

### CVE-2026-43500 — Dirty Frag — Linux XFRM/ESP LPE

- **Mécanisme** : user namespace + SA XFRM ESP-in-TCP → déchiffrement AES-GCM in-place sur page cache → écrasement binaire SUID → shell root
- **Prérequis** : shell local non-privilégié + user namespaces disponibles
- **Droits** : `root` (uid=0) — < 15 s (chemin SUID), 30 s–45 min (chemin `/etc/passwd`)
- **Fichiers** : `demo_esp_proof.py`, `exploit_43500.py`

---

### CVE-2026-46300 — Fragnesia — Linux XFRM ESP-in-TCP LPE

- **Mécanisme** : table nonce→keystream AES-GCM → write byte précis dans page cache → binaire SUID → root (déterministe, sans brute-force)
- **Prérequis** : shell local non-privilégié + user namespaces disponibles
- **Droits** : `root` (uid=0) — ~1-2s déterministe
- **Fichiers** : `exploit_46300.py`

---

### CVE-2026-46333 — ssh-keysign-pwn FD Race

- **Mécanisme** : `pidfd_getfd` race condition sur descripteur FD de `ssh-keysign` → accès fichiers privilégiés (shadow, clés SSH, host keys)
- **Droits** : lecture `/etc/shadow`, clés SSH root, clés hôtes — LPE indirect
- **Fichiers** : `check_cve_2026_46333.py`, `exploit_cve_2026_46333.py`

---

### CVE-2026-42945 — NGINX Rift — nginx Heap BOF

- **Mécanisme** : `is_args` non réinitialisé après `rewrite ?` → len-pass alloue N octets, copy-pass écrit 3N octets (`+` → `%2B`) → heap BOF → corruption `ngx_pool_cleanup_s` → `system()`
- **Droits** : `nobody` (worker nginx)
- **Escalade possible** : chaînable avec CVE-2026-31431 pour passer root
- **Fichiers** : `check_cve_2026_42945.py`, `exploit_cve_2026_42945.py`

---

### CVE-2026-6637 — PostgreSQL refint SQLi + Stack Overflow

- **Mécanisme** : `check_foreign_key` CASCADE construit SQL sans échappement → error-based SQLi via `::int` cast ; `strcat(sql, " where ")` après `snprintf` → stack OOB → SIGABRT
- **Droits** : `postgres` superuser (SECURITY DEFINER) → lecture `/etc/passwd`, dump `pg_authid`
- **Fichiers** : `check_cve_2026_6637.py`, `exploit_cve_2026_6637.py`

---

### CVE-2026-9082 — drupal-sqli-pgsql

- **Mécanisme** : injection dans clé de tableau `filter[xxx]` du endpoint `/jsonapi/node/page` → SQLi boolean-blind sur PostgreSQL
- **Droits** : dump DB Drupal (users, hashes, contenu)
- **Fichiers** : `check_cve_2026_9082.py`, `exploit_cve_2026_9082.py`

---

### CVE-2026-9256 — nginx-poolslip

- **Mécanisme** : captures PCRE chevauchantes + `redirect` → len-pass compte 1 fois l'escape `+`→`%2B`, copy-pass l'écrit 2 fois → heap OOB → `SIGABRT` worker (respawn immédiat)
- **Droits** : crash worker nginx — DoS répétable non authentifié
- **Fichiers** : `check_cve_2026_9256.py`, `exploit_cve_2026_9256.py`

---

### CVE-2026-26980 — Ghost CMS Content API Blind SQLi

- **Mécanisme** : `filter=slug:[...]` interpolé sans paramétrage dans ORDER BY `CASE WHEN` → blind SQLi unauthenticated via oracle overflow (`exp(710)` MySQL / `abs(-9223372036854775808)` SQLite)
- **Droits** : Admin API key (`id:secret`) → accès admin Ghost complet + dump users (email, bcrypt hash, nom)
- **Impact in-the-wild** : 700+ sites compromis (Harvard, Oxford), chaîne ClickFix/FakeCaptcha (Qianxin XLab, 2026-05-07)
- **Fichiers** : `check_cve_2026_26980.py`, `exploit_cve_2026_26980.py`

---

### CVE-2026-48095 — 7-Zip ≤ 26.00 NTFS Heap Buffer Overflow → RCE

- **Mécanisme** : `GetCuSize()` → UB shift `(UInt32)1 << (28+4)` = 1 → `_inBuf.Alloc(1)` alloue 1 octet → `ReadStream_FALSE` écrit 256 MB → vtable ptr `CInStream` écrasé à heap+304 avec données attaquant → SIGSEGV ou shellcode si ASLR désactivé
- **Vecteur** : fichier NTFS malveillant (`ClusterSizeLog=28`, `CompressionUnit=4`) livré par HTTP, email ou partage réseau — la victime ouvre l'archive avec 7-Zip
- **Droits** : user courant (contexte 7-Zip) — RCE arbitraire si ASLR désactivé ; SIGSEGV (DoS) systématique
- **Fichiers** : `check_cve_2026_48095.py`, `exploit_cve_2026_48095.py`

---

### CVE-2025-67644 — langgraph-checkpoint-sqlite SQLi

- **Mécanisme** : `_metadata_predicate()` interpole la clé du filtre de métadonnées directement dans un f-string SQL (`json_extract(..., '$.{query_key}')`) → injection via la clé (`x') = ? OR 1=1--`) → contournement du filtre d'isolation `user_id`
- **Droits** : lecture des checkpoints (et métadonnées sensibles : clés API, tokens, mots de passe) de tous les tenants
- **Fichiers** : `check_cve_2025_67644.py`, `exploit_cve_2025_67644.py`

---

### CVE-2026-8206 — Kirki WordPress Plugin ≤ 6.0.6 Account Takeover

- **Mécanisme** : endpoint REST `kirki-forgot-password` non authentifié accepte un email arbitraire fourni par l'attaquant à la place de celui du compte cible → lien de reset envoyé à l'attaquant
- **Droits** : prise de contrôle totale d'un compte WordPress (admin) sans authentification préalable
- **Fichiers** : `check_cve_2026_8206.py`, `exploit_cve_2026_8206.py`

---

### CVE-2026-23111 — Linux kernel 6.8 nf_tables UAF LPE ("Off By !")

- **Mécanisme** : opérateur `!` inversé dans `nft_map_catchall_activate()` → un élément catchall n'est pas réactivé lors d'un abort de transaction → `chain->use` décrémenté jusqu'à zéro → UAF sur `nft_chain` → spray `msg_msg` (80B → kmalloc-128) → écriture `modprobe_path` → `call_usermodehelper` → shell SUID root
- **Droits** : `root` (uid=0) — nécessite `nokaslr` (sans, leak via `seq_operations`)
- **Fichiers** : `exploit_cve_2026_23111.c`, `check_cve_2026_23111.py`

---

### CVE-2026-41283 — OpenStack Mistral ≤ 22.0.0 Policy Bypass → RCE

- **Mécanisme** : les endpoints `/v2/code_sources` et `/v2/dynamic_actions` n'appliquent pas la règle de politique `create_public_resource: role:admin` → un utilisateur avec un simple rôle `_member_` upload du code Python arbitraire, l'enregistre comme action publique et l'exécute sur le worker executor
- **Droits** : exécution de code sur le worker Mistral + exfiltration des credentials OpenStack (Keystone, PostgreSQL, RabbitMQ) présents dans l'environnement
- **Fichiers** : `check_cve_2026_41283.py`, `exploit_cve_2026_41283.py` (modes `exfil` / `revshell`)

---

### CVE-2026-42533 — NGINX map directive Heap Buffer Overflow

- **Mécanisme** : évaluation en deux passes des variables de script (`add_header`) — la passe taille sous-estime `$1` (captures non initialisées) tandis que la directive `map` met à jour `r->captures` entre-temps → la passe copie écrit 2N+1 octets dans un buffer de N+1 → heap BOF
- **Droits** : DoS (crash worker, SIGABRT glibc) systématique ; primitive d'écriture N octets contrôlés → RCE potentiel (write-what-where)
- **Fichiers** : `check_cve_2026_42533.py`, `exploit_cve_2026_42533.py` (modes `probe` / `dos`)

---

### CVE-2026-44417 — Apache CXF JMS JNDI RCE (bypass CVE-2025-48913)

- **Mécanisme** : le correctif de CVE-2025-48913 sécurise `JndiHelper.createInitialContext()` mais `AbstractMessageListenerContainer.createInitialContext()` instancie toujours `new InitialContext()` directement, sans validation d'URL → JNDI lookup vers un serveur attaquant
- **Droits** : RCE dans le process Apache CXF (JMS transport)
- **Fichiers** : `check_cve_2026_44417.py`, `exploit_cve_2026_44417.py`

---

### CVE-2026-44618 — Apache CXF WS-Transfer XXE

- **Mécanisme** : le parseur XML du module `cxf-rt-ws-transfer` ne désactive pas la résolution des entités externes (CWE-611) → `DOCTYPE` avec entité `SYSTEM` résolue et son contenu renvoyé dans la réponse SOAP
- **Droits** : lecture de fichiers locaux arbitraires / SSRF vers ressources internes
- **Fichiers** : `check_cve_2026_44618.py`, `exploit_cve_2026_44618.py`

---

### CVE-2026-45447 — OpenSSL PKCS7_verify() Heap Use-After-Free

- **Mécanisme** : un message PKCS7 SignedData avec `digestAlgorithms` encodé comme SET vide (`31 00`) provoque la libération prématurée du BIO `indata` par OpenSSL → double-free lorsque l'application appelle `BIO_free(indata)` à son tour
- **Droits** : crash du service (DoS) systématique ; corruption de tas exploitable en RCE selon le contexte applicatif
- **Fichiers** : `check_cve_2026_45447.py`, `exploit_cve_2026_45447.py` (modes `crash` / `check`)

---

### CVE-2026-45505 — Apache ActiveMQ Classic Jolokia Discovery Bypass RCE

- **Mécanisme** : contourne le correctif de CVE-2026-34197 (qui bloquait les URIs `static:(vm://...)`) via des wrappers de découverte sans parenthèses (`masterslave:vm://...`) → charge un `brokerConfig` Spring XML distant via `addNetworkConnector` → RCE
- **Droits** : RCE dans la JVM ActiveMQ (nécessite credentials Jolokia, `admin:admin` par défaut)
- **Fichiers** : `check_cve_2026_45505.py`, `exploit_cve_2026_45505.py` (modes `exploit` / `check` / `verify-patch`)

---

### CVE-2026-46243 — CIFSwitch — cifs.spnego Key Forgery LPE

- **Mécanisme** : absence de hook `.vet_description` sur le type de clé `cifs.spnego` → un utilisateur non privilégié forge une requête `request_key()` avec des champs arbitraires (pid, uid) → `cifs.upcall` (exécuté en root) entre dans le namespace de montage de l'attaquant avant `getpwuid()` → résolution NSS malveillante exécutée en root
- **Droits** : `root` (uid=0) via shell SUID posé par la lib NSS malveillante
- **Fichiers** : `check_cve_2026_46243.py`, `exploit_cve_2026_46243.py`

---

### CVE-2026-49261 — MariaDB Galera Cluster wsrep_notify_cmd RCE

- **Mécanisme** : `wsrep_notify_status()` passe le nom d'un nœud joiner (`wsrep_node_name`) sans échappement à `system()` → substitution de commande shell (`$(cmd)`) exécutée par la victime lors d'une transition d'état Galera
- **Droits** : `mysql` OS user (uid=999) — aucun accès authentifié à la base requis, seul le port gcomm (4567/TCP) doit être joignable
- **Fichiers** : `check_cve_2026_49261.py`, `exploit_cve_2026_49261.py` (modes `proof` / `shell`)

---

### CVE-2026-49975 — Apache httpd mod_http2 — HTTP/2 Bomb (HPACK Cookie Crumb)

- **Mécanisme** : bombe HPACK à références indexées — seed d'une entrée `cookie` dans la table dynamique puis envoi de milliers de références 1 octet ; chaque référence force la reconstruction de la chaîne de cookies fusionnée → allocation mémoire O(N²), combinée à un stall de flow control (`INITIAL_WINDOW_SIZE=0`)
- **Droits** : DoS — épuisement mémoire du container → OOM kill des workers Apache par le kernel
- **Fichiers** : `check_cve_2026_49975.py`, `exploit_cve_2026_49975.py`

---

## Chaînes d'exploitation

```
Réseau (sans accès initial)
  ├── CVE-2026-33032  → www-data
  │     └── + CVE-2026-31431 / CVE-2026-43500 / CVE-2026-46300  → root
  ├── CVE-2026-42945  → nobody (nginx)
  │     └── + CVE-2026-31431 / CVE-2026-43500 / CVE-2026-46300  → root
  ├── CVE-2026-2005   → postgres (OS)
  ├── CVE-2026-6637   → postgres superuser (DB + OS read)
  ├── CVE-2021-47952  → root (container)
  ├── CVE-2025-68613 / CVE-2026-44789 / CVE-2026-44790 / CVE-2026-44791  → node (n8n)
  ├── CVE-2026-9082 / CVE-2026-44381 / CVE-2018-25338 / CVE-2018-25339  → dump DB
  ├── CVE-2026-26980  → Admin API key Ghost (accès admin complet sans auth)
  ├── CVE-2026-48095  → RCE user courant (victime ouvre archive 7-Zip malveillante)
  ├── CVE-2025-67644  → lecture checkpoints/secrets tous tenants (SQLi isolation bypass)
  ├── CVE-2026-8206   → account takeover WordPress (password reset hijack)
  ├── CVE-2026-41283  → RCE worker Mistral + credentials OpenStack
  ├── CVE-2026-42533  → DoS nginx (RCE potentiel via write-what-where)
  ├── CVE-2026-44417 / CVE-2026-44618  → RCE / lecture fichiers (Apache CXF)
  ├── CVE-2026-45447  → DoS OpenSSL (RCE potentiel selon contexte applicatif)
  ├── CVE-2026-45505  → RCE JVM ActiveMQ (bypass CVE-2026-34197)
  └── CVE-2026-49261 / CVE-2026-49975  → RCE MariaDB (mysql) / DoS Apache (OOM)

Local (accès shell non-root déjà obtenu)
  ├── CVE-2026-31431  → root  (kernel AF_ALG)
  ├── CVE-2026-43500  → root  (kernel XFRM ESP)
  ├── CVE-2026-46300  → root  (kernel XFRM ESP-in-TCP, déterministe)
  ├── CVE-2026-46333  → shadow/SSH keys (FD race ssh-keysign)
  ├── CVE-2026-23111  → root  (kernel nf_tables UAF, nokaslr)
  └── CVE-2026-46243  → root  (cifs.spnego key forgery)
```

> CVE-2026-63030 (WordPress REST Batch Route Confusion → SQLi chaînée → pre-auth RCE) est en cours de traitement — non inclus ci-dessus tant que non finalisé.

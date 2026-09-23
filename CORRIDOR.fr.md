🔧 Corridor AI : le harness engineering oublie la moitié de l'équation.



Il y a 2 semaines, on se quittait sur un week-end prolongé plein de vulnérabilités à étudier. Et puis le week-end s'est transformé en nuits très courtes... mais productives.



Depuis quelque temps, tout le monde parle de “𝗛𝗮𝗿𝗻𝗲𝘀𝘀”: 

une couche d’exécution pour contrôler le modèle, gérer les outils, corriger les dérives et erreurs après exécution.



Mais un harness ne peut corriger que ce qu’on a déjà observé.

➡️ C’est de l'engineering de l'exécution.



🏗️ L’autre moitié du problème, c’est le 𝗦𝗰𝗮𝗳𝗳𝗼𝗹𝗱

C'est la structure comportementale du modèle :  

▫️ce qu’il voit,

▫️ce qu’il produit.



Aujourd’hui, l’industrie construit ce scaffold réactivement :

🔁 instruction après instruction,

🔁 correction après correction.



Cloudflare l’a poussé très loin avec Project Glasswing :

▫️ agents spécialisés,

▫️ pipelines complexes.



Mais il manque encore un concept.



📋 𝗖𝗼𝗿𝗿𝗶𝗱𝗼𝗿 𝗔𝗜 : le scaffold expert que personne n'écrit.

Le corridor ne remplace pas les agents. Il définit ce qu'ils doivent exécuter.



Le harness, c'est de l'engineering de l'exécution.

Le corridor, c'est celui de la conception.



🏭 Industrie → Agent = Modèle + Harness

🎯 Corridor → Résultat = Modèle + Expert scaffold



C'est un contrat strict établi par l'expert avant le 1er prompt :

→ étapes suivies

→ preuves produites

→ règles respectées



Le modèle n'est pas guidé. Il ne peut pas improviser. Il doit respecter le contrat.



⚠️ Conséquence directe :

- si le modèle viole le contrat, l'output est invalide.

- On ne juge plus la qualité du modèle mais on vérifie la 𝗰𝗼𝗻𝗳𝗼𝗿𝗺𝗶𝘁é.



Un seul corridor. Pour tout mon process métier :

🧪 analyse vulnérabilité 

🖥️ déploiement env victime 

💣 exploit weaponisé 

📡 preuves réseau/système 

🎥 démo/GIF



💥 Le temps d'écrire ce post, un 26e exploit sort du corridor (avec tous les artefacts): CVE-2026-45505, juste publié, sans PoC public



Je n'ai rien supervisé, juste dit :

➡️ “Traite le CVE-2026-45505”.



Les 26 GIFs sont en commentaires.  



🛠️ La stack, parce que la question va se poser.

▸ VS Code 

▸ Le plugin Claude Code par défaut 

▸ Un fichier .MD comme contrat 

▸ Claude Sonnet 4.6, pas de Mythos



Pas de CLAUDE.md / AGENTS.md / MCP / LangChain / Vector Store / etc..



⚡ Quand le modèle progresse,

le corridor s’exécute mieux sans modifier une ligne du contrat.

Le harness doit continuellement s’adapter aux dérives du modèle.

Le corridor profite des progrès du modèle.



🔬 Next Steps

tester le principe sur d’autres modèles (LLM/SLM/custom).



🔑 Un scaffold n’est bon qu’à la hauteur de l’expertise qui l’a rédigé.



L’IA n’amplifie pas les outils.

Elle amplifie l’expertise.



⚠️ Disclaimer

Les démonstrations publiées ici sont limitées à des preuves visuelles et comportementales pour des raisons d'éthique et de sécurité.



#AIEngineering #CyberSecurity #LLM #AISystems #AgenticAI #SecurityResearch #ScaffoldEngineering #OffensiveSecurity



📎 Sources : en commentaire
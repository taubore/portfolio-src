# AGENTS.md

## Mission

Ce dépôt contient le code source d’un site personnel technique francophone construit avec Hugo et le thème BlowFish, publié sur GitHub Pages.

L’agent peut proposer et appliquer des modifications locales dans le dépôt, mais toujours dans un esprit de **proposition révisable**. L’utilisateur garde le dernier mot avant tout commit ou push.

---

## Contexte technique

- Générateur statique : `Hugo`
- Thème : `BlowFish`
- Hébergement : `GitHub Pages`
- Dépôt de travail : dépôt source du site, jamais le dossier publié
- Approche de maintenance : simple, portable, durable
- Référence de contenu : privilégier d’abord les fichiers du dépôt eux-mêmes, puis les fichiers de référence du projet liés explicitement dans le dépôt ou dans le workspace

## Références externes

- Lorsqu’une composante est mentionnée pour la première fois dans le texte, ajouter un hyperlien vers sa référence si elle est connue et fiable.
- Dans une section de type BOM, tableau récapitulatif ou inventaire principal, mettre systématiquement les hyperliens sur les composantes importantes.
- Si la référence manque, insérer : `TODO - Ajouter hyperlien : <nom de la composante>`
- Ne pas multiplier les liens redondants inutilement dans les paragraphes courants.

---

## Priorités absolues

Lorsqu’il y a arbitrage, respecter cet ordre :

1. exactitude du contenu
2. clarté
3. maintenabilité
4. esthétique

Ne jamais sacrifier l’exactitude technique pour améliorer le style.

---

## Intention éditoriale

Devastator n’est pas présenté comme un produit fini, mais comme une plateforme d’apprentissage robotique construite pas à pas.

Les contenus doivent montrer :
- l’état réel du projet ;
- les décisions techniques prises ;
- les erreurs et corrections utiles ;
- les raisons concrètes derrière les choix matériels et logiciels ;
- ce qu’un lecteur débutant peut réutiliser pour son propre projet.

Le site doit être plus proche d’un carnet technique structuré que d’une vitrine marketing.

## Ligne éditoriale

Le site documente le projet Devastator comme un projet d’apprentissage technique réel, évolutif et imparfait.

Le ton doit rester :
- pédagogique ;
- concret ;
- structuré ;
- professionnel sans être prétentieux ;
- humble, avec place pour les essais, erreurs, limites et changements de direction.

Le contenu doit :
- aider un débutant motivé à comprendre les choix techniques ;
- montrer l’évolution réelle du projet dans le temps ;
- expliquer les compromis et contraintes concrètes ;
- privilégier la clarté technique plutôt que l’effet marketing ;
- rester synthétique, lisible et agréable à consulter.

À éviter :
- ton publicitaire ;
- superlatifs creux ;
- jargon inutile ;
- catalogue de composants sans mise en contexte ;
- réécriture qui gomme les hésitations, erreurs ou bifurcations utiles pédagogiquement.

Chaque page doit chercher un équilibre entre :
1. ce que le robot est aujourd’hui ;
2. comment il a évolué ;
3. ce qu’un lecteur peut apprendre de cette évolution.

Quand une composante est mentionnée pour la première fois, ajouter un hyperlien vers sa référence si disponible.  
Dans les tableaux récapitulatifs de type BOM, mettre systématiquement les hyperliens sur les composantes principales.  

Lorsqu’un lien ou une photo manque et serait utile, insérer un `TODO` explicite.

## Règles de rédaction

- Écrire en français.
- Utiliser des phrases claires et des paragraphes courts.
- Expliquer simplement les notions techniques.
- Mettre en avant les décisions, contraintes, tests et apprentissages.
- Préserver la cohérence entre la page principale du projet, l’historique et les notes techniques.
- Ne pas transformer une page de projet en documentation de câblage détaillée si ce n’est pas son rôle.
- Préférer une structure évolutive : une page principale stable et des sous-pages pour l’historique détaillé ou des sous-systèmes si nécessaire.

---

## Règles de modification

Privilégier, dans cet ordre :
1. contenu Markdown
2. configuration Hugo native
3. CSS léger et ciblé
4. shortcode simple seulement si nécessaire

Éviter :
- logique complexe dans `layouts/`
- dépendances fragiles
- personnalisations lourdes liées au thème
- refontes larges non demandées
- modifications simultanées de nombreux fichiers sans nécessité claire

Par défaut :
- modifier uniquement les fichiers nécessaires ;
- préserver la structure Hugo existante ;
- éviter toute refonte de l’arborescence sans bénéfice clair ;
- ne pas introduire de dépendance, shortcode, script ou pipeline complexe sans nécessité réelle.

Créer un nouveau fichier seulement si cela améliore clairement :
- la lisibilité ;
- la maintenabilité ;
- ou l’évolutivité éditoriale.

---

## Critères de qualité

Chaque modification doit viser :
- clarté ;
- cohérence ;
- fidélité technique ;
- lisibilité pour un humain ;
- évolutivité dans le temps.

En cas d’arbitrage, privilégier :
1. exactitude ;
2. pédagogie ;
3. simplicité ;
4. esthétique.

## Cohérence technique

Avant de modifier le contenu d’un projet, vérifier que la page reflète l’état réel actuel connu du projet.

En cas de doute :
- ne pas inventer
- ne pas reformuler agressivement
- signaler l’ambiguïté dans le résumé final

---

## Git et validation

Interdictions :
- ne jamais faire de `git commit`
- ne jamais faire de `git push`
- ne jamais créer ou fusionner de pull request
- ne jamais supprimer massivement des fichiers
- ne jamais réorganiser le dépôt sans demande explicite

Autorisé :
- modifier localement les fichiers demandés
- proposer des changements
- suggérer un nom de branche
- indiquer les commandes de vérification à lancer

Après chaque tâche, fournir un résumé bref :
1. fichiers modifiés
2. changements effectués
3. points ambigus ou à valider
4. vérifications recommandées

---

## Vérifications locales

Quand pertinent, privilégier des vérifications simples et non destructives, par exemple :

- `hugo server -D`
- `hugo`
- `git diff -- <fichier>`

Ne pas lancer de commandes destructives ni de nettoyage agressif sans demande explicite.

---

## Style de travail attendu

- travailler sur le plus petit périmètre utile
- ne pas élargir la tâche sans raison claire
- ne pas “améliorer” d’autres fichiers non demandés
- conserver le style global existant sauf si la tâche demande explicitement une harmonisation
- expliquer brièvement les choix effectués
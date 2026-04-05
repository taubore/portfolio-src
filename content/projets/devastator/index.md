+++
title = "Devastator"
weight = 10
description = "Robot mobile expérimental utilisé pour apprendre l'électronique, les capteurs et ROS 2."
summary = "Robot mobile expérimental basé sur un Raspberry Pi 4 B 4GB et un Raspberry Pi Pico WH."
date = 2026-01-14
tags = ["Robotique", "Raspberry Pi 4", "Raspberry Pi Pico WH", "DFRobot", "ROS 2", "Python"]
categories = ["Projets"]
status = "En cours"
+++

{{< figure
    src="devastator_thumbnail.jpg"
    alt="Robot mobile expérimental pour l’apprentissage de l’électronique et de ROS 2"
    width="50%"
>}}

## Résumé
Devastator est un robot mobile expérimental utilisé comme plateforme d'apprentissage en électronique, en intégration de capteurs, en Linux et en ROS 2. L'architecture actuelle de référence repose sur un Raspberry Pi 4 B 4GB comme ordinateur principal et un Raspberry Pi Pico WH comme microcontrôleur. Les essais antérieurs autour d'un Raspberry Pi 5, d'un Raspberry Pi 3B+ et d'un ESP32 restent utiles pour comprendre le cheminement du projet, mais ils doivent maintenant être lus comme de l'historique.

## Informations clés
- **Type de projet** : Robot mobile expérimental
- **Objectif principal** : Apprentissage de l’électronique, du Raspberry Pi, de Linux et de ROS 2
- **Architecture actuelle** : Raspberry Pi 4 B 4GB + Raspberry Pi Pico WH
- **Base mécanique** : Chenilles du kit [Devastator de DFRobot](https://www.dfrobot.com/product-1477.html)
- **Actionnement** : 2 moteurs DC 6 V [DFRobot avec encodeur en quadrature (FIT0521)](https://www.dfrobot.com/product-1617.html)
- **Alimentation de travail** : batterie NiMH 6 V pour les moteurs, pack de 6 piles NiMH pour la logique, carte d'alimentation maison sur perfboard
- **Système d'exploitation, langage et framework** : Linux, Python, ROS 2
- **État** : en cours d'intégration

## Description
Ce projet sert de base concrète pour faire évoluer un robot mobile autour de ROS 2, de Python et de plusieurs composants matériels réels. Le robot a été construit à partir du kit [Devastator de DFRobot](https://www.dfrobot.com/product-1477.html), dont les chenilles restent la base mécanique de la configuration actuelle.

L'intérêt du projet n'est pas seulement le résultat final, mais aussi les décisions techniques prises en cours de route. Le choix de l'ordinateur principal et du microcontrôleur a changé plusieurs fois en fonction de contraintes très concrètes : l'alimentation réellement disponible sur le robot, la robustesse de l'architecture électrique et le confort de développement à distance avec VSCode, ROS 2 et SSH.

## État actuel
Le projet reste en cours d'intégration matérielle et logicielle. L'architecture actuelle de référence est la suivante :

- Raspberry Pi 4 B 4GB pour le système principal, l'environnement Linux, ROS 2, le développement à distance et les traitements de plus haut niveau
- Raspberry Pi Pico WH pour les fonctions microcontrôleur, notamment autour des capteurs analogiques, de la commande moteur et du pilotage de servos
- Base mécanique reposant toujours sur les chenilles du kit Devastator et sur deux moteurs DFRobot 6 V avec encodeurs en quadrature
- Un [Seeed Studio Grove Ultrasonic Ranger V2.0](https://ca.robotshop.com/fr/products/ranger-ultrasons-seeedstudio-grove?qd=f9c678a38cdae18967ff3b7829970d27) monté sur un [servomoteur Hitec HS-422](https://ca.robotshop.com/fr/products/servomoteur-hs-422-hitec?qd=f2222dcfa0ee946af00eea88c179699a), prévu pour regarder devant, à gauche et à droite afin de détecter les obstacles et de permettre une conduite de base pour les éviter
- Un [kit de développement scanner laser 360 RPLIDAR A2](https://ca.robotshop.com/fr/products/kit-developpement-scanner-laser-360-rplidar-2?variant=42412104712343), prévu à plus long terme pour le positionnement du robot, mais pas encore intégré ni connecté

Les références au Raspberry Pi 5 et à l'ESP32 présentes dans les photos et notes plus anciennes correspondent à des étapes antérieures et non à l'architecture retenue aujourd'hui.

La partie capteur ultrason n'est toutefois pas encore connectée ni programmée dans l'architecture actuelle. Le module LiDAR fait lui aussi partie de l'objectif du projet, mais sans intégration matérielle ou logicielle à ce stade.

TODO - Ajouter photo : Raspberry Pi 4 monté sur le robot.

## Évolution de l'ordinateur principal
Le choix de l'ordinateur principal a surtout été guidé par un compromis entre performances de calcul, mémoire disponible et alimentation réellement tenable sur le robot.

**Ancienne piste abandonnée : Raspberry Pi 5**  
Le Raspberry Pi 5 a d'abord été envisagé pour disposer d'une marge confortable en performances. En pratique, cette carte demandait une alimentation pouvant fournir jusqu'à 5 A. À ce stade du projet, l'architecture d'alimentation était toutefois contrainte par le matériel déjà disponible : une batterie NiMH 6 V pour les moteurs, un pack de 6 piles NiMH pour la logique et une carte d'alimentation maison construite sur perfboard. Cette architecture n'était pas assez robuste pour alimenter correctement un Raspberry Pi 5, ce qui a conduit à des avertissements d'undervoltage et à l'abandon de cette piste comme solution par défaut.

**Étape intermédiaire : Raspberry Pi 3B+**  
Le Raspberry Pi 3B+ a ensuite servi de solution plus réaliste du point de vue énergétique. Avec un besoin d'environ 2,5 A, il était satisfaisant côté alimentation dans l'architecture disponible. En revanche, ses performances et sa mémoire se sont révélées trop limitées pour développer aisément avec VSCode, ROS 2 et SSH.

**Choix actuel : Raspberry Pi 4 B 4GB**  
Le Raspberry Pi 4 B 4GB, avec un besoin d'environ 3 A, constitue aujourd'hui le meilleur compromis entre performance, mémoire et faisabilité énergétique. Il apporte une marge de travail nettement plus confortable que le Raspberry Pi 3B+, tout en restant plus réaliste à intégrer dans l'architecture d'alimentation actuelle qu'un Raspberry Pi 5.

## Évolution du microcontrôleur
Le microcontrôleur retenu par défaut a lui aussi changé au fil des essais.

**Ancienne piste abandonnée : ESP32**  
L'ESP32 a été envisagé comme microcontrôleur principal, notamment pour la gestion des moteurs et des encodeurs. Cette piste reste visible dans certaines photos plus anciennes, mais elle n'est plus celle retenue comme base du projet.

**Choix actuel : Raspberry Pi Pico WH**  
Le Raspberry Pi Pico WH a remplacé l'ESP32 comme choix par défaut parce qu'il correspond mieux au besoin réel du projet. L'architecture reste plus simple, la base de travail plus lisible et l'ensemble plus cohérent pour l'apprentissage. Le rôle visé du Pico WH est de prendre en charge les capteurs analogiques, la commande des moteurs via le [Cytron MDD3A](https://ca.robotshop.com/fr/products/controleur-deux-moteurs-dc-3a-4-16v-cytron?qd=80d8e7f54ae4597c44a991f1b95499be), le pilotage des servos et la décharge de certaines tâches du Raspberry Pi principal.

## Architecture d'alimentation
À ce stade du projet, l'architecture d'alimentation reste contrainte par le matériel déjà disponible :

- une batterie NiMH 6 V pour les moteurs
- un pack de 6 piles NiMH pour la logique
- une carte d'alimentation maison construite sur perfboard

Cette carte d'alimentation sur perfboard a été construite autour de deux modules qui occupent une place importante dans l'architecture :

- [Pololu 4091 - régulateur abaisseur 5 V 5,5 A (D36V50F5)](https://ca.robotshop.com/fr/products/regulateur-tension-abaisseur-5v-55a-d36v50f5?qd=28823721af3ada67fe7280b7c3bc4ada)
- [Pololu 4090 - régulateur abaisseur 3,3 V 6,5 A (D36V50F3)](https://ca.robotshop.com/fr/products/regulateur-tension-abaisseur-pololu-33v-65a-d36v50f3?qd=6a1194a8c5c572ecd9aee4248462d953)

Ces deux modules structurent la distribution des tensions principales sur le robot. Cette architecture s'est montrée suffisante pour des essais plus modestes, mais pas assez robuste pour un Raspberry Pi 5, ce qui a directement conduit aux avertissements d'undervoltage observés lors des essais avec cette carte.

TODO - Ajouter photo : carte d'alimentation sur perfboard.
TODO - Ajouter photo : modules Pololu.
TODO - Ajouter photo : schéma simplifié de l'alimentation.

## Chaîne de commande moteur
La chaîne de commande moteur repose sur le Cytron MDD3A, qui est une pièce d'architecture importante au même titre que les modules d'alimentation. Il joue un rôle central dans la chaîne de commande entre la logique embarquée et les deux moteurs DC 6 V.

Dans l'organisation visée, le Raspberry Pi 4 B 4GB reste chargé des traitements plus haut niveau, tandis que le Raspberry Pi Pico WH gère la partie microcontrôleur et relaie les commandes vers le Cytron MDD3A. Cette répartition permet de garder une architecture plus claire et de réserver au microcontrôleur les tâches qui demandent une interaction plus directe avec les périphériques.

TODO - Ajouter photo : Cytron MDD3A.
TODO - Ajouter photo : intégration Pico WH + MDD3A.

## Principaux composants
- [Raspberry Pi 4 B 4GB](https://www.digikey.ca/en/products/detail/raspberry-pi/SC0194-9/10258781) : ordinateur principal actuel
- [Raspberry Pi Pico WH](https://www.pishop.ca/product/raspberry-pi-pico-wh-pre-soldered-headers/?searchid=0&search_query=Pico) : microcontrôleur retenu par défaut
- Chenilles du kit [Devastator de DFRobot](https://www.dfrobot.com/product-1477.html)
- 2 moteurs DC 6 V [DFRobot avec encodeur en quadrature (FIT0521)](https://www.dfrobot.com/product-1617.html)
- [Seeed Studio Grove Ultrasonic Ranger V2.0](https://ca.robotshop.com/fr/products/ranger-ultrasons-seeedstudio-grove?qd=f9c678a38cdae18967ff3b7829970d27) : capteur de distance retenu pour détecter les obstacles
- [Servomoteur Hitec HS-422](https://ca.robotshop.com/fr/products/servomoteur-hs-422-hitec?qd=f2222dcfa0ee946af00eea88c179699a) : support mobile du capteur ultrason pour balayer devant, à gauche et à droite
- [Pololu 4091 - régulateur abaisseur 5 V 5,5 A (D36V50F5)](https://ca.robotshop.com/fr/products/regulateur-tension-abaisseur-5v-55a-d36v50f5?qd=28823721af3ada67fe7280b7c3bc4ada) : régulation 5 V dans la carte d'alimentation
- [Pololu 4090 - régulateur abaisseur 3,3 V 6,5 A (D36V50F3)](https://ca.robotshop.com/fr/products/regulateur-tension-abaisseur-pololu-33v-65a-d36v50f3?qd=6a1194a8c5c572ecd9aee4248462d953) : régulation 3,3 V dans la carte d'alimentation
- [Cytron MDD3A](https://ca.robotshop.com/fr/products/controleur-deux-moteurs-dc-3a-4-16v-cytron?qd=80d8e7f54ae4597c44a991f1b95499be) : contrôleur moteur central dans l'architecture actuelle
- [Kit de développement scanner laser 360 RPLIDAR A2](https://ca.robotshop.com/fr/products/kit-developpement-scanner-laser-360-rplidar-2?variant=42412104712343) : module LiDAR prévu pour le positionnement du robot, mais pas encore intégré ni connecté
- Module DAC amplificateur classe D [TENSTAR MAX98357 I2S 3W](https://www.aliexpress.com/item/1005009890423190.html?spm=a2g0o.productlist.main.5.34252fcafdkwuB&algo_pvid=e82d20fb-bf35-49df-bbec-e02a78bb82c0&algo_exp_id=e82d20fb-bf35-49df-bbec-e02a78bb82c0-4&pdp_ext_f=%7B%22order%22%3A%2212%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21CAD%2111.88%215.82%21%21%2158.30%2128.57%21%402101f70717684377662296128ec21f%2112000050492046620%21sea%21CA%213050531386%21X%211%210%21n_tag%3A-29919%3Bd%3Aa83d08a1%3Bm03_new_user%3A-29895&curPageLogUid=vcXzsbGSeduY&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005009890423190%7C_p_origin_prod%3A) : module audio pour la sortie sonore
- Haut-parleur [Visaton BF37 5W, 8 Ohms](https://www.visaton.de/en/products/drivers/fullrange-systems/bf-37-8-ohm) : haut-parleur installé derrière le panneau avant perforé

## Chronologie
Les photos ci-dessous documentent surtout une phase antérieure du projet, centrée sur les essais avec Raspberry Pi 5 et ESP32. Le passage par le Raspberry Pi 3B+, puis l'adoption du Raspberry Pi 4 B 4GB et du Raspberry Pi Pico WH comme architecture de référence, ne sont pas encore illustrés ici par des photos dédiées.

### 2025-12-12 - Peu avant une déconstruction partielle
{{< figure
    src="devastator_001.jpg"
    alt="Robot Devastator modifié avant déconstruction partielle"
>}}
Configuration antérieure, photographiée peu avant une déconstruction partielle en vue de reprendre l'alimentation et de clarifier l'architecture électrique.

### 2025-12-22 - Après la déconstruction partielle
{{< figure
    src="devastator_002.jpg"
    alt="Robot Devastator modifié vue de face"
>}}
Vue de face après déconstruction partielle. À l'avant, on voit le capteur de distance à ultrason monté sur son servomoteur. L'objectif visé est de pouvoir regarder devant, à gauche et à droite afin d'estimer la direction la plus propice pour avancer, c'est-à-dire celle où il y a le moins d'obstacles. Cette partie n'est cependant pas encore connectée ni programmée. Derrière le panneau avant perforé, un haut-parleur Visaton BF 37 8 Ohms est installé.

### 2025-12-22 - Vue du dessus
{{< figure
    src="devastator_003.jpg"
    alt="Robot Devastator modifié vue du dessus"
>}}
Cette photo montre une ancienne piste d'architecture. On y voit un Raspberry Pi 5 en haut à gauche et un ESP32 à droite. À ce stade, l'idée était d'utiliser l'ESP32 comme contrôleur moteur, notamment pour la gestion des encodeurs. Cette organisation n'est plus celle retenue aujourd'hui. Les limites d'alimentation rencontrées avec le Raspberry Pi 5 ont ensuite conduit à l'étape intermédiaire sur Raspberry Pi 3B+, puis au choix actuel du Raspberry Pi 4 B 4GB.

### 2025-12-22 - Capot ouvert
{{< figure
    src="devastator_004.jpg"
    alt="Robot Devastator modifié capot ouvert, vue sur les moteurs"
>}}
Vue sur les deux moteurs DFRobot 6 V avec encodeur en quadrature (FIT0521).

## Prochaines étapes
- Stabiliser l'intégration entre le Raspberry Pi 4 B 4GB et le Raspberry Pi Pico WH
- Valider la commande des moteurs via le Cytron MDD3A et la lecture des encodeurs dans l'architecture actuelle
- Connecter et programmer l'ensemble Grove Ultrasonic Ranger V2.0 + HS-422 pour une détection simple d'obstacles et un balayage avant-gauche-droite
- Étudier l'intégration du RPLIDAR A2 pour préparer le positionnement du robot
- Intégrer et documenter proprement la carte d'alimentation sur perfboard
- Poursuivre l'intégration progressive des capteurs, des servos et de ROS 2

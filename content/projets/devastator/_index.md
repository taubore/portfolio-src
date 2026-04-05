+++
title = "Devastator"
weight = 10
description = "Plateforme de robot mobile chenillée documentée comme un projet d’apprentissage en électronique, Linux et ROS 2."
summary = "Robot mobile expérimental articulé autour d’un Raspberry Pi 4 B 4GB, d’un Raspberry Pi Pico WH et d’une base chenillée Devastator."
date = 2026-01-14
tags = ["Robotique", "Raspberry Pi 4", "Raspberry Pi Pico WH", "DFRobot", "ROS 2", "Python"]
categories = ["Projets"]
status = "En cours"
showTableOfContents = false
orderByWeight = true
+++

{{< figure
    src="devastator_thumbnail.jpg"
    alt="Robot mobile expérimental Devastator sur base chenillée"
    width="50%"
>}}

## Vue d’ensemble
Devastator est un robot mobile expérimental construit sur la base chenillée du [kit Devastator de DFRobot](https://www.dfrobot.com/product-1477.html). Je l’utilise comme plateforme d’apprentissage en électronique, en intégration de capteurs, en Linux et en [ROS 2](https://docs.ros.org/).

L’architecture actuelle de référence repose sur un [Raspberry Pi 4 B 4GB](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) pour la partie système et sur un [Raspberry Pi Pico WH](https://www.raspberrypi.com/products/raspberry-pi-pico/) pour la partie microcontrôleur. Les essais autour d’un Raspberry Pi 5, d’un Raspberry Pi 3B+ et d’un ESP32 restent utiles pour comprendre le cheminement du projet, mais ils relèvent maintenant de l’historique.

## Pourquoi ce projet
L’objectif n’est pas de présenter un robot fini, mais une plateforme concrète pour apprendre en travaillant sur de vraies contraintes. Le projet sert à documenter les choix matériels, les limites rencontrées, les changements de direction et les apprentissages qui restent réutilisables pour d’autres robots mobiles.

## État actuel
Le projet est encore en phase d’intégration matérielle et logicielle.

- **Architecture retenue** : Raspberry Pi 4 B 4GB + Raspberry Pi Pico WH
- **Base mécanique** : chenilles du kit Devastator et deux moteurs DC 6 V [DFRobot FIT0521](https://wiki.dfrobot.com/fit0521/)
- **Alimentation** : batterie NiMH 6 V pour les moteurs, pack de 6 piles NiMH pour la logique et carte d’alimentation maison sur perfboard
- **Sous-systèmes déjà en place** : base mécanique, alimentation de travail, capteur ultrason sur servo, chaîne audio, architecture logicielle de référence
- **Sous-systèmes encore à valider** : commande moteur via le [Cytron MDD3A](https://my.cytron.io/p-3amp-4v-16v-dc-motor-driver-2-channels), lecture des encodeurs et intégration propre Raspberry Pi 4 / Pico WH
- **Sous-systèmes pas encore intégrés** : [RPLIDAR A2](https://www.slamtec.com/en/Lidar/A2/)

## Architecture de référence actuelle
- **Calcul et orchestration** : le Raspberry Pi 4 B 4GB porte l’environnement Linux, le développement à distance, ROS 2 et les traitements de plus haut niveau.
- **Interface microcontrôleur** : le Raspberry Pi Pico WH est retenu pour les capteurs analogiques, le pilotage des servos et la chaîne de commande moteur.
- **Traction** : deux moteurs FIT0521 avec encodeur en quadrature doivent être commandés via le Cytron MDD3A.
- **Alimentation** : la carte maison distribue les tensions à partir d’une batterie NiMH 6 V, d’un pack logique et de deux régulateurs [Pololu 4091](https://www.pololu.com/product-info-merged/4091) et [Pololu 4090](https://www.pololu.com/product-info-merged/4090).
- **Perception proche** : un [Grove Ultrasonic Ranger](https://wiki.seeedstudio.com/Grove-Ultrasonic_Ranger/) monté sur un [servomoteur Hitec HS-422](https://hitecrcd.com/hs-422-deluxe-standard-servo/?setCurrencyId=1) doit permettre un balayage avant-gauche-droite pour l’évitement d’obstacles.
- **Perception à plus long terme** : le RPLIDAR A2 est prévu pour le positionnement, mais n’est ni connecté ni programmé à ce stade.

## Sous-systèmes principaux
- **Puissance et distribution** : c’est le cœur des arbitrages du projet. Les limites réelles de cette partie ont amené l’abandon du Raspberry Pi 5 comme référence de travail.
- **Commande moteur et encodeurs** : la validation de la chaîne Pico WH + Cytron MDD3A + FIT0521 reste une étape clé pour fiabiliser la base roulante.
- **Perception embarquée** : l’ensemble Grove Ultrasonic Ranger + HS-422 est déjà présent physiquement, mais son intégration logicielle reste à faire.
- **Audio embarqué** : une petite chaîne audio est déjà mentionnée dans les sources et complète utilement la plateforme, même si elle reste moins documentée que le reste.

## Quelques photos
Les photos actuelles documentent surtout une phase antérieure du projet. Elles restent utiles pour visualiser la base mécanique, le capteur ultrason et l’encombrement général, mais elles ne montrent pas encore proprement l’architecture de référence Raspberry Pi 4 B 4GB + Pico WH.

{{< figure
    src="Devastator_002.jpg"
    alt="Vue générale du robot Devastator après déconstruction partielle"
    caption="Vue générale après déconstruction partielle. Le capteur ultrason sur servo et le haut-parleur derrière la face avant sont déjà visibles."
    width="70%"
>}}

{{< figure
    src="Devastator_004.jpg"
    alt="Vue ouverte de la base mécanique et des moteurs Devastator"
    caption="Vue sur la base mécanique et les deux moteurs DFRobot 6 V avec encodeur, toujours au centre de l’architecture actuelle."
    width="70%"
>}}

- TODO - Ajouter photo : Raspberry Pi 4 B 4GB monté dans l’architecture actuelle.
- TODO - Ajouter vidéo : essai de conduite de base avec l’architecture Raspberry Pi 4 B 4GB + Pico WH.

## Prochaines étapes
- Stabiliser l’intégration entre le Raspberry Pi 4 B 4GB et le Raspberry Pi Pico WH
- Connecter et programmer l’ensemble Grove Ultrasonic Ranger + HS-422 pour une détection simple d’obstacles
- Intégrer la lecture des encodeurs dans l’architecture actuelle
- Concevoir à l'aide KiCAD une vraie carte d'alimentation pour remplacer celle actuelle sur perfboard.
- Étudier l’intégration du RPLIDAR A2 pour préparer le positionnement du robot
- Poursuivre l’intégration progressive des capteurs, des servos et de ROS 2

## Pour aller plus loin
Les pages listées ci-dessous détaillent l’architecture de référence, les composantes principales et l’évolution du projet sans alourdir cette page d’entrée.

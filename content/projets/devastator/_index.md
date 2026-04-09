+++
title = "Devastator"
weight = 10
description = "Plateforme de robot mobile chenillée documentée comme un projet d’apprentissage en électronique, Linux et ROS 2."
summary = "Robot mobile expérimental articulé autour d’un Raspberry Pi 4 B 4GB, d’un Raspberry Pi Pico WH et d’une base chenillée Devastator."
date=2024-09-01
tags = ["Robotique", "Raspberry Pi 4", "Raspberry Pi Pico WH", "DFRobot", "ROS 2", "Python"]
categories = ["Projets"]
status = "En cours"
showTableOfContents = false
orderByWeight = true
+++

## 1. Informations clés

- **Type de projet** : Robot mobile autonome
- **Objectif principal** : Apprentissage de ROS 2
- **Système d'exploitation, langage et framework** : Linux Ubuntu 24.04 LTS, Python et ROS 2
- **État** : actif

## 2. Vue d’ensemble

Devastator est un robot mobile expérimental construit sur la base chenillée du [kit Devastator de DFRobot](https://www.dfrobot.com/product-1477.html). L’architecture actuelle repose sur un [Raspberry Pi 4 B 4GB](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) et sur un [Raspberry Pi Pico WH](https://www.raspberrypi.com/products/raspberry-pi-pico/).

Je m'en sert essentiellement comme plateforme d’apprentissage, notamment pour l'apprentissage du *framework* robotique  [ROS 2](https://docs.ros.org/).

Le projet est encore en phase d’intégration matérielle et logicielle. Je pourrai conclure avoir atteint l'objectif de ce projet lorsque le scanner laser à 360 degrés [RPLIDAR A2](https://www.slamtec.com/en/Lidar/A2/) aura été intégré et permettra au robot de se déplacer à travers les obstacles.

{{< figure
    src="devastator_thumbnail.jpg"
    alt="Robot mobile expérimental Devastator sur base chenillée"
    width="50%"
>}}

## 3. Architecture

### 3.1 - Coeur du robot et orchestration

Un [Raspberry Pi 4 B 4GB](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) est utilisé sous Linux Ubuntu 24.04 LTS avec ROS 2 Jazzy. Le développement s'effectue via SSH à partir d'un PC lui aussi sous Linux Ubuntu. Le Raspberry Pi 4 constitue le point d’ancrage logiciel du projet pour l'orchestration de l'ensemble du robot et les traitements qui n’ont pas besoin d’être au plus près du matériel.

Le choix d'un Rasbperry Pi 4 4GB a surtout été guidé par un compromis entre performances, mémoire disponible et alimentation réellement tenable sur le robot. Pour des raisons de commodité et de stabilité des connexions, une [carte bouclier GeeekPi](https://www.amazon.ca/-/fr/dp/B08GKQMC72?ref=ppx_yo2ov_dt_b_fed_asin_title) est utilisée.

Un [Raspberry Pi Pico WH](https://www.raspberrypi.com/products/raspberry-pi-pico/) vient complèter le Raspberry Pi 4 en s'occupant du pilotage des moteurs, la lecture des encodeurs en quadraturedes, des capteurs analogiques lorsque ce sera requis et du pilotage du servo. Cette répartition garde le Raspberry Pi 4 sur les tâches de plus haut niveau et réserve au Pico WH les interactions plus directes avec les entrées-sorties. Pour des raisons de commodité et de stabilité des connexions, une [carte bouclier Freenove](https://www.amazon.ca/-/fr/dp/B0BFB53Y2N?ref=ppx_yo2ov_dt_b_fed_asin_title) est utilisée.

#### Difficultés rencontrées et apprentissages

Un Raspberry Pi 5 a d’abord été envisagé mais en pratique, cette carte demandait une alimentation pouvant fournir jusqu’à 5 A, mais le sous-système d'alimentation construit alors n’était pas assez robuste pour l'alimenter correctement, celui-ci menait à des avertissements d’undervoltage.Un Raspberry Pi 3B+ 1GB a ensuite servi de solution plus réaliste du point de vue énergétique. Avec un besoin d’environ 2,5 A, il était satisfaisant côté alimentation dans l’architecture disponible. En revanche, ses performances et sa mémoire se sont révélées trop limitées pour développer confortablement avec VSCode, ROS 2 et SSH. Voilà qui explique l'usage du Raspberry Pi 4 à 4GB.

Ce que j'ai appris avec ceci : Une architecture d’alimentation doit être pensée comme une contrainte de conception de premier plan, pas comme un détail. Une Raspberry Pi plus puissant n’est pas automatiquement le meilleur choix si il fragilise le reste du système sans profiter de la puissance en tant que telle.

Un ESP32 a été envisagé comme microcontrôleur principal avant de fixer l'usage d'un Pico. Cette piste reste visible dans certaines photos de la section chronologie, mais elle n’est plus celle retenue comme base du projet. Pourquoi? Pour rester dans la gamme des Raspberry Pi et me donner l'occasion d'apprendre le Pico WH que j'avais déjà en main.

### 3.2 - Alimentation

Carte maison sur un [perfboard](https://courstechinfo.be/Labo/Perfboard.html) dont l'objectif est de fournir 5 V et 3,3 V respectivement par les modules [Pololu 4091](https://www.pololu.com/product-info-merged/4091) et [Pololu 4090](https://www.pololu.com/product-info-merged/4090) qui sont alimentés à partir d’un pack de 6 piles AA NiMH. Une batterie distincte NiMH de 6 V est prévue pour l'alimentation des deux moteurs FIT0521. Ces deux batteries sont placées sous le robot avec des supports créés avec Fusion 360 puis imprimé en 3D sur une imprimante Flashforge Adventurer 5M Pro, en PLA.

- une batterie NiMH 6 V pour les moteurs
- un pack de 6 piles NiMH pour la logique
- une carte d’alimentation maison construite sur perfboard

Cette carte d’alimentation s’articule autour de deux régulateurs qui structurent la distribution des tensions principales :

- [Pololu 4091 - régulateur abaisseur 5 V 5,5 A (D36V50F5)](https://www.pololu.com/product-info-merged/4091)
- [Pololu 4090 - régulateur abaisseur 3,3 V 6,5 A (D36V50F3)](https://www.pololu.com/product-info-merged/4090)

Cette organisation a suffi pour des essais modestes, mais elle a montré ses limites lorsque le projet s’orientait vers un Raspberry Pi 5. C’est une contrainte importante à garder en tête pour comprendre les choix actuels.

Les limites réelles de cette partie ont amené l’abandon du Raspberry Pi 5 qui était ciblé au départ.

### 3.3 - Base mécanique

Chenilles du [kit Devastator de DFRobot](https://www.dfrobot.com/product-1477.html) avec les deux plaques métalliques les supportant et servant de support aux moteurs.

### 3.4 - Traction

Deux moteurs DC 6 V [DFRobot FIT0521](https://wiki.dfrobot.com/fit0521/) avec encodeur en quadrature contrôlés via le [Cytron MDD3A](https://my.cytron.io/p-3amp-4v-16v-dc-motor-driver-2-channels).

### 3.5 - Perception de l'environnement

Un module ultrason [Grove Ultrasonic Ranger](https://wiki.seeedstudio.com/Grove-Ultrasonic_Ranger/) est monté sur un [servomoteur Hitec HS-422](https://hitecrcd.com/hs-422-deluxe-standard-servo/?setCurrencyId=1) pour un balayage avant-gauche-droite pour effectuer un évitement d’obstacles de base. Un module LiDAR [RPLIDAR A2](https://www.slamtec.com/en/Lidar/A2/) est déjà monté sur le robot, mais n'est pas connecté, ni encore programmé à ce jour. Il s'agira fort probablement de la dernière pièces que je vais connecter.

### 3.6 - Audio / voix

Pour faire parler le robot, l'utilisation de [Piper](https://github.com/rhasspy/piper) pour la partie logicielle. Le Raspberry Pi 4 est connecté à un module DAC amplificateur classe D [TENSTAR MAX98357 I2S 3W](https://www.aliexpress.com/item/1005007889671315.html?spm=a2g0o.order_list.order_list_main.156.10f61802tvFAYq) alors que le TENSTAR est connecté à un haut-parleur [Visaton BF37 5W, 8 Ohms](https://www.visaton.de/en/products/drivers/fullrange-systems/bf-37-8-ohm) installé derrière le panneau avant perforé.

### 3.7 - Contrôle manuel

Une télécommande [PS2 Lynxmotion](https://ca.robotshop.com/fr/products/controleur-robot-ps2-v4-lynxmotion?) est utilisée pour fins de tests lorsque la commande du robot en mode manuelle est requise.

## 4. Prochaines étapes

- Stabiliser l’intégration entre le Raspberry Pi 4 B 4GB et le Raspberry Pi Pico WH.
- Connecter et programmer l’ensemble Grove Ultrasonic Ranger + HS-422 pour une détection simple d’obstacles.
- Poursuivre l’intégration progressive des capteurs et du servomoteur avec ROS 2.
- Intégrer la lecture des encodeurs dans l’architecture actuelle.
- Concevoir à l'aide KiCAD une vraie carte d'alimentation pour remplacer celle actuelle sur perfboard.
- Étudier l’intégration du RPLIDAR A2 pour un évitement d'obstacle plus avancé.

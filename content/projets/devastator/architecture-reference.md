+++
title = "Architecture de référence"
description = "Référence actuelle de Devastator : répartition des rôles, alimentation, chaîne moteur, capteurs et limites connues."
summary = "Vue de référence de l’architecture actuelle : Raspberry Pi 4 B 4GB, Pico WH, alimentation, moteurs, capteurs et audio."
date = 2026-01-14
weight = 10
categories = ["Projets"]
status = "En cours"
showTableOfContents = false
+++

Cette page rassemble l’architecture de référence actuelle de Devastator. Elle documente l’organisation retenue aujourd’hui, même si plusieurs sous-systèmes restent encore en cours d’intégration.

## Vue d’ensemble
| Bloc | Éléments actuels | Rôle dans le projet |
| --- | --- | --- |
| Base mécanique | [Kit Devastator de DFRobot](https://www.dfrobot.com/product-1477.html) + 2 moteurs [FIT0521](https://wiki.dfrobot.com/fit0521/) | Fournir la plateforme roulante et les encodeurs de traction |
| Calcul principal | [Raspberry Pi 4 B 4GB](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) | Linux, ROS 2, développement à distance et traitements de plus haut niveau |
| Microcontrôleur | [Raspberry Pi Pico WH](https://www.raspberrypi.com/products/raspberry-pi-pico/) | Capteurs analogiques, servos et relais vers la commande moteur |
| Alimentation | batterie NiMH 6 V moteurs + pack de 6 piles NiMH logique + carte maison sur perfboard | Distribuer les tensions nécessaires au robot avec le matériel déjà disponible |
| Commande moteur | [Cytron MDD3A](https://my.cytron.io/p-3amp-4v-16v-dc-motor-driver-2-channels) | Faire l’interface entre la logique embarquée et les deux moteurs DC |
| Perception proche | [Grove Ultrasonic Ranger](https://wiki.seeedstudio.com/Grove-Ultrasonic_Ranger/) + [Hitec HS-422](https://hitecrcd.com/hs-422-deluxe-standard-servo/?setCurrencyId=1) | Balayer l’avant du robot et détecter les obstacles proches |
| Perception à venir | [RPLIDAR A2](https://www.slamtec.com/en/Lidar/A2/) | Préparer à plus long terme le positionnement et la cartographie |
| Audio | module basé sur [MAX98357A](https://www.analog.com/en/products/max98357a.html) + haut-parleur [Visaton BF 37 - 8 Ohm](https://www.visaton.de/en/products/drivers/fullrange-systems/bf-37-8-ohm) | Ajouter une sortie sonore simple à la plateforme |

## Calcul principal et logique embarquée
Le Raspberry Pi 4 B 4GB constitue aujourd’hui le point d’ancrage logiciel du projet. C’est lui qui porte l’environnement Linux, le développement à distance, ROS 2, Python et les traitements qui n’ont pas besoin d’être au plus près du matériel.

Le Raspberry Pi Pico WH complète cette partie en prenant la place du microcontrôleur de référence. Son rôle visé est de gérer les capteurs analogiques, le pilotage de servos et la commande des moteurs. Cette répartition garde le Raspberry Pi 4 sur les tâches de plus haut niveau et réserve au Pico WH les interactions plus directes avec les entrées-sorties.

TODO - Ajouter photo : Raspberry Pi 4 B 4GB monté sur le robot.

## Architecture d’alimentation
L’architecture d’alimentation actuelle reste contrainte par le matériel déjà disponible :

- une batterie NiMH 6 V pour les moteurs
- un pack de 6 piles NiMH pour la logique
- une carte d’alimentation maison construite sur perfboard

Cette carte d’alimentation s’articule autour de deux régulateurs qui structurent la distribution des tensions principales :

- [Pololu 4091 - régulateur abaisseur 5 V 5,5 A (D36V50F5)](https://www.pololu.com/product-info-merged/4091)
- [Pololu 4090 - régulateur abaisseur 3,3 V 6,5 A (D36V50F3)](https://www.pololu.com/product-info-merged/4090)

Cette organisation a suffi pour des essais modestes, mais elle a montré ses limites lorsque le projet s’orientait vers un Raspberry Pi 5. C’est une contrainte importante à garder en tête pour comprendre les choix actuels.

- TODO - Ajouter photo : carte d’alimentation sur perfboard.
- TODO - Ajouter photo : modules Pololu.
- TODO - Ajouter schéma simplifié : distribution d’alimentation actuelle.

## Chaîne de commande moteur
La chaîne de commande moteur repose sur le Cytron MDD3A, qui est une pièce d’architecture importante au même titre que la carte d’alimentation. Il assure l’interface entre la logique embarquée et les deux moteurs DC 6 V.

Dans l’organisation visée, le Raspberry Pi 4 B 4GB reste chargé des traitements de plus haut niveau, tandis que le Raspberry Pi Pico WH relaie les commandes vers le Cytron MDD3A et doit, à terme, participer à la lecture des encodeurs. Cette séparation rend l’architecture plus lisible et plus adaptée à une plateforme d’apprentissage.

Le point important ici n’est pas seulement le choix du driver moteur, mais la clarté de la chaîne complète : calcul principal, microcontrôleur, driver, moteurs et encodeurs.

- TODO - Ajouter photo : Cytron MDD3A.
- TODO - Ajouter photo : intégration Pico WH + MDD3A.

## Capteurs et perception
La perception de proximité repose aujourd’hui sur un Grove Ultrasonic Ranger monté sur un servomoteur HS-422. L’objectif visé est simple : regarder devant, à gauche et à droite afin d’estimer la direction la plus praticable pour avancer. Cette partie est déjà présente physiquement, mais elle n’est pas encore connectée ni programmée dans l’architecture actuelle.

Le RPLIDAR A2 relève d’une étape plus lointaine. Il fait bien partie de la trajectoire du projet, mais sans intégration matérielle ou logicielle à ce stade. Il faut donc le lire comme un composant prévu, pas comme un sous-système déjà opérationnel.

## Chaîne audio
Les sources actuelles mentionnent un module DAC amplificateur classe D TENSTAR MAX98357 I2S 3W ainsi qu’un haut-parleur Visaton BF37 5W, 8 Ohms installé derrière le panneau avant perforé.

Cette partie est moins détaillée que l’alimentation, la commande moteur ou les capteurs. Elle reste toutefois utile à documenter parce qu’elle montre que Devastator ne se limite pas à la traction et à la détection d’obstacles.

TODO - Ajouter hyperlien : module audio TENSTAR MAX98357 I2S 3W exact utilisé.

## Limites connues
- La référence actuelle Raspberry Pi 4 B 4GB + Pico WH n’est pas encore documentée par des photos dédiées
- La chaîne moteur n’est pas encore validée de bout en bout dans l’architecture actuelle
- Le capteur ultrason sur servo est monté, mais pas encore intégré logiciellement
- Le RPLIDAR A2 est prévu, sans intégration à ce stade

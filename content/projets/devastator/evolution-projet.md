+++
title = "Évolution du projet"
description = "Historique synthétique de Devastator : essais, bifurcations techniques, composants abandonnés et chronologie photo."
summary = "Lecture historique du projet : choix d’ordinateur principal, choix du microcontrôleur et chronologie visuelle."
date = 2026-01-14
weight = 30
categories = ["Projets"]
status = "En cours"
showTableOfContents = false
+++

Cette page conserve la partie historique de Devastator. Elle sert à comprendre pourquoi l’architecture actuelle est celle du Raspberry Pi 4 B 4GB et du Raspberry Pi Pico WH, et pourquoi certaines pistes plus ambitieuses ou plus anciennes ont été écartées.

## Pourquoi garder l’historique
Le projet n’avance pas en ligne droite. Les essais autour du [Raspberry Pi 5](https://www.raspberrypi.com/products/raspberry-pi-5/), du [Raspberry Pi 3 Model B+](https://www.raspberrypi.com/products/raspberry-pi-3-model-b-plus/) et de l’[ESP32](https://www.espressif.com/en/products/socs/esp32) restent utiles parce qu’ils expliquent des choix toujours visibles aujourd’hui :

- le budget d’alimentation compte autant que la puissance de calcul
- la lisibilité de l’architecture vaut souvent mieux qu’une solution plus ambitieuse mais plus fragile
- une plateforme d’apprentissage gagne à être progressive et reconfigurable

## Évolution de l’ordinateur principal
Le choix de l’ordinateur principal a surtout été guidé par un compromis entre performances de calcul, mémoire disponible et alimentation réellement tenable sur le robot.

### Ancienne piste abandonnée : Raspberry Pi 5
Le Raspberry Pi 5 a d’abord été envisagé pour disposer d’une marge confortable en performances. En pratique, cette carte demandait une alimentation pouvant fournir jusqu’à 5 A. À ce stade du projet, l’architecture d’alimentation reposait déjà sur une batterie NiMH 6 V pour les moteurs, un pack de 6 piles NiMH pour la logique et une carte d’alimentation maison sur perfboard. Cette architecture n’était pas assez robuste pour alimenter correctement un Raspberry Pi 5, ce qui a conduit à des avertissements d’undervoltage et à l’abandon de cette piste comme solution par défaut.

### Étape intermédiaire : Raspberry Pi 3B+
Le Raspberry Pi 3B+ a ensuite servi de solution plus réaliste du point de vue énergétique. Avec un besoin d’environ 2,5 A, il était satisfaisant côté alimentation dans l’architecture disponible. En revanche, ses performances et sa mémoire se sont révélées trop limitées pour développer confortablement avec VSCode, ROS 2 et SSH.

### Choix actuel : Raspberry Pi 4 B 4GB
Le Raspberry Pi 4 B 4GB, avec un besoin d’environ 3 A, constitue aujourd’hui le meilleur compromis entre performance, mémoire et faisabilité énergétique. Il apporte une marge de travail nettement plus confortable que le Raspberry Pi 3B+, tout en restant plus réaliste à intégrer dans l’architecture d’alimentation actuelle qu’un Raspberry Pi 5.

## Évolution du microcontrôleur
Le microcontrôleur retenu par défaut a lui aussi changé au fil des essais.

### Ancienne piste abandonnée : ESP32
L’ESP32 a été envisagé comme microcontrôleur principal, notamment pour la gestion des moteurs et des encodeurs. Cette piste reste visible dans certaines photos plus anciennes, mais elle n’est plus celle retenue comme base du projet.

### Choix actuel : Raspberry Pi Pico WH
Le Raspberry Pi Pico WH a remplacé l’ESP32 comme choix par défaut parce qu’il correspond mieux au besoin réel du projet. L’architecture reste plus simple, la base de travail plus lisible et l’ensemble plus cohérent pour l’apprentissage. Le rôle visé du Pico WH est de prendre en charge les capteurs analogiques, la commande des moteurs via le [Cytron MDD3A](https://my.cytron.io/p-3amp-4v-16v-dc-motor-driver-2-channels), le pilotage des servos et la décharge de certaines tâches du Raspberry Pi principal.

## Ce que cette évolution a appris au projet
- Une architecture d’alimentation doit être pensée comme une contrainte de conception de premier plan, pas comme un détail
- Une carte plus puissante n’est pas automatiquement le meilleur choix si elle fragilise le reste du système
- Clarifier la répartition des rôles entre ordinateur principal et microcontrôleur simplifie autant l’intégration que la documentation

## Chronologie visuelle
Les photos ci-dessous documentent surtout une phase antérieure du projet, centrée sur les essais avec Raspberry Pi 5 et ESP32. Le passage par le Raspberry Pi 3B+, puis l’adoption du Raspberry Pi 4 B 4GB et du Raspberry Pi Pico WH comme architecture de référence, ne sont pas encore illustrés ici par des photos dédiées.

TODO - Ajouter photo : architecture actuelle Raspberry Pi 4 B 4GB + Pico WH après remontage.

### 2025-12-12 - Peu avant une déconstruction partielle
{{< figure
    src="../Devastator_001.jpg"
    alt="Robot Devastator avant déconstruction partielle"
    caption="Configuration antérieure, photographiée peu avant une déconstruction partielle en vue de reprendre l’alimentation et de clarifier l’architecture électrique."
>}}

### 2025-12-22 - Après la déconstruction partielle
{{< figure
    src="../Devastator_002.jpg"
    alt="Robot Devastator vue de face après déconstruction partielle"
    caption="Vue de face après déconstruction partielle. À l’avant, on voit le capteur de distance à ultrason monté sur son servomoteur. L’objectif visé est de pouvoir regarder devant, à gauche et à droite afin d’estimer la direction la plus propice pour avancer, c’est-à-dire celle où il y a le moins d’obstacles. Cette partie n’est cependant pas encore connectée ni programmée. Derrière le panneau avant perforé, un haut-parleur Visaton BF 37 8 Ohms est installé."
>}}

### 2025-12-22 - Vue du dessus
{{< figure
    src="../Devastator_003.jpg"
    alt="Robot Devastator vu du dessus pendant une ancienne piste d’architecture"
    caption="Cette photo montre une ancienne piste d’architecture. On y voit un Raspberry Pi 5 en haut à gauche et un ESP32 à droite. À ce stade, l’idée était d’utiliser l’ESP32 comme contrôleur moteur, notamment pour la gestion des encodeurs. Cette organisation n’est plus celle retenue aujourd’hui. Les limites d’alimentation rencontrées avec le Raspberry Pi 5 ont ensuite conduit à l’étape intermédiaire sur Raspberry Pi 3B+, puis au choix actuel du Raspberry Pi 4 B 4GB."
>}}

### 2025-12-22 - Capot ouvert
{{< figure
    src="../Devastator_004.jpg"
    alt="Robot Devastator capot ouvert avec vue sur les moteurs"
    caption="Vue sur les deux moteurs DFRobot 6 V avec encodeur en quadrature (FIT0521)."
>}}

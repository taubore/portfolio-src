+++
title = "Évolution et historique du projet"
description = "Historique synthétique de Devastator : essais, bifurcations techniques, composants abandonnés et chronologie photo."
summary = "Lecture historique du projet : choix d’ordinateur principal, choix du microcontrôleur et chronologie visuelle."
weight = 10
showTableOfContents = false
+++

## 2025-12-12 - Peu avant une déconstruction partielle

{{< figure
    src="../devastator_2025-12-12.jpg"
    alt="Robot Devastator avant déconstruction partielle"
    caption="Configuration antérieure, photographiée peu avant une déconstruction partielle en vue de reprendre l’alimentation et de clarifier l’architecture électrique."
>}}

## 2025-12-22 - Après la déconstruction partielle

{{< figure
    src="../devastator_2025-12-22_01.jpg"
    alt="Robot Devastator vue de face après déconstruction partielle"
    caption="Vue de face après déconstruction partielle. À l’avant, on voit le capteur de distance à ultrason monté sur son servomoteur. L’objectif visé est de pouvoir regarder devant, à gauche et à droite afin d’estimer la direction la plus propice pour avancer, c’est-à-dire celle où il y a le moins d’obstacles. Cette partie n’est cependant pas encore connectée ni programmée. Derrière le panneau avant perforé, un haut-parleur Visaton BF 37 8 Ohms est installé."
>}}

## 2025-12-22 - Vue du dessus

{{< figure
    src="../devastator_2025-12-22_01.jpg"
    alt="Robot Devastator vu du dessus pendant une ancienne piste d’architecture"
    caption="Cette photo montre une ancienne piste d’architecture. On y voit un Raspberry Pi 5 en haut à gauche et un ESP32 à droite. À ce stade, l’idée était d’utiliser l’ESP32 comme contrôleur moteur, notamment pour la gestion des encodeurs. Cette organisation n’est plus celle retenue aujourd’hui. Les limites d’alimentation rencontrées avec le Raspberry Pi 5 ont ensuite conduit à l’étape intermédiaire sur Raspberry Pi 3B+, puis au choix actuel du Raspberry Pi 4 B 4GB."
>}}

## 2025-12-22 - Capot ouvert

{{< figure
    src="../devastator_2025-12-22_03.jpg"
    alt="Robot Devastator capot ouvert avec vue sur les moteurs"
    caption="Vue sur les deux moteurs DFRobot 6 V avec encodeur en quadrature (FIT0521)."
>}}

## 2026-04-05 - Nouvelle configuration

{{< figure
    src="../devastator_2026-04-05_01.jpg"
    alt="Robot Devastator vue du dessus. Raspberry Pi 4 à droite sous une carte borniers et Raspberry Pi Pico WH à gauche monté sur une carte borniers."
    caption="Nouvelle configuration avec un Raspberry Pi 4 à droite sous une carte borniers et un Raspberry Pi Pico WH à gauche monté sur une carte borniers. Les deux afficheurs LED me permettent de lire le voltage de mes deux pack de batteries NiMH. À droite completement, on voit le module LiDAR qui se monte par dessus tout ceci."
>}}

## 2026-04-05 - Mouvements télécommandés

{{< youtube
    id="ivinoNjZYnw"
    title="Premiers mouvements avec une télécommande"
    caption="Premiers mouvements avec une télécommande de type Playstation 2 de Lynxmotion."
>}}

## 2026-04-05 - Carte d'alimentation

{{< figure
    src="../devastator_2026-04-05_02.jpg"
    alt="Carte d'alimentation du Robot Devastator"
    caption="Il s'agit de la carte d'alimentation construite sur un perfboard et sur laquelle les deux modules de régulation de tension (5 V et 3,3 V) Pololu sont montés. Plusieurs condensateurs pour assurer une stabilité de l'alimentation ainsi qu'un fusible pour plus de sureté."
>}}

## 2026-06-06 - Autonomie simple avec un sonar à ultrason

{{< youtube
    id="rexOt6dcGlg"
    title="Autonomie simple"
    caption="Se déplace seul avec un sonar à ultrason. Lorsqu'un obstacle est rencontré, il s'arrête, regarde à gauche et à droite et choisit là où c'est le plus dégagé. Il fait alors une rotation dans ce sens jusqu'à ce que ce soit suffisament dégagé et se remet en mouvement par en avant. Le robot est capable de parler à l'aide du moteur de synthèse vocale local [Piper](https://github.com/OHF-Voice/piper1-gpl) . Modèle basé sur l'intelligence artificielle qui transforme du texte en parole naturelle."
>}}

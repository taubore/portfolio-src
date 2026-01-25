+++
title = "Devastator"
weight = 19
description = "Mon robot expérimental qui m'aide à apprendre l'électronique et divers capteurs ainsi que le framework ROS 2."
summary = "Robot mobile expérimental pour l’apprentissage de l’électronique et de ROS 2."
thumbnailImage = "devastator_000.jpg"
date = 2026-01-14
tags = ["Robotique", "Raspberry Pi 5", "ESP32", "DFRobot", "ROS 2", "Python"]
categories = ["Projets"]
status = "En cours"
+++

{{< figure
    src="devastator_000.jpg"
    alt="Robot mobile expérimental pour l’apprentissage de l’électronique et de ROS 2"
    width="50%"
>}}

## Informations clés
- **Type de projet** : Robot mobile expérimental
- **Objectif principal** : Apprentissage de l’électronique et de ROS 2
- **Principaux composants** : Raspberry Pi 5, ESP32, kit Devastator de DFRobot
- **Système d'exploitation, langage et framework** : Linux, Python, ROS 2
- **État** : en cours

## Description
Robot expérimental conçu autour de ROS 2 (Jazzy), le Raspberry Pi 5, l'ESP32 et le langage Python. Beaucoup d'apprentissage à avancer en parallèle. Robot initialement bâti à partir du kit [Devastator de DFRobot](https://www.dfrobot.com/product-1477.html), maintenant, je n'utilise que les chenilles de cette plateforme. Les moteurs ont été remplacés par une version avec encodeur en quadrature. La voix du robot, en français, fonctionne grâce à [Piper](https://github.com/rhasspy/piper) via le Raspberry Pi 5 et un petit module amplificateur mono classe D, 3W avec protocole I2S (MAX98357) 

## Principaux composants
- Chenilles du kit [Devastator de DFRobot](https://www.dfrobot.com/product-1477.html)
- Raspeberry Pi 5
- ESP32 
- 2 Moteurs DC 6V [DFRobot avec encodeur en quadrature (FIT0521)](https://www.dfrobot.com/product-1617.html)
- Module DAC amplificateur classe D [TENSTAR MAX98357 I2S 3W](https://www.aliexpress.com/item/1005009890423190.html?spm=a2g0o.productlist.main.5.34252fcafdkwuB&algo_pvid=e82d20fb-bf35-49df-bbec-e02a78bb82c0&algo_exp_id=e82d20fb-bf35-49df-bbec-e02a78bb82c0-4&pdp_ext_f=%7B%22order%22%3A%2212%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21CAD%2111.88%215.82%21%21%2158.30%2128.57%21%402101f70717684377662296128ec21f%2112000050492046620%21sea%21CA%213050531386%21X%211%210%21n_tag%3A-29919%3Bd%3Aa83d08a1%3Bm03_new_user%3A-29895&curPageLogUid=vcXzsbGSeduY&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005009890423190%7C_p_origin_prod%3A)
- Haut parleur [Visaton BF37 5W, 8 Ohms](https://www.visaton.de/en/products/drivers/fullrange-systems/bf-37-8-ohm)

## Chronologie

### 2025-12-12 - Peu avant une déconstruction partielle
{{< figure
    src="devastator_001.jpg"
    alt="Robot Devastator modifié avant déconstruction partielle"
>}}
Ancienne configuration peu avant déconstruction partielle, car je prévois une réfonte au niveau de l'alimentation.

### 2025-12-22 - Après la déconstruction partielle
{{< figure
    src="devastator_002.jpg"
    alt="Robot Devastator modifié vue de face"
>}}
Devant il y a un capteur de distance à ultrason (Seeed Studio - Grove - Ultrasonic Ranger V2.0). Derrière le panneau avant (zone trouée), il y a un haut parleur (Visaton BF 37 8 Ohms).

### 2025-12-22 - Vue du dessus
{{< figure
    src="devastator_003.jpg"
    alt="Robot Devastator modifié vue du dessus"
>}}
Raspberry Pi5 en haut à gauche. À droite un ESP32. Mon intention est de faire du ESP32 mon contrôleur de moteur avec notamment la gestion de l'encodeur. Le Raspebrry Pi donnera les ordres au ESP32 pour tout ce qui se rapporte aux moteurs.

### 2025-12-22 - Capot ouvert
{{< figure
    src="devastator_004.jpg"
    alt="Robot Devastator modifié capot ouvert, vue sur les moteurs"
>}}
Deux moteurs DFRobot 6 V avec encodeur en quadrature (FIT0521).
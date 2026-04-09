+++
title = "Évolution et historique du projet"
description = "Historique synthétique de Devastator : essais, bifurcations techniques, composants abandonnés et chronologie photo."
summary = "Lecture historique du projet : choix d’ordinateur principal, choix du microcontrôleur et chronologie visuelle."
weight = 10
showTableOfContents = false
+++

## 2025-12-23 - Bras *follower* presque terminé

{{< figure
    src="../lerobot_001.jpg"
    alt="Lerobot *follower*"
    caption="La construction semble terminée, mais pas tout à fait. Il me reste encore quelques pièces à assembler."
>}}

## 2026-01-02 - Bras *follower* finalisé et testé

{{< figure
    src="../lerobot_002.jpg"
    alt="Lerobot *follower* avec pièces pour le *leader*"
    caption="Le bras *follower* est maintenant terminé, branché, calibré et testé. Les 6 moteurs Feetech et les pièces pour le *leader* sont imprimés en plastique PLA."
>}}

## 2026-01-18 - Bras *leader* finalisé et testé

{{< figure
    src="../lerobot_003.jpg"
    alt="Lerobot *leader* construit, branché, calibré et testé."
    caption="Le bras *leader* est maintenant terminé, branché, calibré et testé. Quelques soucis lors de la calibration. Je n'avais pas centré la position de mes moteurs avec [l'outil de test de Feetech](https://www.feetechrc.com/software.html) avant l'assemblage. Lors de la calibration, j'ai eu une erreur et j'ai donc dû démonter chaque articulations pour repositionner chaque moteur au centre et remettre la pièces au bon endroit."
>}}

## 2026-01-18 - Premier essais avec le bras *follower*

{{< youtube
    id="maZ5j3GNaw8"
    title="Premiers essais avec le bras follower"
    caption="Premiers essais de mouvements du bras *follower* à partir d'un enregistrement fait avec le bras *leader*."
>}}

### Quelques exlications plus détaillées...

Un [premier programme en Python](https://github.com/Taubore/lerobot-ws/blob/main/Enregistre_leader.py) enregistre un fichier CSV avec des mouvements que j'ai effectués manuellement pendant 10 secondes sur le bras *leader*. Un [second programme Python](https://github.com/Taubore/lerobot-ws/blob/main/Reproduit_follower.py) lit le fichier CSV et reproduit ce mouvement sur le bras *follower*. C'est ce que représente cette vidéo. Encore aucune utilisation d'intelligence artificielle. 

Le programme Python qui reproduit le mouvement est très basique et ne fait aucune compensation de latence ni de compensation d'échelle. Cela signifie que le *follower* ne reproduira pas exactement à l'identique le mouvement du *leader*. 

Les prérequis pour faire rouler ces deux petits programme sont les suivants :  

1) Système d'exploitation [Linux Ubuntu 22.04](https://www.releases.ubuntu.com/). Oui, ce n'est pas la plus récente version, mais celle qui est sans risque de problèmes avec LeRobot. Je n'ai pas encore testé avec la plus récente version.
2) [Visual Studio Code](https://code.visualstudio.com/Download) pour Linux avec extension Python
3) LeRobot (logiciel) : https://huggingface.co/docs/lerobot/installation
4) LeRobot (matériel) : https://huggingface.co/docs/lerobot/so101

## 2026-01-21 - Caméra fixée au bras *follower*

{{< figure
    src="../lerobot_004.jpg"
    alt="Lerobot *follower* avec un caméra Arducam B0200"
    caption="Avec une mini caméra UVC USB 2 1080P montée sur la pince du bras *follower*. Je crois avoir ce qu'il faut pour m'attaquer à ce tutoriel : https://huggingface.co/docs/lerobot/il_robots. Possible qu'une autre caméra soit requise pour une vue du plan dans son ensemble."
>}}

## 2026-01-23 - Bras *follower* suivant les mouvements du bras *leader*

{{< youtube
    id="iu1M_ZqD9nU"
    title="Bras follower suivant les mouvements du bras leader"
    caption="Le bras *follower* suit les mouvements du bras *leader* avec le script [`teleoperate.py`](https://github.com/Taubore/lerobot-ws/blob/main/teleoperate.py). Ceci grâce au travail de [l'équipe projet LeRobot](https://github.com/huggingface/lerobot/graphs/contributors), un tout petit script Python tout simple suffit. Évidemment, la précision n'y est pas tout comme décrit à l'entrée du 2026-01-18, mais ça demeure tout de même impressionnant."
>}}

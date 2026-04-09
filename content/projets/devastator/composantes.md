+++
title = "Liste des composantes principales"
description = "Liste des principales composantes du projet Devastator avec rôle, statut, références et remarques utiles."
summary = "Forme de BOM (Bill of Materials) des composants structurants du projet avec leur rôle, leur statut et les raisons de leur présence."
weight = 20
showTableOfContents = false
+++

Cette page permet d'aborder l'ensemble du projet vu par ses composantes structurantes. Elle ne cherche pas à être exhaustive même si elle est assez complète. L'objectif est de fournir une vue plus synthèse pour expliquer le projet, ses choix techniques et son évolution.

Le tableau ci-dessous mélange donc volontairement les composantes déjà en place, celles retenues pour l’architecture actuelle, celles encore en test ainsi que quelques éléments abandonnés lorsqu’elles expliquent un pivot important du projet, comme l’abandon du Raspberry Pi 5 ou de l’ESP32. La colonne **Statut** permet donc de distinguer ceci.

<table class="devastator-bom">
  <thead>
    <tr>
      <th>Composant</th>
      <th>Rôle dans le projet</th>
      <th>Statut</th>
      <th>Référence / lien</th>
      <th>Remarque utile</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Base mécanique Devastator</td>
      <td>Plateforme roulante chenillée et support mécanique principal</td>
      <td>utilisé</td>
      <td><a href="https://www.dfrobot.com/product-1477.html">DFRobot Devastator</a></td>
      <td>La base mécanique reste la colonne vertébrale du projet malgré les refontes électroniques.</td>
    </tr>
    <tr>
      <td>2 x moteurs DC 6 V FIT0521</td>
      <td>Traction du robot et retour encodeur pour la vitesse / l’odométrie</td>
      <td>en test</td>
      <td><a href="https://wiki.dfrobot.com/fit0521/">DFRobot FIT0521</a></td>
      <td>Les encodeurs sont importants pour fiabiliser la conduite, mais leur lecture reste à valider dans l’architecture actuelle.</td>
    </tr>
    <tr>
      <td>Raspberry Pi 4 B 4GB</td>
      <td>Ordinateur principal pour Linux, ROS 2, Python et le développement à distance</td>
      <td>en test</td>
      <td><a href="https://www.raspberrypi.com/products/raspberry-pi-4-model-b/">Raspberry Pi 4</a></td>
      <td>Choix actuel parce qu’il offre un meilleur compromis performance / mémoire / alimentation que les pistes précédentes.</td>
    </tr>
    <tr>
      <td>Raspberry Pi Pico WH</td>
      <td>Microcontrôleur pour les entrées-sorties, les servos et la commande moteur</td>
      <td>en test</td>
      <td><a href="https://www.raspberrypi.com/products/raspberry-pi-pico/">Raspberry Pi Pico series</a></td>
      <td>Le projet vise explicitement la variante WH. Elle remplace l’ESP32 pour garder une architecture plus simple et plus lisible.</td>
    </tr>
    <tr>
      <td>Cytron MDD3A</td>
      <td>Contrôleur moteur entre la logique embarquée et les deux moteurs DC</td>
      <td>utilisé</td>
      <td><a href="https://my.cytron.io/p-3amp-4v-16v-dc-motor-driver-2-channels">Cytron MDD3A</a></td>
      <td>Pièce centrale de la chaîne de traction. La validation complète avec le Pico WH reste à faire.</td>
    </tr>
    <tr>
      <td>Batterie NiMH 6 V moteurs</td>
      <td>Alimentation dédiée à la propulsion</td>
      <td>utilisé</td>
      <td><a href="https://www.amazon.ca/dp/B08H1VGPTQ?ref=ppx_yo2ov_dt_b_fed_asin_title">Batterie NiMH 6 V</a></td>
      <td>Alimente les deux moteurs</td>
    </tr>
    <tr>
      <td>Pack de 6 piles NiMH logique</td>
      <td>Alimentation de tout le reste sauf des moteurs</td>
      <td>utilisé</td>
      <td><a href="https://ca.robotshop.com/fr/products/piles-aa-rechargeables-tenergy-pro-2800-mah-nimh-4x?variant=42796589908119">6 piles AA NiMH</a> dans un
      <a href="https://ca.robotshop.com/fr/products/support-piles-6-aa-inclus-interrupteur?variant=42411569741975">boitier</a>
      </td>      
      <td>Ce n'est pas la source la plus optimale, mais c'est ce que j'avais à ma portée.</td>
    </tr>
    <tr>
      <td>Carte d’alimentation sur perfboard</td>
      <td>Distribution des tensions</td>
      <td>utilisé</td>
      <td>Assemblage maison sur perfboard</td>
      <td>Élément architectural important, mais pas beaucoup illustré ni documenté.</td>
    </tr>
    <tr>
      <td>Pololu 4091 (D36V50F5)</td>
      <td>Régulation 5 V dans la carte d’alimentation</td>
      <td>utilisé</td>
      <td><a href="https://www.pololu.com/product-info-merged/4091">Pololu 4091</a></td>
      <td>Régulateur structurant de l’alimentation logique principale.</td>
    </tr>
    <tr>
      <td>Pololu 4090 (D36V50F3)</td>
      <td>Régulation 3,3 V dans la carte d’alimentation</td>
      <td>utilisé</td>
      <td><a href="https://www.pololu.com/product-info-merged/4090">Pololu 4090</a></td>
      <td>Complète la carte d’alimentation pour les éléments qui exigent du 3,3 V.</td>
    </tr>
    <tr>
      <td>Grove Ultrasonic Ranger</td>
      <td>Détection d’obstacles à courte portée</td>
      <td>prévu</td>
      <td><a href="https://wiki.seeedstudio.com/Grove-Ultrasonic_Ranger/">Seeed Grove Ultrasonic Ranger</a></td>
      <td>Le capteur est déjà monté, mais pas encore connecté ni programmé dans l’architecture actuelle.</td>
    </tr>
    <tr>
      <td>Servomoteur Hitec HS-422</td>
      <td>Orientation du capteur ultrason pour le balayage avant-gauche-droite</td>
      <td>prévu</td>
      <td><a href="https://hitecrcd.com/hs-422-deluxe-standard-servo/?setCurrencyId=1">Hitec HS-422</a></td>
      <td>Ce servo donne une logique simple de perception active sans ajouter tout de suite un LiDAR.</td>
    </tr>
    <tr>
      <td>RPLIDAR A2</td>
      <td>Perception 360 et préparation du positionnement</td>
      <td>prévu</td>
      <td><a href="https://www.slamtec.com/en/Lidar/A2/">Slamtec RPLIDAR A2</a></td>
      <td>Présent dans la trajectoire du projet, mais pas encore intégré matériellement ni logiciellement.</td>
    </tr>
    <tr>
      <td>Module audio I2S MAX98357</td>
      <td>Sortie audio embarquée</td>
      <td>utilisé</td>
      <td><a href="https://www.analog.com/en/products/max98357a.html">MAX98357A</a></td>
      <td>Les sources citent un module TENSTAR basé sur cette puce. TODO - Ajouter hyperlien : module exact utilisé.</td>
    </tr>
    <tr>
      <td>Haut-parleur Visaton BF37 5 W, 8 Ohms</td>
      <td>Restitution sonore derrière la face avant</td>
      <td>utilisé</td>
      <td><a href="https://www.visaton.de/en/products/drivers/fullrange-systems/bf-37-8-ohm">Visaton BF 37 - 8 Ohm</a></td>
      <td>Visible dans les notes photo. Montre que le robot intègre déjà une petite chaîne audio.</td>
    </tr>
    <tr>
      <td>Raspberry Pi 5</td>
      <td>Ancienne piste pour augmenter la marge de calcul</td>
      <td>abandonné</td>
      <td><a href="https://www.raspberrypi.com/products/raspberry-pi-5/">Raspberry Pi 5</a></td>
      <td>Abandonné comme référence de travail à cause des contraintes d’alimentation et des avertissements d’undervoltage.</td>
    </tr>
    <tr>
      <td>Raspberry Pi 3B+</td>
      <td>Étape intermédiaire plus réaliste énergétiquement</td>
      <td>abandonné</td>
      <td><a href="https://www.raspberrypi.com/products/raspberry-pi-3-model-b-plus/">Raspberry Pi 3 Model B+</a></td>
      <td>Alimentation plus tenable, mais performances et mémoire jugées trop limitées pour le confort de développement visé.</td>
    </tr>
    <tr>
      <td>ESP32</td>
      <td>Ancienne piste pour la commande moteur et les encodeurs</td>
      <td>abandonné</td>
      <td><a href="https://www.espressif.com/en/products/socs/esp32">ESP32 chez Espressif</a></td>
      <td>Visible dans des photos plus anciennes, mais remplacé par le Pico WH dans l’architecture de référence.</td>
    </tr>
  </tbody>
</table>


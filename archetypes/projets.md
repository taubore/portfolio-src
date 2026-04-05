+++
date = '{{ .Date }}'
draft = true
title = '{{ replace (path.Base .File.Dir) "-" " " | title }}'
description = ""
summary = ""
tags = []
categories = ["Projets"]
status = "À documenter"
+++

<!-- Nommer l’image principale avec "thumbnail" ou "cover" pour que BlowFish la réutilise automatiquement dans les listes. -->

## Résumé
Présenter le projet en quelques phrases, avec son objectif réel et ce qu'il permet d'apprendre.

## Informations clés
- **Type de projet** :
- **Objectif principal** :
- **Architecture actuelle** :
- **Système d'exploitation, langage et framework** :
- **État** :

## État actuel
Expliquer ce qui fonctionne déjà, ce qui reste en cours et les limites importantes à garder en tête.

## Principaux composants
- TODO - Ajouter hyperlien : composante principale

## Choix techniques et apprentissages
Décrire les décisions concrètes, les contraintes, les essais utiles, les erreurs et les corrections importantes.

## Chronologie
### {{ .Date.Format "2006-01-02" }} - Point de départ
Documenter l'étape correspondante de façon synthétique.

## Prochaines étapes
- ...

---
title: Nous aider
---

***
La documentation du projet ShadowHive est hebergée sur [github](https://github.com/Loe159/pst) et publiée sur ce site grâce à [Quartz](https://quartz.jzhao.xyz/). Si vous souhaitez contribuer à la documentation de ShadowHive, vous pouvez suivre les étapes ci-dessous. 

## Installation

> [!warning] Prérequis
> 
>Avant de commencer, assurez-vous d'avoir installé `git`, [Node](https://nodejs.org) >= v18.14 et `npm` >= v9.3.1 sur votre système.

Dans le terminal de votre choix, exécutez les commandes suivantes :
```shell
git clone https://github.com/Loe159/ShadowHive.git
cd ShadowHive
npm i
```

Pour développer la documentation du projet, je vous conseille d'ouvrir le dossier `/content` dans Obsidian. C'est ce dossier qui comporte tous les fichier markdowns. Ils seront transformés automatiquement grâce à quartz.

## Build et prévisualisation
Vous pouvez prévisualiser les changements de la documentation en temps réelle avec la commande :
```shell
npx quartz build --serve
```

Vous pouvez ensuite visiter http://localhost:8080 pour voir le rendu.

## Synchronisation
Pour synchroniser votre contenu avec celui-ci, il suffit d'exécuter la commande :
```shell
npx quartz sync
```

## Aide supplémentaire
Pour toute question supplémentaire, vous pouvez consulter la documentation de [Quartz](https://quartz.jzhao.xyz/)
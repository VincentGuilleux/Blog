---
title: "Goûts d’Fruits"
date: 2020-07-12T16:05:57+02:00
draft: false
---

Un site concret valant mieux qu’un long post de blog, rendez-vous [ici](https://www.goutsdfruits.fr) pour le visualiser et sur [GitHub](https://github.com/VincentGuilleux/goutsdfruits) pour le code source.

Comme indiqué dans mon dernier post, il s’agit donc de la première version du site initié en fin de formation que j’ai continué à développer avec l’aide ponctuelle d’une membre de notre groupe projet du Wagon (merci Anne !).

Ce site est utilisé par Marie, une amie de ma femme qui est maraîchère. Il a une triple vocation :
* Présenter la ferme et les produits
* Permettre aux clients de passer des commandes en ligne
* Être utilisé par Marie pour le pilotage de son activité : suivi des commandes, des stocks et des clients

En effet, Marie ne disposait jusque là que d’un site vitrine et consacrait énormément de temps à l’administratif au détriment de son exploitation : prise des commandes, gestion des stocks… En l’absence d’un outil centralisé, cela passait par de multiples fichiers Excel voire posts-its avec tous les problèmes inhérents à ce type de process.

La poursuite de ce projet m’a permis de mettre en œuvre tout de suite ce que j’avais appris pendant ma formation et aussi de m’attaquer à des nouveaux sujets. Et effectivement, c’est beaucoup plus formateur et gratifiant de travailler sur un projet concret que de faire des exercices de code.

La stack utilisée pour la mise en œuvre du site est la suivante :
* HTML / CSS / Bootstrap
* Javascript
* Ruby / Ruby on Rails
* CleverCloud pour l'hébergement

Les principales problématiques techniques que j’ai eu à implémenter sont :
* Mécanismes d’authentification et d’autorisation différenciés en fonction du profil utilisateur : client ou maraîcher
* 2 prix et unités de volume de vente distincts par produits : pour les clients particuliers / magasins
* Renseignement lors de la constitution des stocks d’une date de péremption (=> lots non visibles pour les clients si date de péremption dépassée, alerte pour le maraîcher si date de péremption proche…)
* MAJ automatique des lots de stocks de produits en fonction des prises de commande et des annulations (logique FIFO)
* Implémentation d’un statut pour chaque commande (en cours / préparée / livrée payée) qui est mis à jour par la maraîchère
* Mise en place d’un tableau de bord pour la maraîchère synthétisant sur une page les informations et chiffres clés
* Export en format Excel de la base de données
* Site responsive pour mobile

Dans le prochain post, je détaillerai les points non techniques auxquels j'ai été confronté qui étaient fondamentaux pour la réussite du projet.


Pour conclure de façon visuelle, une copie d’écran du dashboard :

![Dashboard](/post4/dashboard.png)

Ainsi que le schéma de la base de données :


![Database](/post4/database.png)

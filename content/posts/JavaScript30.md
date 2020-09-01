---
title: "JavaScript30"
date: 2020-08-23T14:52:20+02:00
draft: false
tags: [JavaScript]
---

Parmi les conseils de fin de formation du Wagon, on nous a conseillé [ce tutoriel](https://courses.wesbos.com/account) pour approfondir JavaScript. En effet, durant le bootcamp, en dehors des projets, seule une semaine était exclusivement consacrée à ce langage. Or comme ce dernier est incontournable pour le développement Web, il me semblait important d'acquérir des bases sûres en pur JS avant de m'attaquer si besoin à des frameworks style React.

Vous trouverez mes réponses aux différents exercices sur mon [GitHub](https://github.com/VincentGuilleux/JavaScript30).

J'ai trouvé le format assez ludique et le contenu bien adapté à mon niveau sur JS. J'ai finalisé 2/3 des exercices à aujourd'hui. Ceux-ci m'ont permis de mieux comprendre certains points abordés en formation et d'acquérir de nouvelles compétences. Vous trouverez ci-dessous certains de ces éléments :
* Non-équivalence entre les 2 syntaxes possibles de déclaration des fonctions en JS ("classique" vs arrow function) du fait de la différence de traitement du keyword this entre les 2 syntaxes. Il conviendra de privilégier la syntaxe classique en cas de méthodes d'objet et de fonctions callback avec un contexte dynamique (par exemple dans le cas d'un EventListener). Pour des explications complètes, j'ai trouvé cet [article](https://www.freecodecamp.org/news/when-and-why-you-should-use-es6-arrow-functions-and-when-you-shouldnt-3d851d7f0b26/) bien construit.
* Les différentes méthodes d'itération : reduce, map, filter, sort... (et sujets connexes comme par exemple comment convertir une NodeList en array)
* localStorage : stockage web qui permet aux sites et applications JavaScript de stocker et d'accéder à des données directement dans le navigateur, sans date d'expiration.
* La différence entre une référence à un array et une copie de l'array, point important car si une référence à un array est mise à jour, l'array d'origine sera aussi modifié ce qui ne sera pas le cas si c'est une copie de l'array qui est modifiée.
* Perfectionnement dans la syntaxe des QuerySelector et EventListener associés. En particulier, j'ai découvert le concept d'[Event Delegation](https://javascript.info/event-delegation) qui permet dans le cas d'éléments dynamiques (une liste initialement vide par exemple que l'utilisateur peut amender) de plutôt rattacher l'EventListener à l'élément parent. Il est alors possible par exemple dans la fonction associée via une méthode match() sur l'event.target d'effectuer une opération sur l'élément enfant JS => Cette façon de procéder fonctionne quelque soit la taille de la liste (vide, 2 ou plein d'éléments...) ce qui ne serait pas le cas si on associait la méthode addEventListener() directement à chacun des éléments enfants.

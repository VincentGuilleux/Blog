---
title: "Hugo"
date: 2020-07-30T13:56:12+02:00
draft: false
tags: [Hugo]
---

Le sujet du jour : comment créer son blog avec [Hugo](https://gohugo.io/), un générateur open-source de sites Web statiques. C'est avec cet outil que j'ai construit ce blog.

Je ne vais pas détailler ici toutes les étapes de création et de personalisation car les tutos Hugo et articles de blog sur le sujet expliquent très bien les différentes étapes. Vous trouverez donc ci-dessous les différents éléments que j'ai implémenté sur ce blog avec les liens correspondants et si nécessaire quelques explications complémentaires sur certains points.
NB : tous les outils que je décris ci-dessous sont gratuits.

* Quick start : https://gohugo.io/getting-started/quick-start/
Le point de départ pour créer votre blog avec Hugo. Vous choisissez en particulier ici un [thème](https://themes.gohugo.io/) de base pour votre layout. Ol est important de se référer à la page dédiée pour vérifier les spécificités du thème en question (support Turbolinks, responsive, langages, taxonomies, librairie CSS...)

* Déploiement sur GitHub : vous pouvez vous référer à la [documentation Hugo](https://gohugo.io/hosting-and-deployment/hosting-on-github/) et je vous conseille également [cet article](https://inside.getambassador.com/creating-and-deploying-your-first-hugo-site-to-github-pages-1e1f496cf88d). Quel intérêt me direz-vous ? C'est expliqué juste en dessous.

* Hébergement sur Netifly : J'ai choisi Netifly pour l'hébergement de mon blog, notamment pour le 'continuous deployment' qui permet une mise à jour automatique du site à chaque push sur GitHub. La encore, le [tuto Hugo](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/) est assez explicite. Donc aucune manipulation complémentaire à faire une fois la mise à jour du site pushée sur GitHub, Netifly se charge automatiquement et quasi-instantanément du déploiement sur votre nom de domaine.

* Personnalisation du layout de votre thème :
Vous pouvez 'overrider' le CSS de base du thème que vous avez choisi. La façon de procéder dépend dudit thème donc référez vous à sa doc.
Pour ma part, je n'ai pas créé de surcouche CSS spécifique mais préféré modifier les classes CSS directement dans les fichiers partials concernés du thème afin de conserver une arborescence simple. C'était possible dans mon cas car le thème Ananke utilise la librairie CSS [Tachyons](http://tachyons.io/) qui contient de multiples classes (sizing, padding..., un peu à l'image de bootstrap), du coup j'ai pu modifier directement lesdites classes dans les fichiers HTML sans avoir à créer de nouvelles classes CSS.
Pour ce faire, une chose importante à retenir : ne pas modifier directement les fichiers du thème stockés dans _themes/themename/_ mais les copier à la racine de votre dossier en conservant l'arborescence initiale. Par exemple, si vous voulez modifier le header par défaut du thème ananke stocké dans _ananke/layouts/partials/site-header.html_, copiez ce fichier dans _layouts/partials/_ et modifiez la version dupliquée. Sinon, de ma petite expérience, vous allez au devant de quelques problèmes :) (en outre, cela posera nécessairement problème en cas de mise à jour du thème). Du coup, vous vous retrouvez dans _/layouts/_ uniquement avec les fichiers que vous avez modifié et ceux-ci vont automatiquement être utilisés pour construire les pages de votre site à la place de ceux stockés dans le répertoire du thème.
Les noms des fichiers sont explicites, [à retenir notamment](https://gohugo.io/templates/base/) les fichiers suivants :
    * le modèle html de base (pour toutes les pages du site) : *layouts/_default/baseof.html*
    * le fichier html pour un post individuel : *layouts/_default/single.html*

* Ajout de tags pour catégoriser vos posts : afin qu'un utilisateur puisse lister tous les posts relatifs à un sujet donné. Pour implémenter cette fonctionnalité appelée 'taxonomies' dans Hugo, rien de bien sorcier, vous pouvez suivre par exemple [ce tuto](https://www.jakewiesler.com/blog/hugo-taxonomies). A noter que le recours à ces tags génère automatiquement une page _nomdusite/tags/_ listant l'ensemble des articles classés par tag ainsi qu'une page par tag dans _nomdusite/tags/tagname_.

* Ajout d'un formulaire de contact : j'ai utilisé [Formspree](formspree.io) comme proxy pour l'envoi de l'email. Là aussi, c'est très simple à implémenter, recopier le code HTML fourni par Formspree et customizer le layout (dans ce cas, j'ai trouvé utile de créer un fichier CSS dédié que j'ai donc rajouté à mon fichier config.toml comme expliqué [ici](https://themes.gohugo.io/gohugo-theme-ananke/#custom-css).

* Ajout de commentaires : j'ai implémenté [Disqs](https://disqus.com/) récemment car c'est gratuit (moyennant pub) et très facile à implémenter dans un site statique Hugo ([2 lignes de code suffisent](https://gohugo.io/content-management/comments/)). Mais je l'ai retiré assez vite car en fouillant un peu, de nombreux utilisateurs se plaignent pour de multiples raisons (lenteur, tracking, nécessité d'avoir un compte Disq pour commenter...). Et à l'usage, ces bandeaux de pub sont quand même très moches et rappellent à mon goût un peu trop les sites de la fin des années 90 :) Bref, j'ai regardé les alternatives et j'essaierai d'en implémenter une prochainement.

Au final, l'utilisation d'Hugo m'a convaincu. En effet, j'ai trouvé assez simple et rapide de construire son blog ainsi tout en laissant la possibilité de le personnaliser à sa guise. Cela m'a permis sinon à titre perso de me replonger un peu dans des sujets front-end et de découvrir des services clés en main à implémenter sur de tels sites statiques (Formspree, Disqs ou équivalent...).


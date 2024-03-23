# SRC_JS-StartProject_Studies-01
Version d'étude issue de la vidéo Youtube de Thomas Mouchelet

## Ce que fait le projet
Le projet est un développement linéaire (étape par étape) qui consiste à se familliariser avec le framework Vue.Js en 
réalisant par étape successive l'initialisation du développement, la création des données, puis la gestion événementielle 
des likes et des commentaires de chaque carte.
Chaque carte contient une image, un titre, un texte explicatif, un compteur de _like_ et des commentaires.

## Pourquoi le projet est utile
Le projet permet de réaliser :
  1. un développement dans Vue.Js
  2. la création de données fictives (fake datas)
  3. d'exploiter les directives "v-..." de Vue.Js
  4. d'exploiter la gestion des événements
  5. d'exploiter les style _flex_

## Les différentes étapes
### Etape 1 : initialisation avec la mise en place de *Vue.Js*
- Ajout d'un code VueJs 'without Build Tools' (version simplifiée issue de 'using the global build')
  - [Guide Quick Start de vuejs.org](https://vuejs.org/guide/quick-start.html#creating-a-vue-application)
  - [Pour comprendre l'expression 'mount'](https://vuejs.org/guide/essentials/lifecycle.html)

### Etape 2 : création de données (fictives) et chargement en mémoire
- Création de données pour exploitation
  - Création de données de travail avec https://jsonplaceholder.typicode.com/
    - utilisation de données `/posts` (100 posts)
        
  - Dans `html/createApp`, charger les données de l'API REST avec 'mounted()'

### Etape 3 : création des _cartes_
- Afficher les données `data` dans notre Vue
  - remplacer dans `data()`, la donnée "`message: 'Hello Vue`" par une nouvelle donnée (tableau vide) "`postList: []`"
  - supprimer dans le rendu de `#app` la donnée "`{{ message }}`" - qui n'existe plus !
  - remplacer le message `console.log` par une insertion (`push()`) des données Json dans la données `postList`
    - utilisation du contexte `this` pour accéder au tableau `postList`
    - utilisation de la syntaxe de décomposition (spread syntax) en utilisant le `push()`
      - codes équivallents : `this.postList.push(...data) <=> this.postList = data`
  - afficher les données récupérées dans l'Id `app`
    - création d'une `section` contenant une classe `row`, `col` et `card`
    - la classe `card` contient une image et un `card-body`
    - la classe `card-body` contient un titre `h5` et un paragraphe `card-text`
    - dupliquer les `col` plusieurs fois (Alt+Shift+Flèche bas)
        
- pour le débug dans le navigateur, ajouter un outil '`Vue.js devtools`'
  - fait pour Chrome et FireFox : ne fonctionne pas pour Chrome (pas d'explication...)

- pour les images utiliser un créateur d'image (recherche : fake img api)
  - création des données images avec https://picsum.photos/
    - utilisation pour l'image du code source 'https://picsum.photos/200/300'

### Etape 4 : mettre du style aux _cartes_
- mettre un style aux `.card` de notre Vue
  - créer un ficher style.scss (fichier en SASS)
    - pour compiler le Sass (*.scss) en CSS (*.css), utilisation d'une extension VSCode '_Live Sass Compiler_'
      - utiliser la méthode d'installation demandée : Ctrl+P puis code '_ext install glenn2223.live-sass_'
    - pour `.card` faire un style en Sass, puis le compiler en utilisant '`Watch Sass`' du menu bas pour obtenir 'style.css'
  - créer le lien '`style.css`' dans '`index.html`'
    - disposer les éléments `.card` avec une disposition `flex` dans le 'style.scss'

### Etape 5 : afficher toutes les _cartes_ avec les données chargées en mémoire
- exploiter les données de `postList` pour les afficher en élément `.card`
  - suppression des éléménts `.col` qui ont été dupliqués (il faut n'en garder qu'un seul pour conserver la structure dans le DOM)
  - utiliser la directive `v-for` de Vue.Js (documentation par recherche de : '`v-for dans vue.js`') pour les éléménts `.col`
    - Documentation [Guide VueJs : list](https://v2.fr.vuejs.org/v2/guide/list.html)
  - la directive `v-for` permet de parcourir `postList` par `myPostItem` avec la clé de parcourt `myPostItem.id` (structure fourni lors du post)
    - compléter les éléments `.card-title` avec la structure déclarative `{{ myPostItem.title }}`
    - compléter les éléments `.card-text` avec la structure déclarative `{{ myPostItem.body }}`

### Etape 6 : compléter chaque _carte_ avec un compteur de _likes_ 
- compléter les éléments `.card` avec un '`card-footer`
  - le `.card-footer` contien un "bouton de like" et un "compteur de like" avec un style '`flex`'
  - améliorer le style du "bouton de like"

### Etape 7 : compter les _likes_ pour chaque carte
- compter les "like" avec une gestion d'événement dans Vue
  - recherche documentation '`event vuejs`' (document : https://v2.fr.vuejs.org/v2/guide/events.html)
    - ajout de l'instruction `v-on` de gestion d'événement `click` sur le bouton de `.card-footer` en déclenchant une méthode '`ddLike(myItemPost)`
      - déclaration de la "méthode `addLike(myItemPost)`" dans la Vue `createApp`
      - la méthode `addLike(myItemPost)` identifie un champ `likes` dans la structure `postList` (visualisation possible avec '`Vue.js devtools`')
    - gestion du compteur de likes (élément `span` de `.card-footer`)

### Etape 8 : ajouter à chaque carte une liste de commentaires
- ajouter des commentaires pour chaque `.card`
  - pour chaque élémnet `.card`, ajouter un élément `.comments` dans `postList`
    - ajouter un formulaire `form` sans action et comprenant un `input`
      - mettre un style adapté pour ce formulaire (la classe `.comment` doit être placée à la racine ! **Raison non comprise !**)
    - gestion d'un événement de soumission du formulaire avec `v-on: submit` associé à une méthode `addComment()` dans la Vue `createApp`
      - pour éviter le rechargement de la page (lors de la soumission), il faut utiliser `submit.prevent`
        - pour ajouter un commentaire sur l'élémént `.card`, il faut préciser `myPostItem` et avoir le contenu de la soumission avec l'événement `event`
        - la valeur du commentaire `myValue` est le premier élément `.elements[0].value` de l'événement cible `event.target`
        - Le commentaire est inséré dans un élément structuré `myComment` comprenant `{ id, body }` 
  - afficher les commentaires dans chaque élément `.card`
    - ajouter un élément `.commentsList` dans l'élément `.Comments`
    - la directive `v-for` permet de parcourir mes commentaires `myPostItem.comments` par `myCommentItem` avec la clé de parcourt `myCommenttItem.id`
      - la structure finale est la suivante : **postList [ i ] { userId, id, title, body, likes, comments { id, body} }**

### Etape 9 : axes d'amélioreation
- Quelques idées d'amélioration
  -mettre des 'likes' par 'commentaire'
  - plusieurs photos et carrousel par élément `.card`
  - gérer l'affichage pour réduire la hauteur de la page
  - adapter le nombre de colonne en fonction de la largeur de la page
  - améliorer le **README.ms**
        
## Remerciements
Débutant en développement en HTML, CSS et JavaScript, ce projet constitue mon premier développement sous Vue.Js.

Je remercie Thomas Mouchelet pour sa vidéo sur YouTube qui m'a permis de comprendre rapidement et simplement comment mener les étapes de ce projet.

- Vidéos à l'origine du projet :
  - [#1 - Vuejs 3, projet pour débuter - Thomas Mouchelet - YouTube](https://www.youtube.com/watch?v=IMLFPPVrn3w)
  - [#2 - Vuejs 3, projet pour débuter - Thomas Mouchelet - YouTube](https://www.youtube.com/watch?v=H5tOffytJ-Q)

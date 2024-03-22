# SRC_JS-StartProject_Studies-01
Version d'étude issue de la vidéo Youtube de Thomas Mouchelet

Etape 1 :
    - Ajout d'un code VueJs 'without Build Tools' (version simplifiée issue de 'using the global build')
        => lien : https://vuejs.org/guide/quick-start.html#creating-a-vue-application

        => Pour comprendre l'expression 'mount' : https://vuejs.org/guide/essentials/lifecycle.html

Etape 2 :
    - Création de données pour exploitation
        => Création de données de travail avec https://jsonplaceholder.typicode.com/
            >> utilisation de données '/posts' (100 posts)
        
        => Dans 'html/createApp', charger les données de l'API REST avec 'mounted()'

Etape 3 :
    - Afficher les données 'data' dans notre Vue
        => remplacer dans data(), la donnée " message: 'Hello Vue' " par une nouvelle donnée (tableau vide) " postList: [] "
        => supprimer dans le rendu de '#app' la donnée "{{ message }}" - qui n'existe plus !
        => remplacer le message 'console.log' par une insertion ('push()') des données Json dans la données 'postList'
            +=> utilisation du contexte 'this' pour accéder au tableau 'postList'
            +=> utilisation de la syntaxe de décomposition (spread syntax) en utilisant le push()
                    ++=> codes équivallents : this.postList.push(...data) <=> this.postList = data
        => afficher les données récupérées dans l'Id 'app'
            +=> création d'une 'section' contenant une classe 'row, 'col' et 'card'
            +=> la classe 'card' contient une image et un 'card-body'
            +=> la classe 'card-body' contient un titre 'h5' et un paragraphe 'card-text'
            +=> dupliquer les 'col' plusieurs fois (Alt+Shift+Flèche bas)
        
    - pour le débug dans le navigateur, ajouter un outil 'Vue.js devtools'
        => fait pour Chrome et FireFox : ne fonctionne pas pour Chrome

    - pour les images utiliser un créateur d'image (recherche : fake img api)
        => création des données images avec https://picsum.photos/
            >> utilisation pour l'image du code source 'https://picsum.photos/200/300'

Etape 4 :
    - mettre un style aux '.card' de notre Vue
        => créer un ficher style.scss (fichier en SASS)
            +=> pour compiler le Sass (*.scss) en CSS (*.css), utilisation d'une extension VSCode 'Live Sass Compiler'
                >> utiliser la méthode d'installation demandée : Ctrl+P puis code 'ext install glenn2223.live-sass.'
            +=> pour '.card' faire un style en Sass, puis le compiler en utilisant 'Watch Sass' du menu bas pour obtenir 'style.css'
        => créer le lien 'style.css' dans 'index.html'
    - disposer les éléments '.card' avec une disposition 'flex' dans le 'style.scss'

Etape 5 :
    - exploiter les données de 'postList' pour les afficher en élément '.card'
        => suppression des éléménts '.col' qui ont été dupliqués (il faut n'en garder qu'un seul pour conserver la structure dans le DOM)
        => utiliser la directive 'v-for' de Vue.Js (documentation par recherche de : 'v-for dans vue.js') pour les éléménts '.col'
            >> Documentation : https://v2.fr.vuejs.org/v2/guide/list.html
            +=> la directive 'v-for' permet de parcourir 'postList' par 'myPostItem' avec la clé de parcourt 'myPostItem.id' (structure fourni lors du post)
            +=> compléter les éléments '.card-title' avec la structure déclarative {{ myPostItem.title }}
            +=> compléter les éléments '.card-text' avec la structure déclarative {{ myPostItem.body }}

Etape 6 :
    - compléter les éléments '.card' avec un '.card-footer'
        => le '.card-footer' contien un "bouton de like" et un "compteur de like" avec un style 'flex'
            +=> améliorer le style du "bouton de like"
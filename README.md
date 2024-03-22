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

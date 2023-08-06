---
description: Optimisez son style avec sass,scss ? comment ça fonctionne ?
---

# 05-Sass

Sass (Syntactically Awesome Style Sheets) est un langage de feuille de style préprocesseur qui étend la syntaxe du CSS. Il permet aux développeurs d'écrire du CSS de manière plus organisée, maintenable et puissante en utilisant des fonctionnalités avancées telles que les variables, les fonctions, les boucles et les mixins. SCSS (Sassy CSS) est une syntaxe de Sass qui ressemble davantage au CSS traditionnel et est compatible avec tous les navigateurs.

Voici comment **Sass**/**SCSS** fonctionne et comment il peut être utilisé pour optimiser le style de vos feuilles de style :

1. Installation et configuration :
   * Pour utiliser Sass/SCSS, vous devez d'abord l'installer sur votre machine. Cela peut se faire via npm (Node Package Manager) en installant le package `sass` globalement ou localement dans votre projet.
   * Une fois installé, vous pouvez commencer à utiliser Sass/SCSS en créant des fichiers avec l'extension .scss.
2.  Utilisation des variables :

    * Les variables Sass/SCSS permettent de stocker des valeurs réutilisables, comme des couleurs, des tailles de police, des marges, etc. Cela facilite la maintenance du code, car vous pouvez simplement modifier la valeur de la variable pour mettre à jour toutes les occurrences dans le code.
    * Exemple :

    ```scss
    $primary-color: #007bff;

    body {
      background-color: $primary-color;
    }
    ```
3.  Utilisation des **mixins**&#x20;

    * Les mixins permettent de regrouper un ensemble de propriétés CSS dans un seul bloc et de les réutiliser sur différentes sélecteurs. Cela permet de réduire la duplication de code et de faciliter les changements de style cohérents.
    * Exemple :

    ```scss
    @mixin rounded-border($radius) {
      border-radius: $radius;
    }

    .button {
      @include rounded-border(5px);
    }

    .card {
      @include rounded-border(10px);
    }
    ```
4.  Utilisation des **fonctions** et des **opérations** :

    * Sass/SCSS permet également d'utiliser des fonctions pour effectuer des opérations mathématiques, des manipulations de chaînes, des couleurs, etc. Cela permet d'ajouter de la logique au style et de rendre le code plus dynamique.
    * Exemple :

    ```scss
    $base-font-size: 16px;

    body {
      font-size: $base-font-size;
    }

    h1 {
      font-size: $base-font-size * 2;
    }
    ```
5.  **Importation** de fichiers :

    * Sass/SCSS permet d'importer des fichiers partiels dans un fichier principal, ce qui facilite l'organisation du code en plusieurs fichiers pour des parties spécifiques du site. Cela améliore la lisibilité et la maintenabilité du code.
    * Exemple :

    ```scss
    // Fichier main.scss
    @import 'variables';
    @import 'mixins';
    @import 'styles';
    ```
6.  **Compilation** :

    * Pour que les navigateurs puissent interpréter le code Sass/SCSS, il doit être compilé en CSS. Vous pouvez compiler manuellement à l'aide de la commande Sass dans votre terminal ou en utilisant des outils automatisés comme Webpack, Gulp ou Grunt.


7.  Contrôle des sélecteurs CSS :

    * Sass/SCSS offre des fonctionnalités pour contrôler les sélecteurs CSS générés, ce qui permet d'éviter les sélecteurs redondants et d'augmenter la spécificité. Cela aide à écrire un code CSS plus modulaire et maintenable.
    * Exemple :

    ```scss
    .container {
      h1 {
        font-size: 24px;
      }
      p {
        font-size: 16px;
      }
    }
    ```
8.  Utilisation des opérateurs de condition :

    * Sass/SCSS propose des opérateurs de condition, tels que `if()`, `else if()`, `else`, qui permettent d'ajouter de la logique conditionnelle dans le code CSS. Cela peut être utile pour gérer différents styles en fonction de certains critères.
    * Exemple :

    ```scss
    $dark-theme: true;

    body {
      background-color: if($dark-theme, #333, #fff);
    }
    ```
9.  Modularité et architecture :

    * Sass/SCSS encourage une approche modulaire dans la conception des feuilles de style, en divisant le code en plusieurs fichiers partiels, chacun ayant une responsabilité spécifique. Cela rend le code plus facile à gérer et à maintenir, en particulier pour les grands projets.
    * Exemple de structure de fichiers :

    ```css
    styles/
    ├── _variables.scss
    ├── _mixins.scss
    ├── _typography.scss
    ├── _layout.scss
    └── main.scss
    ```
10. Autres fonctionnalités avancées&#x20;

* Sass/SCSS propose une variété d'autres fonctionnalités avancées, telles que les boucles, les maps, les fonctions personnalisées, les imports conditionnels, etc. Ces fonctionnalités rendent le langage très puissant et flexible pour gérer des cas d'utilisation complexes.

En utilisant Sass/SCSS, vous pouvez considérablement améliorer l'efficacité et la maintenabilité de votre code CSS. Les fonctionnalités telles que les variables, les mixins, les fonctions et l'importation de fichiers permettent de réduire la duplication de code, d'organiser le code de manière modulaire, et d'ajouter de la logique dans le style. Cela facilite la gestion des styles sur de grands projets et permet de créer des feuilles de style optimisées et évolutives.

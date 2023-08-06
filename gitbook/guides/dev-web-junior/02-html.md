---
description: C'est quoi le balisage ? Comment fonctionne une page web.
---

# 02-Html

Le balisage, en informatique et en développement web, fait référence à l'utilisation de balises pour marquer et structurer le contenu d'un document. Dans le contexte du développement web, le balisage est utilisé pour créer des pages web en définissant la structure, le contenu et le style du document. Le balisage est réalisé en utilisant des langages de balisage tels que HTML (Hypertext Markup Language) pour structurer le contenu et CSS (Cascading Style Sheets) pour le styliser.

Voici comment fonctionne une page web :

1. Structure du document (HTML) :
   * Lorsque vous créez une page web, vous écrivez le code HTML pour définir la structure du document. Vous utilisez des balises HTML pour indiquer les différents éléments de la page tels que les titres, les paragraphes, les images, les liens, les listes, les tableaux, etc.
   * Chaque balise a une signification et un rôle spécifique dans la page. Par exemple, la balise `<h1>` est utilisée pour les titres principaux, `<p>` pour les paragraphes, `<img>` pour les images, `<a>` pour les liens, etc.
   * Les balises HTML sont souvent imbriquées les unes dans les autres pour définir la hiérarchie et la structure de la page.
2. Mise en forme (CSS) :
   * Une fois que la structure de la page est définie avec le balisage HTML, vous pouvez utiliser des règles CSS pour styliser la page. Les règles CSS spécifient comment les éléments HTML doivent être affichés, tels que la couleur, la police, la taille, les marges, les espacements, etc.
   * Les règles CSS sont appliquées en utilisant des sélecteurs pour cibler les éléments spécifiques de la page. Par exemple, vous pouvez appliquer un style particulier à tous les éléments `<p>` en utilisant le sélecteur `p` dans vos règles CSS.
3. Affichage dans le navigateur :
   * Une fois que vous avez écrit le code HTML et CSS, vous enregistrez le fichier avec l'extension .html et l'ouvrez dans un navigateur web (comme Google Chrome, Mozilla Firefox, etc.).
   * Le navigateur interprète le code HTML et CSS et affiche la page web en conséquence. Il suit la structure et les règles de style pour rendre le contenu de la page visuellement dans la fenêtre du navigateur.
4. Interaction et JavaScript (facultatif) :
   * Si vous avez besoin d'ajouter des fonctionnalités interactives à votre page, vous pouvez utiliser JavaScript. JavaScript est un langage de programmation qui permet de créer des fonctionnalités dynamiques sur la page, telles que des boutons cliquables, des animations, des formulaires interactifs, etc.

En résumé, une page web fonctionne en utilisant le balisage HTML pour définir la structure du document et en utilisant les règles CSS pour styliser le contenu. Le navigateur interprète ensuite le code HTML et CSS pour afficher la page web à l'utilisateur. Le JavaScript peut également être utilisé pour ajouter des fonctionnalités interactives supplémentaires à la page.

***

#### Exemple

Voici un exemple simple d'une page web utilisant le balisage HTML, les règles CSS et le JavaScript pour créer une page interactive.

HTML (index.html)&#x20;

```html
<!DOCTYPE html>
<html>
<head>
  <title>Exemple de page web</title>
  <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>
  <h1>Bienvenue sur ma page web !</h1>
  <p>Cliquez sur le bouton ci-dessous pour changer la couleur du titre.</p>
  <button id="changeColorButton">Changer la couleur</button>

  <script src="script.js"></script>
</body>
</html>
```

CSS (styles.css) :

```css
body {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #f0f0f0;
}

h1 {
  color: blue;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
}
```

JavaScript (script.js) :

```js
document.getElementById("changeColorButton").addEventListener("click", function() {
  var title = document.querySelector("h1");
  var randomColor = getRandomColor();
  title.style.color = randomColor;
});

function getRandomColor() {
  var letters = "0123456789ABCDEF";
  var color = "#";
  for (var i = 0; i < 6; i++) {
    color += letters[Math.floor(Math.random() * 16)];
  }
  return color;
}
```

Dans cet exemple, nous avons créé une page web simple avec un titre (`<h1>`), un paragraphe (`<p>`) et un bouton (`<button>`). Le fichier CSS (styles.css) est utilisé pour styliser la page en définissant les couleurs et les styles des éléments. Le JavaScript (script.js) est utilisé pour ajouter une fonctionnalité interactive au bouton. Lorsque le bouton est cliqué, la couleur du titre (`<h1>`) change aléatoirement en utilisant la fonction `getRandomColor()`.

Notez que les trois fichiers HTML, CSS et JavaScript sont liés entre eux dans le fichier index.html en utilisant les balises `<link>` pour la feuille de style CSS et `<script>` pour le fichier JavaScript.

Lorsque vous ouvrez le fichier index.html dans votre navigateur, vous verrez la page web avec le titre et le paragraphe, ainsi qu'un bouton. Si vous cliquez sur le bouton, la couleur du titre changera de manière aléatoire à chaque clic.

***

#### Schéma

```
Dossier
├── index.html
├── styles.css
└── script.js
```


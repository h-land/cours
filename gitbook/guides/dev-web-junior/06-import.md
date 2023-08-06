---
description: >-
  Import de CDN, c'est quoi un framework ? Comment importer des librairy diverse
  ?
---

# 06-Import

1. Import de CDN : Un CDN (Content Delivery Network) est un réseau de serveurs répartis géographiquement qui permet de distribuer des ressources web, telles que des bibliothèques JavaScript, des fichiers CSS, des polices, des images, etc., à partir de serveurs situés physiquement plus près des utilisateurs. L'utilisation d'un CDN pour importer des ressources dans votre site web peut améliorer les performances en réduisant les temps de chargement et en garantissant une disponibilité élevée des fichiers.

Pour importer une bibliothèque ou une ressource depuis un CDN dans votre projet web, vous pouvez utiliser une balise `<script>` pour les fichiers JavaScript ou une balise `<link>` pour les fichiers CSS, avec l'attribut `src` pointant vers l'URL du fichier hébergé sur le CDN. Par exemple :

```html
<!-- Import de jQuery depuis un CDN -->
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

<!-- Import de Bootstrap CSS depuis un CDN -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
```

2. Framework : Un framework est un ensemble d'outils, de bibliothèques, de conventions et de modèles de conception préétablis qui fournissent une structure et une base pour développer des applications web plus rapidement et efficacement. Les frameworks permettent aux développeurs de se concentrer sur la logique métier plutôt que sur les détails techniques de bas niveau.

Il existe différents types de frameworks, tels que :

* Frameworks front-end : Utilisés pour développer l'interface utilisateur d'une application web, généralement basés sur HTML, CSS et JavaScript. Exemples : React, Angular, Vue.js.
* Frameworks back-end : Utilisés pour gérer la logique serveur et les requêtes HTTP. Exemples : Express.js, Django, Ruby on Rails.
* Frameworks full-stack : Combinent à la fois le front-end et le back-end pour offrir une solution complète de développement web. Exemples : Meteor, MEAN stack.

3. Import de bibliothèques diverses : Pour importer des bibliothèques diverses dans votre projet, vous pouvez également utiliser des CDN, comme décrit précédemment. Vous pouvez également télécharger les fichiers localement dans votre projet et les référencer dans votre code HTML ou CSS en utilisant des chemins relatifs.

Exemple d'import d'une bibliothèque JS depuis un fichier local :

```html
<!-- Import d'une bibliothèque JavaScript depuis un fichier local -->
<script src="js/ma_bibliotheque.js"></script>
```

Exemple d'import d'une bibliothèque CSS depuis un fichier local :

```html
<!-- Import d'une bibliothèque CSS depuis un fichier local -->
<link rel="stylesheet" href="css/ma_bibliotheque.css">
```

Lorsque vous importez des bibliothèques, assurez-vous de respecter les dépendances et les exigences spécifiées par la bibliothèque et de suivre les instructions d'installation et d'utilisation fournies par les auteurs de la bibliothèque.

En résumé, pour importer des ressources et des bibliothèques dans votre projet web, vous pouvez utiliser des CDN pour des ressources communes, ou télécharger les fichiers localement pour des bibliothèques spécifiques. Les frameworks, quant à eux, fournissent une structure et des outils pour développer des applications web plus rapidement et plus efficacement.

---
description: >-
  API Rest, Web services, ... ? c'est quoi ce charabia ? Qui partage ses outils
  ?
---

# 09-API

Une API REST (Representational State Transfer) et les web services sont des concepts essentiels dans le développement d'applications web. Voici des explications pour mieux comprendre :

1.  API REST (Representational State Transfer) : Une API REST est un style d'architecture pour concevoir des services web qui permettent à différentes applications de communiquer entre elles via Internet. Elle repose sur le protocole HTTP et définit des règles pour créer, lire, mettre à jour et supprimer (CRUD) des ressources exposées par le serveur. Les API REST utilisent généralement des méthodes HTTP telles que GET, POST, PUT et DELETE pour interagir avec les ressources.

    Une API REST utilise des URI (Uniform Resource Identifier) pour identifier les ressources et les verbes HTTP pour définir les actions à effectuer sur ces ressources. Les données sont souvent échangées au format JSON (JavaScript Object Notation) ou XML (eXtensible Markup Language).
2.  Web Services : Les web services sont des services accessibles via Internet qui permettent à différentes applications de communiquer et d'échanger des données. Ils utilisent généralement des protocoles standard tels que HTTP, SOAP (Simple Object Access Protocol), REST, XML-RPC, etc. pour permettre l'interopérabilité entre les différents systèmes.

    Les web services peuvent être de différents types, notamment :

    * SOAP (Simple Object Access Protocol) : Utilise XML pour structurer les données et les messages.
    * REST (Representational State Transfer) : Utilise le protocole HTTP et des URI pour interagir avec les ressources.
    * JSON-RPC : Utilise JSON pour les données et effectue des appels de procédure distante (RPC).
    * XML-RPC : Utilise XML pour les données et effectue des appels de procédure distante (RPC).

    Les web services sont largement utilisés dans le développement d'applications pour permettre l'intégration de différentes fonctionnalités et services provenant de différentes sources.
3.  Partage des outils : Dans le contexte du développement logiciel, le partage des outils fait référence à la pratique de mettre à disposition des développeurs et de la communauté des outils logiciels, des bibliothèques, des frameworks, des API, etc., qui peuvent être utilisés pour accélérer et faciliter le processus de développement.

    De nombreuses entreprises, organisations et développeurs partagent leurs outils avec la communauté open source, ce qui permet à d'autres développeurs de les utiliser, de les améliorer et de les adapter à leurs propres besoins. Le partage d'outils favorise la collaboration, l'efficacité et l'innovation dans le domaine du développement logiciel.

    Des plateformes de partage d'outils et de bibliothèques open source populaires, telles que GitHub, NPM (Node Package Manager), PyPI (Python Package Index), Maven (pour Java), etc., sont utilisées pour rendre les outils accessibles et faciles à intégrer dans les projets de développement.

En résumé, les API REST et les web services facilitent la communication entre différentes applications et services. Le partage d'outils open source est une pratique courante qui favorise la collaboration, l'innovation et l'enrichissement de la communauté du développement logiciel. Ces concepts sont essentiels pour le développement moderne d'applications efficaces et interconnectées.

***

### Exemple

Voici un exemple simple d'une application Node.js avec Express.js qui utilise une API REST pour gérer une liste de tâches (to-do list). Dans cet exemple, nous allons implémenter les opérations CRUD (Create, Read, Update, Delete) pour gérer les tâches.

Assurez-vous d'avoir Node.js et Express.js installés sur votre machine.

1. Créez un nouveau projet Node.js et installez Express.js :

```bash
bashCopy codemkdir node-express-todo
cd node-express-todo
npm init -y
npm install express
```

2. Créez un fichier `app.js` dans le répertoire du projet avec le contenu suivant :

```javascript
javascriptCopy codeconst express = require('express');
const app = express();
const port = 3000;

app.use(express.json());

// Tableau pour stocker les tâches (simulons une base de données en mémoire)
let tasks = [];

// Route pour récupérer toutes les tâches
app.get('/tasks', (req, res) => {
  res.send(tasks);
});

// Route pour créer une nouvelle tâche
app.post('/tasks', (req, res) => {
  const { description } = req.body;
  const newTask = { id: tasks.length + 1, description, completed: false };
  tasks.push(newTask);
  res.send('Tâche créée avec succès');
});

// Route pour mettre à jour une tâche par son ID
app.put('/tasks/:id', (req, res) => {
  const taskId = parseInt(req.params.id);
  const { description, completed } = req.body;
  const taskIndex = tasks.findIndex((task) => task.id === taskId);
  if (taskIndex !== -1) {
    tasks[taskIndex] = { ...tasks[taskIndex], description, completed };
    res.send('Tâche mise à jour avec succès');
  } else {
    res.status(404).send('Tâche non trouvée');
  }
});

// Route pour supprimer une tâche par son ID
app.delete('/tasks/:id', (req, res) => {
  const taskId = parseInt(req.params.id);
  tasks = tasks.filter((task) => task.id !== taskId);
  res.send('Tâche supprimée avec succès');
});

// Démarrage du serveur
app.listen(port, () => {
  console.log(`Serveur démarré sur http://localhost:${port}`);
});
```

3. Exécutez l'application :

```bash
bashCopy codenode app.js
```

L'application sera démarrée sur `http://localhost:3000`.

Maintenant que l'application est en cours d'exécution, vous pouvez utiliser un outil comme Postman pour effectuer les opérations CRUD sur la liste de tâches. Voici quelques exemples d'utilisation des routes avec Postman :

* Requête GET pour récupérer toutes les tâches : `GET http://localhost:3000/tasks`
*   Requête POST pour créer une nouvelle tâche : `POST http://localhost:3000/tasks` Body (raw, JSON) :

    ```json
    jsonCopy code{
      "description": "Acheter des fruits"
    }
    ```
*   Requête PUT pour mettre à jour une tâche par son ID : `PUT http://localhost:3000/tasks/1` Body (raw, JSON) :

    ```json
    jsonCopy code{
      "description": "Acheter des légumes",
      "completed": true
    }
    ```
* Requête DELETE pour supprimer une tâche par son ID : `DELETE http://localhost:3000/tasks/1`

Cet exemple illustre une application Node.js avec Express.js qui met en œuvre une API REST pour gérer une liste de tâches. Vous pouvez tester les différentes routes pour gérer les tâches en utilisant Postman ou tout autre client REST. N'hésitez pas à étendre cet exemple pour ajouter plus de fonctionnalités et personnaliser l'application selon vos besoins spécifiques.

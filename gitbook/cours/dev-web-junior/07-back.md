---
description: Le back-end c'est quoi ? le plus simple pour commencer ? C'est quoi un CRUD ?
---

# 07-Back

Le back-end est la partie d'une application web qui gère les opérations et la logique du serveur. Il est responsable du traitement des requêtes des utilisateurs, de l'accès à la base de données, de l'authentification, des calculs, de la gestion des fichiers, etc. Le back-end communique avec le front-end (la partie visible par les utilisateurs) pour fournir les données et les fonctionnalités nécessaires.

Le back-end est généralement écrit en langages de programmation tels que JavaScript (avec Node.js), Python, Ruby, Java, PHP, etc., et s'exécute sur le serveur.

Le plus simple pour commencer dépend de vos préférences et de votre expérience en programmation. Voici quelques options populaires pour commencer avec le back-end :

1. **Node.js** avec _Express.js_ : Node.js est une plateforme JavaScript côté serveur basée sur le moteur V8 de Google Chrome. Express.js est un framework minimaliste pour Node.js qui facilite la création d'applications web et d'APIs RESTful. Étant donné que vous êtes déjà familier avec JavaScript en tant que langage front-end, Node.js pourrait être une option naturelle pour vous commencer avec le back-end.
2. **Python** avec _Flask_ : Python est un langage de programmation populaire et facile à apprendre. Flask est un micro-framework web pour Python qui est simple et convivial pour créer des applications web de petite à moyenne taille.
3. **Ruby** avec _Ruby on Rails_ : Ruby est un langage élégant et convivial, et Ruby on Rails (ou simplement Rails) est un framework web complet qui facilite le développement rapide d'applications web en suivant la convention plutôt que la configuration.

Un **CRUD** est un acronyme pour les opérations de base sur les données : Create, Read, Update et Delete. Ces opérations représentent les principales actions qui peuvent être effectuées sur des données dans une base de données.

* **Create** (Créer) : Permet de créer de nouvelles entrées de données dans la base de données.
* **Read** (Lire) : Permet de lire (récupérer) les données existantes à partir de la base de données.
* **Update** (Mettre à jour) : Permet de modifier les données existantes dans la base de données.
* **Delete** (Supprimer) : Permet de supprimer des données existantes de la base de données.

Le CRUD est un concept fondamental en développement web, car la plupart des applications nécessitent une interaction avec une base de données pour stocker, récupérer et modifier des données. Les opérations CRUD sont fréquemment utilisées dans le développement back-end pour mettre en œuvre les fonctionnalités d'un site web ou d'une application.

***

### Exemple

#### NodeJS & ExpressJS

Voici un exemple simple d'une application Node.js avec Express.js qui répond à une requête GET pour renvoyer un message de bienvenue :

1. Assurez-vous d'avoir Node.js et Express.js installés sur votre machine.
2. Créez un nouveau projet Node.js et installez Express.js :

```bash
mkdir node-express-example
cd node-express-example
npm init -y
npm install express
```

3. Créez un fichier `app.js` dans le répertoire du projet avec le contenu suivant :

```javascript
const express = require('express');
const app = express();
const port = 3000;

// Route pour répondre à la requête GET '/'
app.get('/', (req, res) => {
  res.send('Bienvenue sur notre application Node.js avec Express.js !');
});

// Démarrage du serveur
app.listen(port, () => {
  console.log(`Serveur démarré sur http://localhost:${port}`);
});
```

4. Exécutez l'application :

```bash
node app.js
```

L'application sera démarrée sur `http://localhost:3000`. Lorsque vous accédez à cette URL dans votre navigateur ou via un outil comme Postman, vous verrez le message de bienvenue s'afficher.

Cet exemple est une application Node.js très simple avec Express.js qui répond à une requête GET sur la racine (`/`) et envoie un message de bienvenue. Vous pouvez étendre cette application pour ajouter plus de routes, gérer des requêtes POST, PUT, DELETE, etc., et ajouter des fonctionnalités supplémentaires selon vos besoins spécifiques.

***

#### NodeJS, ExpressJS & MongoDB

Voici un exemple simple d'une application Node.js avec Express.js et MongoDB pour mettre en œuvre les opérations CRUD :

1. Assurez-vous d'avoir Node.js, Express.js et MongoDB installés sur votre machine.
2. Créez un nouveau projet Node.js et installez les dépendances nécessaires :

```bash
mkdir node-express-mongodb-example
cd node-express-mongodb-example
npm init -y
npm install express mongodb
```

3. Créez un fichier `app.js` dans le répertoire du projet avec le contenu suivant :

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const MongoClient = require('mongodb').MongoClient;

const app = express();
const port = 3000;

// Middleware pour parser le corps des requêtes en JSON
app.use(bodyParser.json());

// Connexion à la base de données MongoDB
const uri = 'mongodb://localhost:27017';
const client = new MongoClient(uri, { useNewUrlParser: true, useUnifiedTopology: true });

let collection;

client.connect((err) => {
  if (err) {
    console.log('Erreur lors de la connexion à MongoDB :', err);
    return;
  }

  console.log('Connexion à MongoDB établie avec succès');
  const db = client.db('mydb');
  collection = db.collection('users');

  // Démarrage du serveur après la connexion à la base de données
  app.listen(port, () => {
    console.log(`Serveur démarré sur http://localhost:${port}`);
  });
});

// Route pour créer un nouvel utilisateur
app.post('/users', (req, res) => {
  const newUser = req.body;

  collection.insertOne(newUser, (err, result) => {
    if (err) {
      res.status(500).send('Erreur lors de la création de l\'utilisateur');
    } else {
      res.send(result.ops[0]);
    }
  });
});

// Route pour récupérer tous les utilisateurs
app.get('/users', (req, res) => {
  collection.find().toArray((err, users) => {
    if (err) {
      res.status(500).send('Erreur lors de la récupération des utilisateurs');
    } else {
      res.send(users);
    }
  });
});

// Route pour mettre à jour un utilisateur par son ID
app.put('/users/:id', (req, res) => {
  const userId = req.params.id;
  const updatedUser = req.body;

  collection.findOneAndUpdate(
    { _id: new mongodb.ObjectId(userId) },
    { $set: updatedUser },
    { returnOriginal: false },
    (err, result) => {
      if (err) {
        res.status(500).send('Erreur lors de la mise à jour de l\'utilisateur');
      } else {
        res.send(result.value);
      }
    }
  );
});

// Route pour supprimer un utilisateur par son ID
app.delete('/users/:id', (req, res) => {
  const userId = req.params.id;

  collection.deleteOne({ _id: new mongodb.ObjectId(userId) }, (err, result) => {
    if (err) {
      res.status(500).send('Erreur lors de la suppression de l\'utilisateur');
    } else {
      res.send(`Utilisateur avec l'ID ${userId} supprimé`);
    }
  });
});
```

4. Assurez-vous que votre instance MongoDB locale est en cours d'exécution sur le port par défaut (27017) ou mettez à jour l'URL de connexion `uri` dans `app.js` en fonction de votre configuration MongoDB.
5. Pour exécuter l'application, utilisez la commande suivante :

```bash
node app.js
```

L'application démarrera sur `http://localhost:3000`. Vous pouvez utiliser un outil comme Postman pour tester les différentes routes CRUD.

Cet exemple est une application web très basique avec Express.js et MongoDB, mais cela vous montre comment mettre en œuvre les opérations CRUD pour gérer les utilisateurs dans une base de données MongoDB. Vous pouvez étendre cette application avec des fonctionnalités supplémentaires et l'adapter selon vos besoins spécifiques.

***

#### NodeJS, ExpressJS & MySQL

Voici un exemple d'une application Node.js avec Express.js qui utilise une base de données MySQL. Dans cet exemple, nous allons créer une API simple pour gérer des utilisateurs, en effectuant des opérations CRUD sur la base de données MySQL.

Assurez-vous d'avoir Node.js, Express.js et le module `mysql` installés sur votre machine.

1. Créez un nouveau répertoire pour le projet et initialisez un nouveau projet Node.js :

```bash
mkdir node-express-mysql-example
cd node-express-mysql-example
npm init -y
```

2. Installez les dépendances nécessaires :

```bash
npm install express mysql
```

3. Créez un fichier `app.js` dans le répertoire du projet avec le contenu suivant :

```javascript
const express = require('express');
const mysql = require('mysql');

const app = express();
const port = 3000;

// Connexion à la base de données MySQL
const db = mysql.createConnection({
  host: 'localhost',
  user: 'your_mysql_username',
  password: 'your_mysql_password',
  database: 'mydb'
});

db.connect((err) => {
  if (err) {
    console.log('Erreur lors de la connexion à la base de données MySQL :', err);
    return;
  }
  console.log('Connexion à la base de données MySQL établie avec succès');
});

// Middleware pour parser le corps des requêtes en JSON
app.use(express.json());

// Route pour récupérer tous les utilisateurs
app.get('/users', (req, res) => {
  const query = 'SELECT * FROM users';
  db.query(query, (err, results) => {
    if (err) {
      res.status(500).send('Erreur lors de la récupération des utilisateurs depuis la base de données');
    } else {
      res.send(results);
    }
  });
});

// Route pour créer un nouvel utilisateur
app.post('/users', (req, res) => {
  const { nom, prenom, age, email } = req.body;
  const query = 'INSERT INTO users (nom, prenom, age, email) VALUES (?, ?, ?, ?)';
  db.query(query, [nom, prenom, age, email], (err, result) => {
    if (err) {
      res.status(500).send('Erreur lors de la création de l\'utilisateur dans la base de données');
    } else {
      res.send('Utilisateur créé avec succès');
    }
  });
});

// Route pour mettre à jour un utilisateur par son ID
app.put('/users/:id', (req, res) => {
  const userId = req.params.id;
  const { nom, prenom, age, email } = req.body;
  const query = 'UPDATE users SET nom=?, prenom=?, age=?, email=? WHERE id=?';
  db.query(query, [nom, prenom, age, email, userId], (err, result) => {
    if (err) {
      res.status(500).send('Erreur lors de la mise à jour de l\'utilisateur dans la base de données');
    } else {
      res.send('Utilisateur mis à jour avec succès');
    }
  });
});

// Route pour supprimer un utilisateur par son ID
app.delete('/users/:id', (req, res) => {
  const userId = req.params.id;
  const query = 'DELETE FROM users WHERE id=?';
  db.query(query, [userId], (err, result) => {
    if (err) {
      res.status(500).send('Erreur lors de la suppression de l\'utilisateur dans la base de données');
    } else {
      res.send('Utilisateur supprimé avec succès');
    }
  });
});

// Démarrage du serveur
app.listen(port, () => {
  console.log(`Serveur démarré sur http://localhost:${port}`);
});
```

Assurez-vous de remplacer `your_mysql_username` et `your_mysql_password` par vos informations de connexion MySQL appropriées.

4. Exécutez l'application :

```bash
node app.js
```

L'application sera démarrée sur `http://localhost:3000`. Vous pouvez utiliser un outil comme Postman pour tester les différentes routes CRUD (GET, POST, PUT, DELETE) pour gérer les utilisateurs dans la base de données MySQL.

Cet exemple vous montre comment créer une API simple avec Node.js et Express.js qui interagit avec une base de données MySQL. Vous pouvez étendre cette application pour gérer d'autres entités et ajouter des fonctionnalités supplémentaires selon vos besoins spécifiques.

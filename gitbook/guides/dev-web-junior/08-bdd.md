---
description: C'est quoi une BDD (base de donnée) ? à quoi sa sert ?
---

# 08-BDD

Une BDD (Base de données) est un système organisé de stockage de données structurées. Elle permet de stocker, de gérer et de récupérer efficacement des informations sous forme de tables, de documents, de graphes ou d'autres structures de données, en fonction du type de BDD utilisée. Les bases de données sont largement utilisées dans le domaine de l'informatique et sont essentielles pour le stockage et la gestion des données dans les applications et les systèmes.

À quoi ça sert ? Les bases de données servent à plusieurs fins importantes :

1. Stockage de données : Les BDD permettent de stocker de grandes quantités de données de manière structurée et organisée. Elles peuvent stocker des informations relatives aux utilisateurs, aux produits, aux commandes, aux transactions financières, etc.
2. Gestion des données : Les BDD fournissent des mécanismes pour ajouter, mettre à jour et supprimer des données de manière cohérente et sécurisée. Cela permet aux applications d'accéder et de manipuler les données de manière fiable.
3. Requêtes et récupération de données : Les BDD offrent des fonctionnalités pour effectuer des requêtes et des recherches dans les données, permettant ainsi de récupérer des informations spécifiques rapidement et efficacement.
4. Sécurité des données : Les BDD permettent de mettre en œuvre des contrôles d'accès et des autorisations pour protéger les données sensibles des utilisateurs non autorisés.
5. Gestion de la concurrence : Lorsque plusieurs utilisateurs accèdent simultanément aux données, les BDD gèrent les verrous et les conflits pour assurer l'intégrité des données.
6. Intégrité des données : Les BDD peuvent imposer des contraintes sur les données pour garantir que les informations stockées respectent certaines règles ou normes spécifiques.
7. Sauvegardes et récupération : Les BDD permettent de créer des sauvegardes régulières pour prévenir la perte de données en cas de panne matérielle ou d'erreurs.

En somme, les bases de données jouent un rôle central dans le développement de logiciels et d'applications, en permettant de stocker et de gérer de manière fiable de grandes quantités de données. Elles sont utilisées dans une variété de domaines, y compris les systèmes d'entreprise, les sites web, les applications mobiles, les applications financières, les réseaux sociaux, les jeux et bien d'autres. Sans les bases de données, la gestion et l'accès aux données seraient beaucoup plus complexes et inefficaces.

***

#### Exemple

Voici un exemple d'une base de données **MySQL** avec quelques requêtes **SQL** pour créer une table, insérer des données et effectuer des requêtes de sélection :

1. Tout d'abord, assurez-vous d'avoir MySQL installé sur votre machine.
2. Connectez-vous à votre serveur MySQL en utilisant l'interface en ligne de commande ou un outil de gestion de bases de données (comme **MySQL Workbench**).
3. Créez une nouvelle base de données :

```sql
CREATE DATABASE mydb;
```

4. Utilisez la base de données nouvellement créée :

```sql
USE mydb;
```

5. Créez une table pour stocker des informations sur les utilisateurs :

```sql
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nom VARCHAR(50) NOT NULL,
  prenom VARCHAR(50) NOT NULL,
  age INT,
  email VARCHAR(100)
);
```

6. Insérez quelques enregistrements dans la table :

```sql
INSERT INTO users (nom, prenom, age, email)
VALUES
  ('Doe', 'John', 30, 'john.doe@example.com'),
  ('Smith', 'Jane', 25, 'jane.smith@example.com'),
  ('Johnson', 'Michael', 35, 'michael.johnson@example.com');
```

7. Effectuez quelques requêtes de sélection :

* Sélectionnez tous les enregistrements dans la table :

```sql
SELECT * FROM users;
```

* Sélectionnez les utilisateurs dont l'âge est supérieur à 30 :

```sql
SELECT * FROM users WHERE age > 30;
```

* Sélectionnez les utilisateurs dont le prénom est 'Jane' :

```sql
SELECT * FROM users WHERE prenom = 'Jane';
```

* Sélectionnez les utilisateurs dont le nom commence par 'J' :

```sql
SELECT * FROM users WHERE nom LIKE 'J%';
```

Ceci est un exemple simple d'une base de données MySQL avec quelques requêtes SQL. Les bases de données permettent de stocker, gérer et interroger efficacement de grandes quantités de données. Les requêtes SQL sont utilisées pour communiquer avec la base de données et effectuer diverses opérations telles que la création de tables, l'insertion de données et la récupération d'informations spécifiques.


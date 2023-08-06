---
description: >-
  Comment tester notre code ? les outils, les différents test, conceptions,
  intégrations, production, charge, ...
---

# 10-Test

Tester le code est une étape essentielle du processus de développement logiciel pour s'assurer que le code fonctionne correctement, qu'il répond aux exigences spécifiées et qu'il est exempt de bugs. Il existe plusieurs types de tests, des outils et des pratiques qui peuvent être utilisés pour assurer la qualité du code et garantir que l'application se comporte comme prévu. Voici un aperçu des différents types de tests, des pratiques et des outils de test utilisés dans le cycle de développement logiciel :

1. Tests unitaires : Les tests unitaires sont des tests qui visent à vérifier le bon fonctionnement des unités de code individuelles, comme les fonctions, les méthodes ou les classes. Ils sont généralement écrits par les développeurs eux-mêmes et exécutés fréquemment pour détecter rapidement les erreurs dans le code. Les tests unitaires peuvent être automatisés à l'aide de frameworks de test tels que Mocha, Jest (pour JavaScript), NUnit, JUnit (pour Java), etc.
2. Tests d'intégration : Les tests d'intégration vérifient le bon fonctionnement des interactions entre différentes parties du système ou entre différentes applications. Ils s'assurent que les composants fonctionnent correctement ensemble. Les tests d'intégration peuvent être automatisés en utilisant des outils de test d'intégration appropriés.
3. Tests fonctionnels : Les tests fonctionnels vérifient si l'application fonctionne correctement du point de vue de l'utilisateur final en testant des scénarios réels d'utilisation. Ces tests peuvent être automatisés à l'aide d'outils de test d'interface utilisateur tels que Selenium, Puppeteer, Cypress, etc.
4. Tests de charge et de performance : Les tests de charge et de performance évaluent la capacité d'une application à supporter une charge importante, à gérer un grand nombre d'utilisateurs simultanément et à répondre rapidement. Des outils tels que JMeter, Gatling, Artillery, etc., peuvent être utilisés pour effectuer des tests de charge et de performance.
5. Tests de sécurité : Les tests de sécurité visent à identifier les vulnérabilités et les failles de sécurité potentielles dans l'application. Des outils tels que OWASP ZAP, Burp Suite, etc., sont utilisés pour effectuer des tests de sécurité.
6. Intégration continue (CI) : L'intégration continue est une pratique où le code est intégré fréquemment dans un référentiel central, et chaque intégration déclenche une suite de tests automatisés pour vérifier la qualité du code. Des outils comme Jenkins, Travis CI, CircleCI, GitLab CI/CD, etc., sont utilisés pour la mise en œuvre de l'intégration continue.
7. Livraison continue (CD) : La livraison continue est une pratique qui vise à automatiser le processus de déploiement d'une application dans des environnements de test, de préproduction et de production. L'objectif est de fournir un logiciel prêt pour la production à tout moment. Les outils CI/CD tels que ceux mentionnés ci-dessus sont utilisés pour la livraison continue.
8. Tests de régression : Les tests de régression sont effectués pour s'assurer qu'une nouvelle fonctionnalité ou une modification du code n'a pas introduit de nouveaux bugs ou cassé des fonctionnalités existantes.
9. Tests manuels : Outre les tests automatisés, les tests manuels peuvent également être utilisés pour explorer l'application, vérifier l'interface utilisateur et effectuer des scénarios d'utilisation complexes.
10. Mocking et stubbing : Dans le cadre des tests unitaires et d'intégration, des techniques de mock et de stub peuvent être utilisées pour simuler le comportement de dépendances externes et isoler les unités testées.

En résumé, le processus de test logiciel comprend une variété de tests (unitaires, fonctionnels, de charge, de sécurité, etc.) ainsi que des pratiques telles que l'intégration continue, la livraison continue et les tests automatisés pour garantir la qualité du code, la stabilité et la fiabilité de l'application. Les tests jouent un rôle crucial dans le développement logiciel moderne pour assurer la satisfaction des utilisateurs et la réussite du projet.



### Exemple

#### Node JS & Jest

Voici un exemple simple de test unitaire en Node.js en utilisant le framework de test Jest. Dans cet exemple, nous allons tester une fonction simple qui ajoute deux nombres et renvoie le résultat.

1. Assurez-vous d'avoir Node.js installé sur votre machine.
2. Installez Jest en tant que dépendance de développement dans votre projet :

```bash
bashCopy codenpm install jest --save-dev
```

3. Créez un fichier `math.js` dans le répertoire du projet avec la fonction que nous allons tester :

```javascript
// math.js
function add(a, b) {
  return a + b;
}

module.exports = add;
```

4. Créez un fichier de test `math.test.js` dans le même répertoire avec les tests unitaires :

```javascript
// math.test.js
const add = require('./math');

test('adds 1 + 2 to equal 3', () => {
  expect(add(1, 2)).toBe(3);
});

test('adds -3 + 7 to equal 4', () => {
  expect(add(-3, 7)).toBe(4);
});

test('adds 0 + 0 to equal 0', () => {
  expect(add(0, 0)).toBe(0);
});
```

5. Exécutez les tests en utilisant Jest :

```bash
npx jest
```

Jest exécutera les tests et affichera le résultat à l'écran :

```vbnet
PASS  ./math.test.js
  ✓ adds 1 + 2 to equal 3 (3 ms)
  ✓ adds -3 + 7 to equal 4 (1 ms)
  ✓ adds 0 + 0 to equal 0 (1 ms)

Test Suites: 1 passed, 1 total
Tests:       3 passed, 3 total
Snapshots:   0 total
Time:        0.708 s, estimated 1 s
Ran all test suites.
```

Dans cet exemple, nous avons créé une fonction simple `add` dans le fichier `math.js` et l'avons exportée en tant que module pour la tester. Dans le fichier de test `math.test.js`, nous avons utilisé Jest pour exécuter trois tests unitaires différents. Chaque test utilise l'assertion `expect` pour vérifier que le résultat de la fonction `add` est égal au résultat attendu.

Cet exemple montre comment créer et exécuter un test unitaire simple en Node.js en utilisant Jest. Vous pouvez ajouter plus de tests pour couvrir différents scénarios et garantir le bon fonctionnement de votre code. Les tests unitaires sont un moyen efficace de s'assurer que chaque partie du code fonctionne correctement de manière isolée, ce qui facilite la détection rapide des erreurs et des bugs.



#### NodeJS, Mocha & Chai

Voici un exemple de test unitaire en Node.js en utilisant Mocha comme framework de test et Chai comme bibliothèque d'assertions.

1. Assurez-vous d'avoir Node.js installé sur votre machine.
2. Installez Mocha et Chai en tant que dépendances de développement dans votre projet :

```bash
npm install mocha chai --save-dev
```

3. Créez un fichier `math.js` dans le répertoire du projet avec la fonction que nous allons tester :

```javascript
// math.js
function add(a, b) {
  return a + b;
}

module.exports = add;
```

4. Créez un fichier de test `math.test.js` dans le même répertoire avec les tests unitaires :

```javascript
// math.test.js
const chai = require('chai');
const expect = chai.expect;

const add = require('./math');

describe('add function', () => {
  it('should return the sum of two positive numbers', () => {
    expect(add(1, 2)).to.equal(3);
  });

  it('should return the sum of a positive number and a negative number', () => {
    expect(add(-3, 7)).to.equal(4);
  });

  it('should return zero when adding zero to any number', () => {
    expect(add(0, 100)).to.equal(100);
    expect(add(0, -5)).to.equal(-5);
    expect(add(0, 0)).to.equal(0);
  });
});
```

5. Exécutez les tests en utilisant Mocha :

```bash
npx mocha
```

Mocha exécutera les tests et affichera le résultat à l'écran :

```typescript
add function
    ✓ should return the sum of two positive numbers
    ✓ should return the sum of a positive number and a negative number
    ✓ should return zero when adding zero to any number


  3 passing (9ms)
```

Dans cet exemple, nous avons créé une fonction simple `add` dans le fichier `math.js` et l'avons exportée en tant que module pour la tester. Dans le fichier de test `math.test.js`, nous avons utilisé Mocha pour définir une suite de tests (`describe`) pour la fonction `add`, et chaque test utilise l'assertion `expect` de Chai pour vérifier que le résultat de la fonction `add` est égal au résultat attendu.

Cet exemple montre comment créer et exécuter un test unitaire simple en Node.js en utilisant Mocha comme framework de test et Chai comme bibliothèque d'assertions. Vous pouvez ajouter plus de tests pour couvrir différents scénarios et garantir le bon fonctionnement de votre code. Les tests unitaires sont un moyen efficace de s'assurer que chaque partie du code fonctionne correctement de manière isolée, ce qui facilite la détection rapide des erreurs et des bugs.

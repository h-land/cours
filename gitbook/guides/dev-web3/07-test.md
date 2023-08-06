---
description: Comment réaliser les test unitaire avec chaï, mocha, ethers, ... ?
---

# 07-Test

\
Tester un smart contrat (contrat intelligent) est une étape essentielle dans le développement d'applications décentralisées (DApps) basées sur la blockchain. Voici pourquoi le test des smart contrats est crucial :

1. Vérifier la fonctionnalité : Les tests permettent de vérifier si le smart contrat se comporte conformément aux spécifications et aux exigences fonctionnelles définies.
2. Identifier les erreurs et les bugs : Les tests unitaires et les tests d'intégration aident à détecter les erreurs et les bugs dans le smart contrat, ce qui permet de les corriger avant le déploiement sur la blockchain.
3. Garantir la sécurité : Les tests de sécurité permettent de s'assurer que le smart contrat est résistant aux attaques courantes, telles que les attaques de débordement, les attaques de déni de service, les attaques de dépassement, etc.
4. Éviter les vulnérabilités : Les tests de sécurité permettent de repérer les vulnérabilités potentielles du smart contrat, notamment en vérifiant les fonctions sensibles telles que les transferts de fonds.
5. Valider les contrats complexes : Dans le cas de contrats complexes et interconnectés, les tests permettent de s'assurer que l'ensemble du système fonctionne correctement et que les interactions entre les contrats sont correctement gérées.
6. Faciliter la maintenance : Les tests unitaires garantissent que les modifications ultérieures du smart contrat n'entraînent pas de régressions ou de problèmes inattendus.



Pour réaliser des tests unitaires avec Mocha, Chai, Ethers.js et Hardhat dans un environnement de développement Ethereum, suivez les étapes ci-dessous :

1. Installation des dépendances : Assurez-vous d'avoir Node.js installé sur votre machine. Créez ensuite un nouveau projet Node.js et installez les dépendances nécessaires :

```bash
npm init -y
npm install hardhat mocha chai ethers --save-dev
```

2. Configuration de Hardhat : Créez un fichier `hardhat.config.js` à la racine de votre projet et configurez votre réseau de test local. Vous pouvez utiliser Ganache comme réseau de test local pour Hardhat.

```javascript
// hardhat.config.js

module.exports = {
  networks: {
    development: {
      url: "http://127.0.0.1:8545", // Mettez à jour avec le port de votre réseau de test local
    },
  },
  solidity: "0.8.0", // Version du compilateur Solidity
};
```

3. Créez les contrats intelligents : Créez les contrats intelligents que vous souhaitez tester en Solidity et placez-les dans le dossier "contracts" à la racine de votre projet.
4. Écrivez les tests unitaires : Créez un dossier "test" à la racine de votre projet et écrivez les fichiers de test avec Mocha et Chai. Voici un exemple de test pour un contrat ERC-20 basique :

```javascript
// test/Token.test.js

const { expect } = require('chai');

describe('Token', function () {
  let Token;
  let token;
  let owner;
  let addr1;
  let addr2;

  beforeEach(async () => {
    [owner, addr1, addr2] = await ethers.getSigners();

    // Déployez votre contrat ERC-20 ici et assignez-le à la variable "token"
    const TokenFactory = await ethers.getContractFactory('Token');
    token = await TokenFactory.deploy();
  });

  it('should have a name, symbol, and total supply', async function () {
    expect(await token.name()).to.equal('My Token');
    expect(await token.symbol()).to.equal('MTK');
    expect(await token.totalSupply()).to.equal(ethers.utils.parseEther('1000000'));
  });

  it('should transfer tokens between accounts', async function () {
    const amount = ethers.utils.parseEther('1000');

    // Transfert de tokens de l'owner à addr1
    await token.transfer(addr1.address, amount);
    expect(await token.balanceOf(addr1.address)).to.equal(amount);

    // Vérification du solde de l'owner après le transfert
    expect(await token.balanceOf(owner.address)).to.equal(ethers.utils.parseEther('999000'));
  });

  it('should not allow transferring more tokens than the sender has', async function () {
    const balance = await token.balanceOf(owner.address);
    const amount = balance.add(ethers.utils.parseEther('1'));

    // Tentative de transfert de tokens supérieurs au solde de l'owner
    await expect(token.transfer(addr1.address, amount)).to.be.reverted;
  });
});
```

5. Exécutez les tests : Pour exécuter les tests, exécutez la commande suivante dans votre terminal :

```bash
npx hardhat test
```

Cela exécutera les tests unitaires que vous avez écrits à l'aide de Hardhat et vous donnera des résultats sur la réussite ou l'échec de chaque test.

Les tests unitaires sont essentiels pour vérifier que vos contrats intelligents fonctionnent correctement et qu'ils répondent aux exigences spécifiées. Ils vous aident à identifier et à corriger les erreurs avant de déployer vos contrats sur un réseau réel, ce qui contribue à garantir la sécurité et la fiabilité de vos applications décentralisées.

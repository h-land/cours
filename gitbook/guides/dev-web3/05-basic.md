---
description: Comment créer un token, et faire des échanges avec sur une DAPP ? dev local
---

# 05-Basic

Pour créer un token et effectuer des échanges avec sur une DApp en développement local, vous pouvez suivre les étapes suivantes :

1. Environnement de développement : Assurez-vous d'avoir un environnement de développement Ethereum en place. Vous pouvez utiliser Hardhat, Truffle ou Ganache pour créer un réseau de test local Ethereum.
2. Création du contrat du token : Écrivez le contrat intelligent du token en utilisant Solidity. Vous pouvez créer un token ERC-20 basique en utilisant le code que nous avons fourni précédemment. Assurez-vous de définir les propriétés du token telles que le nom, le symbole, le nombre de décimales et le nombre total de tokens.
3. Compilation et déploiement du contrat : Compilez le contrat à l'aide de Hardhat, Truffle ou un autre outil de développement. Déployez le contrat sur votre réseau de test local Ethereum en utilisant un compte de test.
4. Interagir avec le contrat : Une fois que le contrat est déployé, vous pouvez interagir avec lui en utilisant Web3.js ou Ethers.js dans votre DApp. Vous pouvez appeler les fonctions du contrat pour transférer des tokens, vérifier les soldes, etc.
5. Création de la DApp : Développez l'interface utilisateur de votre DApp en utilisant des technologies front-end telles que HTML, CSS et JavaScript. Utilisez Web3.js ou Ethers.js pour communiquer avec le contrat du token et effectuer des transactions.
6. Gestion des clés privées : Pour effectuer des transactions sur le réseau de test local Ethereum, vous aurez besoin de clés privées pour signer les transactions. Vous pouvez utiliser MetaMask en mode de développement pour fournir des clés privées de compte de test.
7. Test de la DApp : Testez votre DApp en effectuant des transactions de transfert de tokens, en vérifiant les soldes, etc. Assurez-vous que tout fonctionne correctement et que votre DApp interagit correctement avec le contrat du token.
8. Débogage et amélioration : Déboguez votre DApp et résolvez tout problème ou bogue qui pourrait survenir. Améliorez l'expérience utilisateur et ajoutez des fonctionnalités supplémentaires si nécessaire.

En suivant ces étapes, vous pourrez créer et échanger des tokens sur une DApp en développement local. Cela vous permettra de tester et de peaufiner votre DApp avant de la déployer sur le réseau principal Ethereum ou sur d'autres réseaux publics.

### Exemple

Pour créer une DApp très basique, nous allons créer un exemple simple d'une application de vote décentralisée qui permet aux utilisateurs de voter pour différentes propositions. Nous utiliserons HTML, CSS, JavaScript, et Solidity pour les contrats intelligents. Assurez-vous d'avoir Node.js installé sur votre machine.

Étapes pour créer une DApp de vote basique :

1. Initialisation du projet : Créez un nouveau dossier pour votre projet et initialisez un projet Node.js en exécutant la commande suivante dans le terminal :

```bash
npm init -y
```

2. Installation des dépendances : Installez les dépendances nécessaires pour le développement front-end et pour communiquer avec la blockchain Ethereum :

```bash
npm install ethers hardhat @nomiclabs/hardhat-ethers --save-dev
```

3. Configuration de Hardhat : Créez un fichier `hardhat.config.js` à la racine de votre projet et configurez Hardhat pour compiler les contrats intelligents Solidity :

```javascript
// hardhat.config.js
require("@nomiclabs/hardhat-ethers");

module.exports = {
  solidity: "0.8.0",
};
```

4. Contrat intelligent pour le vote : Créez un fichier `Vote.sol` dans un dossier appelé `contracts` à la racine de votre projet. Le contrat permettra de stocker les propositions et les votes des utilisateurs.

```solidity
// contracts/Vote.sol
pragma solidity ^0.8.0;

contract Vote {
    string public question;
    string[] public options;
    mapping(uint256 => uint256) public votes;

    constructor(string memory _question, string[] memory _options) {
        question = _question;
        options = _options;
    }

    function vote(uint256 optionIndex) public {
        require(optionIndex < options.length, "Invalid option index");
        votes[optionIndex]++;
    }
}
```

5. Compilation du contrat : Compilez le contrat en exécutant la commande suivante dans le terminal :

```bash
npx hardhat compile
```

6. Interface utilisateur : Créez un fichier `index.html` à la racine de votre projet pour l'interface utilisateur de la DApp. Voici un exemple basique :

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Vote DApp</title>
</head>
<body>
    <h1>Vote DApp</h1>
    <h2 id="question"></h2>
    <ul id="options"></ul>
    <button onclick="vote()">Vote</button>
    <script src="./app.js"></script>
</body>
</html>
```

7. Interaction avec le contrat : Créez un fichier `app.js` à la racine de votre projet pour interagir avec le contrat et effectuer des votes.

```javascript
// app.js
const { ethers } = require("ethers");
const contractAbi = require("./artifacts/contracts/Vote.sol/Vote.json").abi;

const contractAddress = "0x..."; // Remplacez par l'adresse de déploiement de votre contrat
const options = ["Option 1", "Option 2", "Option 3"]; // Remplacez par les options de vote

async function loadContract() {
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  const signer = provider.getSigner();
  const contract = new ethers.Contract(contractAddress, contractAbi, signer);

  // Récupérer les informations sur le contrat
  const question = await contract.question();
  document.getElementById("question").textContent = question;

  const optionsLength = await contract.options.length;
  const optionsList = document.getElementById("options");
  optionsList.innerHTML = "";

  for (let i = 0; i < optionsLength; i++) {
    const option = await contract.options(i);
    const optionItem = document.createElement("li");
    optionItem.textContent = option;
    optionsList.appendChild(optionItem);
  }
}

async function vote() {
  const optionIndex = parseInt(prompt("Entrez l'index de l'option pour voter:"));
  if (!isNaN(optionIndex)) {
    const provider = new ethers.providers.Web3Provider(window.ethereum);
    const signer = provider.getSigner();
    const contract = new ethers.Contract(contractAddress, contractAbi, signer);
    await contract.vote(optionIndex);
    alert("Votre vote a été enregistré!");
    loadContract();
  } else {
    alert("Index invalide!");
  }
}

window.ethereum
  .request({ method: "eth_requestAccounts" })
  .then(() => loadContract())
  .catch((err) => alert("Erreur lors de la connexion au portefeuille : " + err.message));
```

8. Exécution de la DApp : Pour exécuter la DApp, ouvrez le fichier `index.html` dans un navigateur web. Assurez-vous d'avoir installé MetaMask ou tout autre portefeuille Ethereum qui prend en charge l'interaction avec des DApps. Vous devriez pouvoir voter pour l'une des options proposées en utilisant votre portefeuille Ethereum.

Notez que cet exemple est très basique et ne prend pas en compte des aspects importants tels que la sécurité, l'authentification et l'optimisation. Dans un environnement de production, il est essentiel de considérer ces aspects et de passer par des audits de sécurité pour s'assurer que la DApp est sécurisée et robuste.

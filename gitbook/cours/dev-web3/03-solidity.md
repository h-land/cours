---
description: C'est quoi le solidity ? Comment l'utiliser ? c'est quoi l'EVM ?
---

# 03-Solidity

Solidity est un langage de programmation utilisé pour écrire des contrats intelligents sur la blockchain Ethereum. C'est le langage le plus populaire pour le développement de contrats intelligents, car il est spécialement conçu pour interagir avec la machine virtuelle Ethereum (EVM) et faciliter la création de contrats sécurisés et robustes.

Voici quelques caractéristiques clés de Solidity :

1. Syntaxe similaire à JavaScript : Solidity est inspiré de la syntaxe de JavaScript, ce qui le rend relativement facile à apprendre pour les développeurs familiers avec JavaScript et d'autres langages similaires.
2. Typage statique : Solidity est un langage à typage statique, ce qui signifie que les types de variables doivent être déclarés explicitement. Cela aide à prévenir les erreurs de type et à rendre le code plus sûr.
3. Support pour les contrats intelligents : Solidity est conçu pour la création de contrats intelligents qui s'exécutent sur la blockchain Ethereum. Il prend en charge les fonctionnalités spécifiques aux contrats intelligents, telles que l'accès aux soldes d'adresse, la gestion des événements, etc.
4. Sécurité et audibilité : Solidity intègre des fonctionnalités de sécurité pour aider les développeurs à écrire des contrats sécurisés, et il est largement utilisé et audité par la communauté pour assurer la qualité du code.

Pour utiliser Solidity, vous avez besoin d'un environnement de développement adapté au développement de contrats intelligents sur Ethereum. Voici les étapes générales pour commencer à utiliser Solidity :

1. Installez un environnement de développement : Vous pouvez utiliser des outils tels que Truffle, Hardhat ou Remix pour créer, compiler et déployer des contrats intelligents en Solidity.
2. Apprenez la syntaxe : Familiarisez-vous avec la syntaxe de Solidity en utilisant la documentation officielle, les tutoriels en ligne et les exemples de code.
3. Écrivez votre contrat intelligent : Utilisez un éditeur de code pour écrire votre contrat intelligent en Solidity. Définissez les fonctions, les variables et les événements nécessaires pour le fonctionnement de votre contrat.
4. Compilez et déployez : Utilisez l'outil de développement que vous avez choisi pour compiler votre contrat en bytecode EVM, puis déployez-le sur la blockchain Ethereum à l'aide d'un portefeuille ou d'un client Ethereum.

L'EVM (Ethereum Virtual Machine) est la machine virtuelle qui exécute les contrats intelligents écrits en Solidity et dans d'autres langages compatibles avec Ethereum. L'EVM est une machine de calcul Turing complète, ce qui signifie qu'elle peut exécuter n'importe quel algorithme ou programme qui peut être exprimé de manière algorithmique.

L'EVM fonctionne sur chaque nœud de la blockchain Ethereum et assure la cohérence de l'exécution des contrats intelligents sur l'ensemble du réseau. C'est grâce à l'EVM que les contrats intelligents sont sécurisés, immuables et transparents, car leur exécution est vérifiée par l'ensemble du réseau décentralisé.

### Exemple

Voici un exemple simple d'un contrat en Solidity qui implémente un token ERC-20 basique. Un token ERC-20 est un type de contrat intelligent qui représente une cryptomonnaie ou un actif numérique fongible sur la blockchain Ethereum.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleToken {
    string public name;
    string public symbol;
    uint8 public decimals;
    uint256 public totalSupply;
    mapping(address => uint256) public balanceOf;

    event Transfer(address indexed from, address indexed to, uint256 value);

    constructor(string memory _name, string memory _symbol, uint8 _decimals, uint256 _totalSupply) {
        name = _name;
        symbol = _symbol;
        decimals = _decimals;
        totalSupply = _totalSupply * 10**uint256(decimals);
        balanceOf[msg.sender] = totalSupply;
    }

    function transfer(address to, uint256 value) public returns (bool) {
        require(to != address(0), "Invalid address");
        require(value <= balanceOf[msg.sender], "Insufficient balance");

        balanceOf[msg.sender] -= value;
        balanceOf[to] += value;

        emit Transfer(msg.sender, to, value);
        return true;
    }
}
```

Dans cet exemple, nous avons créé un contrat nommé `SimpleToken`, qui implémente un token ERC-20 basique avec les fonctionnalités suivantes :

1. `name`, `symbol`, `decimals`, `totalSupply` : Ce sont les propriétés du token qui définissent son nom, son symbole, le nombre de décimales pour le traitement des montants et le nombre total de tokens en circulation.
2. `balanceOf` : C'est une mapping qui stocke le solde de chaque adresse détenteur de tokens.
3. `Transfer` : C'est un événement émis chaque fois qu'une transaction de transfert de tokens a lieu.
4. `constructor` : C'est la fonction qui est exécutée une seule fois lors du déploiement du contrat pour initialiser les propriétés du token.
5. `transfer` : C'est la fonction qui permet aux utilisateurs de transférer leurs tokens à d'autres adresses. Elle vérifie d'abord que le destinataire n'est pas une adresse nulle, puis vérifie si l'expéditeur a suffisamment de tokens pour effectuer le transfert. Enfin, elle met à jour les soldes des deux adresses impliquées dans la transaction et émet un événement `Transfer`.

Notez que cet exemple est très basique et ne prend pas en compte des aspects importants tels que la sécurité, l'authentification et l'optimisation. Dans un environnement de production, il est essentiel de considérer ces aspects et de passer par des audits de sécurité pour s'assurer que le contrat est sûr et robuste.

---
description: >-
  C'est quoi un smart-contract ? Les standarts de base, erc20, erc721, erc1155,
  ... ? Comment s'en servir ?
---

# 02-Smart Contract

Un smart-contract, ou contrat intelligent, est un programme informatique auto-exécutable qui s'exécute automatiquement lorsqu'il est activé par des conditions prédéfinies. Ces contrats intelligents sont généralement déployés sur une blockchain et fonctionnent de manière transparente, sans nécessiter d'intermédiaire.

Les standards de base pour les smart-contracts sont des spécifications techniques qui définissent les interfaces communes pour des fonctionnalités spécifiques. Ils permettent d'assurer l'interopérabilité et l'interchangeabilité entre différents contrats intelligents, facilitant ainsi leur utilisation et leur compatibilité avec diverses applications et plateformes.

Voici quelques-uns des standards de base les plus couramment utilisés pour les smart-contracts sur la blockchain Ethereum :

1. ERC-20 (Ethereum Request for Comments 20) : Le standard ERC-20 définit une interface commune pour les tokens fongibles sur la blockchain Ethereum. Les tokens ERC-20 sont interchangeables, c'est-à-dire qu'un token est équivalent à un autre du même type et peut être divisé en sous-unités. Ils sont couramment utilisés pour représenter des actifs numériques tels que des cryptomonnaies, des jetons d'utilité et des actifs financiers.
2. ERC-721 (Ethereum Request for Comments 721) : Le standard ERC-721 définit une interface pour les tokens non fongibles (NFTs) sur la blockchain Ethereum. Contrairement aux tokens ERC-20, chaque token ERC-721 est unique et non interchangeable, ce qui en fait un représentant numérique d'un actif unique. Les NFTs sont utilisés pour représenter des œuvres d'art numériques, des propriétés virtuelles, des objets de jeu, etc.
3. ERC-1155 (Ethereum Request for Comments 1155) : Le standard ERC-1155 définit une interface pour les tokens multi-fongibles (semi-fongibles) sur la blockchain Ethereum. Les tokens ERC-1155 permettent de combiner des caractéristiques des tokens ERC-20 et ERC-721, ce qui permet de créer des collections de tokens fongibles et non fongibles dans un seul contrat. Ils sont utilisés pour des applications telles que les jeux où différents objets peuvent avoir des propriétés communes.

Pour se servir d'un smart-contract, les étapes typiques sont les suivantes :

1. Déployer le contrat sur la blockchain : Le développeur doit déployer le contrat intelligent sur la blockchain en utilisant un outil de développement approprié comme Truffle ou Hardhat.
2. Interagir avec le contrat : Une fois le contrat déployé, les utilisateurs et les applications peuvent interagir avec lui en appelant ses fonctions publiques. Les fonctions publiques sont celles qui sont accessibles aux utilisateurs et qui peuvent être exécutées.
3. Gérer les événements : Les smart-contracts peuvent également émettre des événements pour informer les utilisateurs de certaines actions importantes sur la blockchain.
4. Utiliser des bibliothèques et des interfaces : Pour faciliter l'utilisation de contrats intelligents, des bibliothèques et des interfaces sont disponibles pour implémenter les interactions avec les contrats de manière simplifiée.

Il est essentiel de comprendre les spécifications du contrat intelligent que vous utilisez et de suivre les instructions fournies par les développeurs pour interagir avec lui en toute sécurité et de manière appropriée. La documentation officielle des contrats intelligents et des standards ERC est une ressource précieuse pour comprendre leur fonctionnement et leur utilisation.

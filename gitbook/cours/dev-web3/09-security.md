---
description: >-
  Comprendre l'exploitation de certaines failles, re-entrancy, gas-out-limit,
  ...
---

# 09-Security

Les smart contracts sont soumis à divers risques et vulnérabilités de sécurité en raison de leur nature décentralisée et immuable. Voici quelques-unes des failles de sécurité courantes dans les smart contracts :

1. Vulnérabilité aux débordements d'entiers (Integer Overflow/Underflow) : Si les entiers ne sont pas correctement vérifiés, des opérations arithmétiques peuvent provoquer des débordements ou des sous-débordements, entraînant des résultats imprévisibles.
2. Réentrance : C'est l'une des vulnérabilités les plus critiques. Un smart contract peut être exploité en utilisant un appel réentrant pour effectuer des opérations avant que l'état du contrat ne soit mis à jour, ce qui permet à l'attaquant de détourner des fonds ou de bloquer le contrat.
3. Manipulation des timestamp : Si un smart contract utilise le timestamp pour prendre des décisions importantes, il peut être manipulé par un mineur malveillant qui peut modifier le timestamp pour profiter de la situation.
4. Failles dans la gestion des autorisations : Un contrat peut permettre à des utilisateurs non autorisés d'accéder à certaines fonctions sensibles ou modifier des variables cruciales.
5. Problèmes d'appels de fonction : Un smart contract doit être vigilant lors de l'appel de fonctions externes, car cela peut entraîner des problèmes de gas limit dépassé ou d'exécution inattendue.
6. Division par zéro : Comme pour les débordements, une division par zéro peut provoquer un arrêt brutal du contrat.
7. Vulnérabilités de l'Oracle : Les smart contracts peuvent dépendre des informations externes fournies par des oracles, qui sont sujets à des manipulations malveillantes.
8. Dépassement de limite de gaz (Gas Limit) : Si un contrat nécessite une grande quantité de gaz pour s'exécuter, il peut dépasser la limite de gaz et entraîner une interruption de l'exécution.
9. Contrats malveillants et pièges : Certains contrats peuvent être conçus pour exploiter les erreurs courantes des autres développeurs ou pour piéger les utilisateurs en transférant des fonds.
10. Mauvaise gestion des jetons : Dans le cas d'ERC20 ou d'ERC721, une mauvaise gestion des jetons peut entraîner des pertes de fonds pour les utilisateurs.

Pour minimiser les risques et renforcer la sécurité des smart contracts, il est essentiel de suivre les meilleures pratiques de développement, d'effectuer des audits de sécurité, d'utiliser des frameworks de test, et de toujours garder à l'esprit les implications des fonctions et des opérations effectuées dans un environnement décentralisé et public comme la blockchain. La sécurité doit être une priorité absolue lors du développement et du déploiement de smart contracts.

Pour se prémunir des risques et des failles de sécurité courantes dans les smart contracts, voici quelques bonnes pratiques et mesures à suivre :

1. Audits de sécurité : Faites effectuer des audits de sécurité par des experts en blockchain et en sécurité pour identifier les vulnérabilités potentielles et les failles de sécurité dans votre smart contract.
2. Utiliser des bibliothèques et des standards éprouvés : Utilisez des bibliothèques et des standards de smart contracts bien établis, tels qu'OpenZeppelin, pour éviter de réinventer la roue et pour bénéficier des bonnes pratiques de sécurité déjà mises en place.
3. Validation et vérification : Validez soigneusement toutes les entrées et les sorties de données pour éviter les débordements d'entiers, les divisions par zéro et d'autres erreurs d'exécution.
4. Limiter les autorisations : N'accordez que les autorisations nécessaires aux utilisateurs et aux autres contrats pour accéder aux fonctions sensibles de votre smart contract.
5. Utilisation de la fonction `transfer` : Lorsque vous transférez des fonds à un autre contrat ou un utilisateur, utilisez plutôt la fonction `transfer` (ou `send`) pour éviter les problèmes de gas limit dépassé.
6. Utilisation de modificateurs : Utilisez des modificateurs pour effectuer des vérifications et des autorisations avant l'exécution des fonctions critiques.
7. Vérifier les contrats tiers : Si votre smart contract dépend d'autres contrats tiers, vérifiez attentivement leur sécurité et leur intégrité avant de les utiliser.
8. Utiliser des types de données adaptés : Utilisez des types de données appropriés pour les opérations arithmétiques afin d'éviter les débordements et les erreurs.
9. Tests approfondis : Effectuez des tests approfondis, y compris des tests d'unité, des tests d'intégration et des tests de sécurité pour identifier et corriger les erreurs et les bogues potentiels.
10. Utiliser des mécanismes de réparation : Envisagez d'utiliser des mécanismes de mise à jour ou de mise à niveau pour corriger les erreurs dans votre smart contract en cas de besoin.
11. Restreindre l'accès à certaines fonctions : Si certaines fonctions ne doivent être accessibles qu'à des utilisateurs spécifiques, mettez en place des mécanismes d'autorisation pour contrôler l'accès.
12. Apprendre des expériences passées : Étudiez les incidents de sécurité passés dans le domaine des smart contracts pour comprendre les erreurs courantes et les meilleures pratiques à suivre.

Se prémunir des risques et des failles de sécurité dans les smart contracts demande une approche proactive et vigilante. En adoptant une approche méthodique, en suivant les meilleures pratiques de développement et en effectuant des tests rigoureux, vous pouvez développer des smart contracts plus robustes et sécurisés pour vos applications décentralisées.

***

### Exemple

voici un exemple simple d'un smart contract vulnérable à la réentrance :

```solidity
// Smart contract vulnérable à la réentrance
pragma solidity ^0.8.0;

contract VulnContract {
    mapping(address => uint256) public balances;

    function deposit() public payable {
        // Ajoute le montant envoyé au solde de l'utilisateur
        balances[msg.sender] += msg.value;
    }

    function withdraw(uint256 _amount) public {
        // Vérifie que l'utilisateur a suffisamment de fonds pour effectuer le retrait
        require(_amount <= balances[msg.sender], "Fonds insuffisants");

        // Effectue le retrait en envoyant les fonds à l'utilisateur
        (bool success, ) = msg.sender.call{value: _amount}("");
        require(success, "Le retrait a échoué");

        // Met à jour le solde de l'utilisateur après le retrait
        balances[msg.sender] -= _amount;
    }
}
```

Explication de l'exemple :

1. Le smart contract `VulnContract` permet aux utilisateurs de déposer des fonds et de retirer une certaine quantité de ces fonds.
2. La fonction `deposit` permet aux utilisateurs de déposer des fonds sur le contrat. Lorsque cette fonction est appelée, le montant envoyé est ajouté au solde de l'utilisateur.
3. La fonction `withdraw` permet aux utilisateurs de retirer une certaine quantité de fonds du contrat. L'utilisateur doit spécifier le montant qu'il souhaite retirer.
4. Le smart contract stocke les soldes des utilisateurs dans une variable `balances`, qui est une association entre l'adresse de l'utilisateur et son solde.

Vulnérabilité de réentrance :

La vulnérabilité de réentrance se produit dans la fonction `withdraw` car elle permet aux utilisateurs de retirer des fonds avant que leur solde ne soit mis à jour. Cela signifie qu'un attaquant peut appeler la fonction `withdraw` de manière répétée avant que son solde ne soit déduit, ce qui lui permet de retirer plus de fonds qu'il ne possède réellement.

Par exemple, si l'attaquant a un solde de 100 ETH, il peut effectuer le scénario suivant pour exploiter la vulnérabilité de réentrance :

1. L'attaquant appelle la fonction `withdraw` avec `_amount` égal à 100 ETH.
2. La fonction `withdraw` envoie les 100 ETH à l'adresse de l'attaquant.
3. Cependant, le solde de l'attaquant n'est pas encore mis à jour.
4. L'attaquant appelle à nouveau la fonction `withdraw` avec `_amount` égal à 100 ETH (son solde initial).
5. La fonction `withdraw` envoie à nouveau 100 ETH à l'adresse de l'attaquant.

L'attaquant peut répéter ce processus de manière répétée avant que son solde ne soit déduit, ce qui lui permet de retirer plus de fonds qu'il ne possède réellement.

Pour éviter cette vulnérabilité de réentrance, il est essentiel de mettre à jour le solde de l'utilisateur avant de lui transférer des fonds dans la fonction `withdraw`. Cela peut être réalisé en modifiant l'ordre des opérations dans la fonction `withdraw` comme suit :

```solidity
function withdraw(uint256 _amount) public {
    // Vérifie que l'utilisateur a suffisamment de fonds pour effectuer le retrait
    require(_amount <= balances[msg.sender], "Fonds insuffisants");

    // Met à jour le solde de l'utilisateur avant le retrait
    balances[msg.sender] -= _amount;

    // Effectue le retrait en envoyant les fonds à l'utilisateur
    (bool success, ) = msg.sender.call{value: _amount}("");
    require(success, "Le retrait a échoué");
}
```

En effectuant le retrait après avoir mis à jour le solde de l'utilisateur, vous pouvez éviter la vulnérabilité de réentrance et rendre le smart contract plus sûr.

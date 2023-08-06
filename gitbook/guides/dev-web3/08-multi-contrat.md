---
description: >-
  Comment rassemblé plusieurs contrat ensemble ? fixé un prix erc20 sur un
  erc721 ou erc1155 ?
---

# 08-Multi Contrat

Rassembler plusieurs contrats ensemble dans un projet Ethereum est une pratique courante qui présente de nombreux avantages. Cela permet de créer des applications décentralisées (DApps) plus complexes et modulaires, tout en favorisant la réutilisation du code et la séparation des préoccupations. Voici quelques raisons importantes pour rassembler plusieurs contrats ensemble :

1. Modularité : En séparant le code en différents contrats, vous pouvez créer des modules réutilisables qui peuvent être utilisés dans différents contrats ou projets. Cela facilite la maintenance et l'évolutivité de votre code.
2. Séparation des préoccupations : La séparation des fonctionnalités en différents contrats permet de clarifier la structure de votre code et de mieux organiser votre DApp. Chaque contrat peut être responsable d'une fonctionnalité spécifique, ce qui rend le code plus facile à comprendre et à gérer.
3. Réutilisation du code : En regroupant certaines fonctionnalités dans des contrats séparés, vous pouvez réutiliser ces contrats dans plusieurs parties de votre DApp ou dans différents projets, ce qui permet d'économiser du temps et des efforts de développement.
4. Mise à jour sélective : En divisant votre DApp en contrats distincts, vous pouvez mettre à jour ou améliorer une partie du système sans affecter les autres parties. Cela permet de minimiser les risques d'introduire de nouvelles erreurs tout en introduisant de nouvelles fonctionnalités.
5. Souplesse et évolutivité : La modularité permet de créer une architecture flexible, ce qui facilite l'ajout de nouvelles fonctionnalités et l'extension de votre DApp à mesure que les besoins évoluent.
6. Sécurité : En séparant les fonctionnalités sensibles dans des contrats distincts, vous pouvez renforcer la sécurité de votre DApp. Par exemple, vous pouvez garder les fonctions de gestion des fonds dans un contrat distinct pour minimiser les risques d'attaques et de vulnérabilités.
7. Testabilité : En divisant votre DApp en contrats plus petits et plus ciblés, il est plus facile de tester chaque fonctionnalité individuellement, ce qui facilite la détection et la correction des erreurs.

En résumé, rassembler plusieurs contrats ensemble dans un projet Ethereum offre une approche modulaire et organisée pour le développement de DApps. Cela permet d'améliorer la réutilisation du code, la sécurité, la testabilité et l'évolutivité de votre application décentralisée. La séparation des contrats en fonctionnalités distinctes rend également le code plus clair et facilite la maintenance, ce qui est essentiel pour développer des applications robustes et fiables sur la blockchain.

***

### Exemple

Pour fixer un prix en ERC20 sur un ERC721 ou ERC1155, vous pouvez utiliser un contrat de marché (marketplace) ou un contrat d'enchères décentralisé. Le but est de permettre aux détenteurs d'ERC721 ou ERC1155 de mettre en vente leurs actifs numériques (nfts) en échange d'une certaine quantité d'ERC20, et aux autres utilisateurs d'acheter ces actifs en payant le prix demandé en ERC20.

Voici comment cela peut être réalisé en utilisant un contrat de marché basique :

1. Création du contrat ERC721 ou ERC1155 : Tout d'abord, vous avez besoin d'un contrat ERC721 ou ERC1155 qui représente les actifs numériques que les utilisateurs souhaitent vendre.
2. Création du contrat de marché : Créez un contrat de marché qui permet aux utilisateurs de mettre en vente leurs actifs ERC721 ou ERC1155 en échange d'une certaine quantité d'ERC20. Le contrat de marché doit gérer les offres de vente et les achats des utilisateurs.

```solidity
solidityCopy code// Contrat de marché basique
pragma solidity ^0.8.0;

import "./IERC20.sol";
import "./IERC721.sol"; // Remplacez par le contrat ERC721 ou ERC1155

contract Market {
    address public owner;
    IERC20 public erc20Token; // L'adresse du contrat ERC20

    struct Sale {
        address seller;
        uint256 tokenId;
        uint256 price;
    }

    mapping(uint256 => Sale) public tokenIdToSale;

    constructor(address _erc20Token) {
        owner = msg.sender;
        erc20Token = IERC20(_erc20Token);
    }

    function createSale(uint256 _tokenId, uint256 _price) external {
        // Vérifiez que le propriétaire de l'ERC721 ou ERC1155 met en vente le token
        // Ajoutez des vérifications supplémentaires selon vos besoins (par exemple, autoriser uniquement le propriétaire à vendre)

        tokenIdToSale[_tokenId] = Sale({
            seller: msg.sender,
            tokenId: _tokenId,
            price: _price
        });
    }

    function buyToken(uint256 _tokenId) external {
        Sale memory sale = tokenIdToSale[_tokenId];
        require(sale.price > 0, "Token not for sale");
        require(erc20Token.balanceOf(msg.sender) >= sale.price, "Insufficient balance");

        // Transférez l'ERC20 du compte acheteur au vendeur
        erc20Token.transferFrom(msg.sender, sale.seller, sale.price);

        // Transférez l'ERC721 ou ERC1155 du vendeur à l'acheteur
        // Ajoutez cette logique selon que vous utilisez ERC721 ou ERC1155
    }
}
```

Notez que ce code est un exemple très basique et ne gère pas tous les cas d'utilisation ou les mesures de sécurité. Dans un environnement de production, vous devriez ajouter davantage de vérifications pour garantir que le contrat de marché fonctionne de manière sécurisée et sans problème.

Assurez-vous également de déployer le contrat ERC20 et le contrat de marché sur la même blockchain pour qu'ils puissent interagir correctement.


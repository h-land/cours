---
description: Le websocket c'est quoi ? Quels est ça force ? Qui et quand l'utiliser ?
---

# 06-WebSocket

Les WebSockets sont une technologie de communication bidirectionnelle en temps réel entre un navigateur web et un serveur. Ils permettent une communication persistante et à faible latence, contrairement aux requêtes HTTP traditionnelles qui sont basées sur le modèle de requête-réponse.

Force des WebSockets :

1. Communication bidirectionnelle : Les WebSockets permettent aux clients (navigateurs web) et aux serveurs de communiquer en temps réel dans les deux sens. Cela signifie que le serveur peut envoyer des données aux clients sans que ceux-ci aient besoin de faire une demande explicite.
2. Faible latence : Grâce à leur nature persistante, les WebSockets réduisent la latence de communication entre le client et le serveur. Ils éliminent le besoin de créer une nouvelle connexion à chaque requête, ce qui permet une communication plus rapide.
3. Moins de surcharge réseau : Comme les WebSockets maintiennent une connexion ouverte, il n'y a pas besoin de rétablir la connexion à chaque interaction, ce qui réduit la surcharge du réseau et améliore les performances.
4. Économie d'énergie : En évitant de créer de nouvelles connexions pour chaque communication, les WebSockets peuvent aider à économiser de l'énergie sur les appareils clients, notamment sur les appareils mobiles.

Quand utiliser les WebSockets :

Les WebSockets sont utiles dans les scénarios où la communication en temps réel est requise, par exemple :

1. Applications de chat en temps réel : Les WebSockets sont parfaits pour les applications de chat qui nécessitent des mises à jour instantanées des messages.
2. Applications de jeux en ligne : Les WebSockets permettent une communication en temps réel entre les joueurs et le serveur, ce qui est essentiel pour les jeux multijoueurs en ligne.
3. Tableaux de bord en temps réel : Les WebSockets peuvent être utilisés pour afficher des données en temps réel sur un tableau de bord, telles que des indicateurs de performance ou des statistiques en direct.
4. Applications collaboratives : Pour les applications qui nécessitent une collaboration en temps réel entre plusieurs utilisateurs, les WebSockets offrent une solution efficace.

Il est important de noter que les WebSockets ne sont pas adaptés à tous les cas d'utilisation. Pour les applications qui ne nécessitent pas de communication en temps réel, les requêtes HTTP traditionnelles peuvent être suffisantes et plus simples à mettre en œuvre. Cependant, lorsque des mises à jour instantanées et en temps réel sont nécessaires, les WebSockets sont un outil puissant pour fournir une communication bidirectionnelle efficace entre les clients et le serveur.


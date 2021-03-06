---
description: 
manager: dongill
ms.topic: article
author: rpsqrd
ms.author: ryanpu
ms.prod: powershell
keywords: powershell,applet de commande,jea
ms.date: 2016-12-05
title: Fichier Lisez-moi
ms.technology: powershell
ms.openlocfilehash: f9609f6eb7547c627bc23687c7eb242dd2f5f457
ms.sourcegitcommit: f75fc25411ce6a768596d3438e385c43c4f0bf71
translationtype: HT
---
# <a name="just-enough-administration"></a>Just Enough Administration

Just Enough Administration (JEA) est une technologie de sécurité qui permet une administration déléguée de tout ce qui peut être géré avec PowerShell.
Avec JEA, vous pouvez :

- **Réduire le nombre d’administrateurs sur vos ordinateurs** en exploitant des comptes virtuels qui exécutent des actions privilégiées au nom d’utilisateurs normaux.
- **Limiter les opérations réalisables par les utilisateurs** en spécifiant les applets de commande, fonctions et commandes externes qu’ils peuvent exécuter.
- **Comprenez mieux ce que font vos utilisateurs** avec des transcriptions et des journaux qui vous montrent exactement quelles commandes un utilisateur a exécutées pendant sa session.

**Pourquoi est-ce important ?**

Les comptes à privilèges élevés utilisés pour administrer vos serveurs posent un important risque de sécurité.
Si une personne malveillante compromet l’un de ces comptes, elle peut lancer des [attaques latérales](http://aka.ms/pth) au sein de votre organisation.
Chaque compte qu'elle compromet peut lui donner accès à encore plus de comptes et de ressources, et donc lui permettre de voler plus facilement des secrets de l’entreprise, de lancer une attaque par déni de service et bien plus encore.

Il n’est pas non plus toujours facile de supprimer les privilèges d’administrateur.
Envisagez le scénario courant dans lequel le rôle DNS est installé sur la même machine que votre contrôleur de domaine Active Directory.
Vos administrateurs DNS ont besoin de privilèges d’administrateur local pour résoudre les problèmes liés au serveur DNS. Mais, pour cela, vous devez les intégrer comme membres au groupe de sécurité « Admins du domaine » disposant de privilèges élevés.
Cette approche permet effectivement aux administrateurs DNS de contrôler tout votre domaine et d’accéder à toutes les ressources situées sur cet ordinateur.

JEA permet de résoudre le problème en vous permettant d’adopter le principe des *privilèges minimum*.
Avec JEA, vous pouvez configurer un point de terminaison de gestion pour DNS qui leur donne accès à toutes les commandes PowerShell dont ils ont besoin pour réaliser leurs tâches, mais c’est tout.
Cela signifie que vous pouvez leur octroyer un accès approprié pour réparer un cache DNS empoisonné ou redémarrer le serveur DNS sans leur donner par inadvertance des droits sur Active Directory, parcourir le système de fichiers, ou exécuter des scripts potentiellement dangereux.
Mieux encore, quand la session JEA est configurée pour utiliser des comptes virtuels privilégiés temporaires, vos administrateurs DNS peuvent se connecter au serveur en utilisant des informations d’identification d’utilisateurs *non administrateurs* et exécuter quand même des commandes qui exigent généralement des privilèges d’administrateur.
Cette fonctionnalité vous permet de supprimer des utilisateurs dans des rôles d’administrateur local ou de domaine largement privilégiés et, à la place, de contrôler soigneusement ce qu’ils sont en mesure d’effectuer sur chaque machine.

## <a name="get-started-with-jea"></a>Bien démarrer avec JEA

Vous pouvez commencer à utiliser JEA dès aujourd'hui sur n’importe quelle machine exécutant Windows Server 2016 ou Windows 10.
Vous pouvez également exécuter JEA sur d’anciens systèmes d’exploitation avec une mise à jour de Windows Management Framework.
Pour en savoir plus sur la configuration requise pour utiliser JEA et découvrir comment créer, utiliser et auditer un point de terminaison JEA, consultez les rubriques suivantes :

- [Conditions préalables](prerequisites.md) : explique comment configurer votre environnement de manière à utiliser JEA.
- [Fonctionnalités de rôle](role-capabilities.md) : explique comment créer des rôles qui déterminent ce qu’un utilisateur est autorisé à faire dans une session JEA.
- [Configurations de session](session-configurations.md) : explique comment configurer des points de terminaison JEA mappant les utilisateurs sur des rôles et définir l’identité JEA.
- [Inscription de JEA](register-jea.md) : créez un point de terminaison JEA et permettez aux utilisateurs de s’y connecter.
- [Utilisation de JEA](using-jea.md) : découvrez les diverses méthodes d’utilisation de JEA.
- [Considérations de sécurité](security-considerations.md) : passez en revue les bonnes pratiques et les implications des options de configuration de JEA.
- [Audit et rapport de JEA](audit-and-report.md) : découvrez comment auditer les points de terminaison JEA et créer des rapports.
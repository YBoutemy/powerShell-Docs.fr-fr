---
title: "Appel direct de méthodes de ressources DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 97d97a36830088d6ee1296cda5310e087fc41893
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="calling-dsc-resource-methods-directly"></a>Appel direct de méthodes de ressources DSC

>S’applique à : Windows PowerShell 5.0

Vous pouvez utiliser l’applet de commande [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) pour appeler directement les fonctions ou méthodes d’une ressource DSC (les fonctions **Get-TargetResource**, **Set-TargetResource** et **Test-TargetResource** d’une ressource basée sur MOF, ou les méthodes **Get**, **Set** et **Test** d’une ressource basée sur la classe). Elle peut être utilisée par des tiers qui veulent utiliser des ressources DSC, ou comme un outil très utile lors du développement de ressources. 

Cette applet de commande est généralement utilisée avec une propriété de métaconfiguration `refreshMode = 'Disabled'`, mais vous pouvez l’utiliser quelle que soit la valeur de **refreshMode**.

Lors de l’appel de l’applet de commande **Invoke-DscResource**, vous spécifiez la méthode ou fonction à appeler à l’aide du paramètre **Method**. Vous spécifiez les propriétés de la ressource en passant une table de hachage comme valeur du paramètre **Property**.

Voici quelques exemples d’appels directs de méthodes de ressources :

## <a name="ensure-a-file-is-present"></a>S’assurer de la présence d’un fichier

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a>Tester la présence d’un fichier

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a>Obtenir le contenu du fichier

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

>**Remarque :** l’appel direct de méthodes de ressources composites n’est pas pris en charge. Appelez plutôt les ressources sous-jacentes qui forment la ressource composite.

## <a name="see-also"></a>Voir aussi
- [Écriture d’une ressource DSC personnalisée avec MOF](authoringResourceMOF.md) 
- [Écriture d’une ressource DSC personnalisée avec les classes PowerShell](authoringResourceClass.md)
- [Débogage des ressources DSC](debugResource.md)


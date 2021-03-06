---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,applet de commande
ms.date: 2016-12-12
title: Utilisation de variables pour stocker des objets
ms.technology: powershell
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: 232296f8db3ea665fcdf14dfe4962b96d230d733
ms.sourcegitcommit: 8acbf9827ad8f4ef9753f826ecaff58495ca51b0
translationtype: HT
---
# <a name="using-variables-to-store-objects"></a>Utilisation de variables pour stocker des objets
Windows PowerShell fonctionne avec des objets. Windows PowerShell permet de créer des variables (essentiellement des objets nommés) pour conserver les sorties en vue d’une utilisation ultérieure. Si vous êtes habitué à utiliser des variables dans d’autres interpréteurs de commandes, n’oubliez pas que les variables Windows PowerShell sont des objets, et non du texte.

Les variables sont toujours spécifiées avec le caractère initial $, et leur nom peut comprendre des caractères alphanumériques ou des traits de soulignement.

### <a name="creating-a-variable"></a>Création d’une variable
Vous pouvez créer une variable en tapant un nom de variable valide :

```
PS> $loc
PS>
```

Cette opération ne retourne aucun résultat, car **$loc** n’a pas de valeur. Vous pouvez créer une variable et lui attribuer une valeur au cours de la même étape. Windows PowerShell ne crée la variable que si elle n’existe pas. Sinon, il attribue la valeur spécifiée à la variable existante. Pour stocker votre emplacement actuel dans la variable **$loc**, tapez :

```
$loc = Get-Location
```

Aucune sortie ne s’affiche quand vous tapez cette commande, car la sortie est envoyée à $loc. Dans Windows PowerShell, une sortie affichée est un effet secondaire du fait que les données non redirigées autrement sont toujours envoyées à l’écran. La saisie de $loc affiche votre emplacement actuel :

```
PS> $loc

Path
----
C:\temp
```

Vous pouvez utiliser l’applet de commande **Get-Member** pour afficher des informations sur le contenu de variables. Le piping de $loc vers l’applet de commande Get-Member montre qu’il s’agit d’un objet **PathInfo**, tout comme la sortie de l’applet de commande Get-Location :

```
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

### <a name="manipulating-variables"></a>Manipulation de variables
Windows PowerShell fournit plusieurs commandes pour manipuler des variables. Vous pouvez afficher leur liste complète sous forme lisible en tapant ce qui suit :

```
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

Outre les variables que vous créez dans votre session Windows PowerShell actuelle, il existe plusieurs variables définies par le système. Vous pouvez utiliser l’applet de commande **Remove-Variable** pour effacer toutes les variables non contrôlées par Windows PowerShell. Pour effacer toutes les variables, tapez la commande suivante :

```
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

Cela a pour effet d’afficher l’invite de confirmation ci-dessous.

```
Confirm
Are you sure you want to perform this action?
Performing operation "Remove Variable" on Target "Name: Error".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):A
```

Si vous exécutez ensuite l’applet de commande **Get-Variable**, vous voyez les autres variables Windows PowerShell. Dans la mesure où il existe également un lecteur Windows PowerShell variable, vous pouvez également afficher toutes les variables Windows PowerShell en tapant ce qui suit :

```
Get-ChildItem variable:
```

### <a name="using-cmdexe-variables"></a>Utilisation de variables Cmd.exe
Bien que Windows PowerShell ne soit pas Cmd.exe, il s’exécute dans un environnement d’interface de commande, et peut utiliser les mêmes variables que celles disponibles tout environnement sous Windows. Ces variables sont exposées via un lecteur nommé **env**:. Vous pouvez consulter ces variables en tapant ce qui suit :

```
Get-ChildItem env:
```

Si les applets de commande variables standards ne sont pas conçues pour fonctionner avec des variables **env :**, vous pouvez toujours utiliser celles-ci en spécifiant le préfixe **env:**. Par exemple, pour afficher le répertoire racine du système d’exploitation, vous pouvez utiliser la variable **%systemroot%** de l’interface de commande à partir de Windows PowerShell en tapant ce qui suit :

```
PS> $env:SystemRoot
C:\WINDOWS
```

Vous pouvez également créer et modifier des variables d’environnement à partir de Windows PowerShell. Les variables d’environnement auxquelles vous accédez à partir de Windows PowerShell sont conformes aux règles normales applicables aux variables d’environnement ailleurs dans Windows.


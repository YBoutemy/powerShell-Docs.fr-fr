# <a name="reporting-on-jea"></a>Création de rapports sur JEA
Pour signaler l’état de votre configuration JEA, vous pouvez utiliser :
1.  **Get-PSSessionConfiguration** pour retourner une liste de tous les points de terminaison inscrits sur un ordinateur donné.
2.  **Get-PSSessionCapability** pour créer un rapport sur les capacités dont dispose tout utilisateur donné sur un point de terminaison spécifique.

Voici un exemple de **Get-PSSessionCapability** :
```powershell
Get-PSSessionCapability -ConfigurationName Maintenance -Username "CONTOSO\JohnDoe"

CommandType     Name                                               Version    Source           
-----------     ----                                               -------    ------           
Alias           clear -> Clear-Host                                                            
Alias           cls -> Clear-Host                                                              
Alias           exsn -> Exit-PSSession                                                         
Alias           gcm -> Get-Command                                                             
Alias           measure -> Measure-Object                                                      
Alias           select -> Select-Object                                                        
Function        Clear-Host                                                                     
Function        Exit-PSSession                                                                 
Function        Get-Command                                                                    
Function        Get-FormatData                                                                 
Function        Get-Help                                                                       
Function        Get-UserInfo                                                                   
Function        Measure-Object                                                                 
Function        Out-Default                                                                    
Function        Select-Object                                                                  
Cmdlet          Restart-Service                                    3.0.0.0 Microsof...


```

Pour générer un rapport sur les _actions_ effectuées par les utilisateurs pendant une session de JEA, vous pouvez :
1. Activer les transcriptions de « procuration de privilège » pour ce point de terminaison JEA et consulter le répertoire de transcription pour obtenir un journal complet des actions de chaque utilisateur
2. Activer la journalisation des modules PowerShell et inspecter les journaux des événements PowerShell
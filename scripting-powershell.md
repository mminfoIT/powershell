# Scripting PowerShell

- [Définitions](#definitions)
- [Création d’un script sous Powershell ISE au format .ps1:](#creation-dun-script-sous-powershell-ise-au-format-ps1)
- [Commenter un script :](#commenter-un-script)
- [Gestion des variables et opérations :](#gestion-des-variables-et-operations)
- [Stratégies d’exécution des scripts :](#strategies-dexecution-des-scripts)
- [Types de boucles et conditions :](#types-de-boucles-et-conditions)
  - [Boucle FOR](#boucle-for)
  - [Boucle WHILE](#boucle-while)
  - [Boucle FOREACH](#boucle-foreach)
  - [Condition IF, ELSEIF, ELSE](#condition-if-elseif-else)
  - [Condition SWITCH](#condition-switch)
- [Les fonctions](#les-fonctions)
- [Gestions des erreurs :](#gestions-des-erreurs)
  - [Erreurs non-critiques :](#erreurs-non-critiques)
  - [Erreurs critiques :](#erreurs-critiques)
  - [TRY / CATCH / FINALLY :](#try-catch-finally)
  - [$Error :](#error)
  - [$? :](#page-5aa9ed68-e533-45f9-8589-10445ee54c38)
  - [$LASTEXITCODE :](#lastexitcode)
  - [\-ErrorAction :](#erroraction)
  - [\-ErrorVariable :](#errorvariable)
  - [Throw :](#throw)

# Définitions 

PowerShell est un outil d'automatisation des tâches développé par Microsoft, qui combine un shell de ligne de commande et un langage de script. Il a été conçu pour administrer les systèmes et automatiser des tâches sur des ordinateurs Windows, mais il est également disponible sur d'autres systèmes d'exploitation comme Linux et macOS via PowerShell Core.

**Shell de ligne de commande** : PowerShell permet aux utilisateurs d'interagir avec leur système via des commandes textuelles (appelées cmdlets), de manipuler des fichiers, d'exécuter des programmes et de gérer des services. Il offre un environnement plus riche que les autres shells classiques comme Command Prompt, grâce à son intégration avec le .NET Framework.

**Langage de script** : PowerShell permet d'écrire des scripts pour automatiser des tâches répétitives ou complexes. Ces scripts peuvent inclure des boucles, des conditions, des fonctions, des variables, et peuvent interagir avec des systèmes d'exploitation, des applications, des bases de données et des services web.

**Orienté objet** : Contrairement à d'autres shells où les données sont généralement traitées sous forme de texte, PowerShell fonctionne avec des objets .NET, ce qui permet un traitement plus structuré des données et facilite l'interopérabilité avec des applications Windows et d'autres systèmes.

**Gestion de l'administration système** : PowerShell est largement utilisé pour l'administration de serveurs, la gestion des utilisateurs, la configuration des réseaux, la surveillance des performances, la gestion des services et des processus. Il offre une grande flexibilité, notamment grâce à l'accès aux API Windows Management Instrumentation (WMI) et à d'autres outils d'administration.

**Modules et extensions** : PowerShell peut être étendu par des modules, qui sont des bibliothèques de cmdlets spécialisées. Par exemple, des modules pour la gestion d'Azure, de SharePoint, de VMware, et bien d'autres, permettent aux administrateurs de gérer des ressources cloud et des systèmes tiers de manière efficace.

Historique des versions Powershell : 

| Version | Date de sortie | Notes |
| --- | --- | --- |
| PowerShell 7.2 | Novembre 2021 | Basée sur .NET 6.0. |
| PowerShell 7.1 | Novembre 2020 | Basée sur .NET 5.0. |
| PowerShell 7.0 | Mars 2020 | Basée sur .NET Core 3.1. |
| PowerShell 6.0 | Septembre 2018 | Basée sur .NET Core 2.0. Première version installable sur Windows, Linux et macOS. |
| PowerShell 5.1 | Août 2016 | Publiée dans Windows 10 (mise à jour anniversaire) et Windows Server 2016 et dans le cadre de Windows Management Framework (WMF) 5.1. |
| PowerShell 5.0 | Février 2016 | Intégrée dans Windows 10 version 1511. Publiée dans Windows Management Framework (WMF) 5.0. Installable sur Windows Server 2008 R2, Windows Server 2012, Windows 10, Windows 8.1 Entreprise, Windows 8.1 Professionnel et Windows 7 SP1. |
| PowerShell 4.0 | Octobre 2013 | Intégrée à Windows 8.1 et à Windows Server 2012 R2. Installable sur Windows 7 SP1, Windows Server 2008 SP1 et Windows Server 2012. |
| PowerShell 3.0 | octobre 2012 | Intégrée à Windows 8 et à Windows Server 2012. Installable sur Windows 7 SP1, Windows Server 2008 SP1 et Windows Server 2008 R2 SP1. |
| PowerShell 2.0 | Juillet 2009 | Intégrée à Windows 7 et à Windows Server 2008 R2. Installable sur Windows XP SP3, Windows Server 2003 SP2 et Windows Vista SP1. |
| PowerShell 1.0 | Novembre 2006 | Installable sur Windows XP SP2, Windows Server 2003 SP1 et Windows Vista. Composant facultatif de Windows Server 2008. |

Au fur et à mesure que vous découvrez PowerShell, il est important de bien appréhender les diverses versions que vous pouvez rencontrer, selon le type et l’édition de votre système d’exploitation. Il existe deux plateformes PowerShell principales :

- Windows PowerShell
- PowerShell (initialement appelé PowerShell Core)

**Windows PowerShell**

Windows PowerShell est disponible exclusivement pour le système d’exploitation Windows. Windows PowerShell 1.0 a été présenté en 2006 en tant que composant installable sur Windows XP Service Pack 2 (SP2), Windows Server 2003 SP1 et Windows Vista. Il s’agissait aussi d’un composant facultatif de Windows Server 2008. En 2009, PowerShell 2.0 a été intégré à Windows 7 et Windows Server 2008 R2. Toutes les versions de Windows PowerShell jusqu’à la version 5.1 incluse, à savoir la version disponible avec Windows 10, sont intégrées à un système d’exploitation Windows.

Windows PowerShell est un composant de système d’exploitation. Il bénéficie donc des mêmes contrats de support et de licence que son système d’exploitation parent pendant son cycle de vie.

**PowerShell**

PowerShell est fourni, installé et configuré séparément de Windows PowerShell. Publié pour la première fois en 2018 sous le nom de PowerShell Core 6.0, il s’agissait de la première version offrant une prise en charge multiplateforme, étendant ainsi sa disponibilité aux systèmes d’exploitation macOS et Linux.

La dernière version de PowerShell est PowerShell 7.2, disponible par le biais de Microsoft Update.

PowerShell et Windows PowerShell sont installés séparément et vous pouvez exécuter des commandes prises en charge en utilisant l’un ou l’autre des environnements.

# Création d’un script sous Powershell ISE au format .ps1: 

Lancement de Windows PowerShell ISE (Integrated Scripting Environment) en tant qu’administrateur

![](https://lh7-qw.googleusercontent.com/docsz/AD_4nXfA2D6_DUVFuUNlilThNdfjb3NDMi_sAQvcgQz7CXP2EhUp-8j1vWNkfFtImdo96ZXyhXmOPBPxdedhMeYONY6TFOZBUiqf3UQ-TLa80-nGs0nVb0iTV5yQa_DpUZWjQTf4QOvbIZuZq503nIX8tnE?key=7Go0bxew_bmfvkMgCv9McXc_)

Une fois lancé, l’outil se présente ainsi : 

![](https://lh7-qw.googleusercontent.com/docsz/AD_4nXewzbAu2HHLswLzoVTkrWSfIgVW67RqGSrLRmJTeOQLXz6RxEFn3Mi6pEFdkfGiT6LUHFYu7-uYCxTo4iN_89Ec1PG_0Yu-MRL4i0t8FUxCGOeNHiQewDMhblP-8IA18YPy2O19InnvpENF_7Z4mec?key=7Go0bxew_bmfvkMgCv9McXc_)

Vous avez une fenêtre du haut permettant d’écrire un script (éditeur de texte/script), une console PowerShell pour naviguer en PowerShell, exécuter votre script directement ou encore faire du débug.

Sur la droite vous avez la possibilité d’insérer des commandes directement dans votre script via la liste des commandes PowerShell tout en filtrant selon les modules au choix.

# Commenter un script : 

- Commentaire sur une ligne : « # »
- Commentaire sur plusieurs ligne / bloc de commentaires :  « <# ….*texte……* #> » 

```
# Ceci est un commentaire
# Ceci est un second commentaire

<#

--------------------------------------------------------------------------------------------------

Ceci est un bloc de commentaires 


Tout ce qui se trouve à l'intérieur ne sera pas traité comme étant des commandes ou du script


--------------------------------------------------------------------------------------------------

#>
```

# Gestion des variables et opérations : 

En programmation/scripting, une variable permet de stocker des informations afin de les utiliser dans un traitement. 

En scripting PowerShell, les variables sont automatiquement typées selon ce qui est déclaré dans ces dernières. Néanmoins, il est possible de forcer le typage des variables ou même de les convertir selon les besoins.

![](https://lh7-qw.googleusercontent.com/docsz/AD_4nXe2Whi_VtWffwRdnRKC0N5IV3K60bCh2ETN5Qj8Pzdo2PYIflu05U9MKLyX3JNJys3HAL59D3jYXiBrtbAKrpZLgnUCSndXLsuZP3N_oGewIbQVjQI7vLmY04nDD7QLUV248QAhXW69onI6RDAyuw?key=7Go0bxew_bmfvkMgCv9McXc_)

Par défaut, une variable est locale et donc accessible uniquement au sein du script en cours d’exécution.

```
$Variable1 = 50

$Variable2 = "Test"

[int]$Variable3 = 50 # Nous forçons le typage de variable de manière explicite 

# Il est également possible de la convertir avec l’outil -as : 

$Chiffre = $Variable3 -as [int] # La variable Chiffre prendra la valeur de la variable3 après conversion en « integer »
```

Au contraire, une variable d’environnement est accessible au sein du script en cours mais également en dehors.

- Variable d’environnement système
  - Portée : Tout les utilisateurs de la machine
  - Stockage : HKLM:\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\Environment
  - Déclaration : \[System.Environment\]::SetEnvironmentVariable("MON\_VAR", "valeur", "Machine")

- Variable d’environnement utilisateur : 
  - Portée : Toutes les sessions PowerShell d’un utilisateur, même après redémarrage.
  - Stockage : HKCU:\\Environment
  - Déclaration : \[System.Environment\]::SetEnvironmentVariable("MON\_VAR", "valeur", "User")

Exemples de variables réservées par PowerShell : 

```
$PSVersionTable # Donne la version de PowerShell installée

$_ # Objet courant dans une boucle ou pipeline

$? # Booléen, soit $true (succès) ou $false (echec) de la dernière commande

$Error # Liste des erreurs récentes (sous forme de tableau)
```

**Exemples d’opérations de comparaison :** 

![](https://lh7-qw.googleusercontent.com/docsz/AD_4nXdWhUhAxELf9mTZ8Eico1LkyQTWHvluNZA85O3DWaWc81dKEYQIHZfw996FqvUNHkAaJU96TbLpf33hlbcuBqMQArpEaS7xeLxt9-XLSeX7LT1YqvfhIglNTf7oKEh7nsVGqk9b-nxgORGpa3XRBw?key=7Go0bxew_bmfvkMgCv9McXc_)

![](https://lh7-qw.googleusercontent.com/docsz/AD_4nXfyksTUc17Gvn6Vr-ULxoQHH69Ftl_vGkTV3c5-wNy4tSsSuYGvnZ1QRa1tuJBiRpvvSKjbJmw71Xxk3YmGzYJUQ5jklT8Aq1FJdMzkVt0DAcSyQgyVBGPeFd3Z7wAK0S5_cl7IujyKMOLI9081iA?key=7Go0bxew_bmfvkMgCv9McXc_)

# Stratégies d’exécution des scripts : 

La stratégie d’exécution dans PowerShell a pour but de réduire la possibilité qu’un utilisateur exécute involontairement des scripts PowerShell. Vous pouvez la considérer comme une fonctionnalité de sécurité qui contrôle les conditions dans lesquelles PowerShell charge des fichiers de configuration et exécute des scripts. Cette fonctionnalité permet d’éviter l’exécution de scripts malveillants.

Il est important de souligner que la stratégie d’exécution dans PowerShell n’est pas un système de sécurité qui restreint les actions de l’utilisateur. Par exemple, si les utilisateurs ne peuvent pas exécuter un script, ils peuvent facilement contourner une stratégie en entrant le contenu du script sur la ligne de commande.

Pour identifier la stratégie d’exécution en vigueur pendant la session PowerShell active, utilisez l’applet de commande suivante :

```

Get-ExecutionPolicy

```

Vous pouvez configurer les paramètres de stratégie suivants :

- **AllSigned**. Limite l’exécution d’un script à tous les scripts signés. Ce paramètre nécessite que tous les scripts soient signés par un éditeur approuvé, y compris les scripts que vous écrivez sur l’ordinateur local. Vous recevez une invite avant toute exécution de scripts provenant d’éditeurs que vous n’avez pas encore classés comme approuvés ou non approuvés. Toutefois, la vérification de la signature d’un script n’élimine pas le risque que ce script soit malveillant. Elle assure uniquement un contrôle supplémentaire qui réduit ce risque.
- **Default**. Définit la stratégie d’exécution par défaut, à savoir Restricted pour les clients Windows et RemoteSigned pour les serveurs Windows.
- **RemoteSigned**. Il s’agit de la stratégie d’exécution par défaut pour les ordinateurs serveurs Windows. Les scripts peuvent s’exécuter, mais la stratégie nécessite une signature numérique provenant d’un éditeur approuvé sur les scripts et fichiers de configuration qui ont été téléchargés à partir d’Internet. Ce paramètre ne nécessite pas de signatures numériques sur les scripts écrits sur l’ordinateur local.
- **Restricted**. Il s’agit de la stratégie d’exécution par défaut pour les ordinateurs clients Windows. Elle permet d’exécuter des commandes individuelles, mais elle n’autorise pas les scripts.
- **Unrestricted**. Il s’agit de la stratégie d’exécution par défaut pour les ordinateurs non-Windows, que vous ne pouvez pas modifier. Elle permet aux scripts non signés de s’exécuter. Cette stratégie avertit l’utilisateur avant d’exécuter les scripts et fichiers de configuration qui ne proviennent pas de la zone intranet locale.
- **Undefined**. Indique qu’il n’existe pas de stratégie d’exécution définie dans l’étendue actuelle. Si la stratégie d’exécution est Undefined dans toutes les étendues, la stratégie d’exécution en vigueur Restricted pour les clients Windows et RemoteSigned pour Windows Server.

Pour modifier la stratégie d’exécution dans PowerShell, utilisez la commande suivante :

```
Set-ExecutionPolicy -ExecutionPolicy <PolicyName>
```

# Types de boucles et conditions :

## Boucle FOR

La boucle for est utilisée pour répéter une action un nombre défini de fois. Elle est idéale quand on connaît le point de départ, la condition de fin et l’incrémentation.

**Fonctionnement :**

- Initialise une variable.
- Vérifie une condition à chaque tour.
- Incrémente (ou décrémente) la variable.

**Utilité :**

Compter, parcourir une séquence numérique, répéter une tâche un nombre de fois connu.

**Syntaxe :** 

```
for ($i = 1; $i -le 5; $i++) {

Write-Host "Boucle numéro $i"
}
```

## Boucle WHILE

La boucle while répète une action tant qu’une condition est vraie. Elle est idéale quand on ne connaît pas à l’avance le nombre de répétitions.

**Fonctionnement :**

- Évaluer une condition.
- Exécute le bloc tant que la condition est vraie.

**Utilité :** 

- Attendre une saisie correcte.
- Répéter jusqu’à une action utilisateur.
- Lire une entrée en boucle.

**Syntaxe :** 

```
$i = 1
while ($i -le 5) {
  
  Write-Host "Boucle numéro $i"
  $i++
}
```

## Boucle FOREACH

La boucle foreach permet de parcourir chaque élément d’une collection (liste, tableau, etc.).

**Fonctionnement :** 

- Prend un élément de la liste à la fois.
- Exécute le bloc pour cet élément.
- Passe au suivant jusqu’à la fin.

**Utilité :** 

Parcourir des tableaux, collections, objets (par exemple suite à la récupération d’une liste de processes : Get-Process ou services : Get-Service, etc.)

**Syntaxe :** 

```
$users = @("Bob","Eric","David","Jean")
ForEach ($user in $users) {
  Write-Host "Utilisateur : $user"
}
```

## Condition IF, ELSEIF, ELSE

La structure if permet de tester une condition et d’exécuter une ou plusieurs instructions si cette condition est vraie.

Elle peut être étendue avec :

- else (si la condition est fausse)
- elseif (pour tester d’autres cas)

**Fonctionnement :** 

- Le script vérifie si une condition est vraie.
- Si elle est vraie : exécute le bloc de code dans le if.
- Sinon : regarde les elseif, ou exécute le bloc else.

Il est possible d’imbriquer des conditions dans d’autres conditions afin de gérer différents cas de figure.

**Utilité :** 

- Prendre des décisions dans un script.
- Gérer des cas différents selon les entrées.
- Appliquer des vérifications ou validations.

**Syntaxe :** 

```
# L'utilisateur rentre son âge et cette valeur va être intégrée à la variable "age" en tant qu'entier
[int]$age = Read-Host "Quel est votre âge ?" 

#Entre 0 et 12 ans
if ($age -ge 0 -and $age -le 12) {
    Write-Host "Catégorie : Enfant" -ForegroundColor DarkGreen
}
#Entre 13 et 17 ans
elseif ($age -ge 13 -and $age -le 17) {
    Write-Host "Catégorie : Adolescent" -ForegroundColor Blue
}

#Entre 18 et 64 ans
elseif ($age -ge 18 -and $age -le 64) {
    Write-Host "Catégorie : Adulte" -ForegroundColor Gray
}

#A partir de 65 ans
elseif ($age -ge 65) {
    Write-Host "Catégorie : Senior" -ForegroundColor Magenta


}
#Le script rentrera ici si le chiffre rentré est négatif
else {
    Write-Host "Âge invalide." -ForegroundColor Red
}
```

## Condition SWITCH

Permet de tester une valeur contre plusieurs cas possibles, et d’effectuer des actions en fonction

**Fonctionnement :**

- Il compare une valeur cible à différents cas (valeurs possibles).
- Si un cas correspond, le bloc correspondant est exécuté.

**Utilité :** 

- Alternative plus lisible à une suite de if/elseif (avec une multitude de tests)
- Très utile dans les menus, choix utilisateur, traitements groupés

**Syntaxe :** 

```
$mois = Read-Host "Entrez un numéro de mois"

switch ($mois)
{
"1" {Write-Host "Mois de Janvier" -ForegroundColor DarkGreen }
"2" {Write-Host "Mois de Février" -ForegroundColor DarkGreen }
"3" {Write-Host "Mois de Mars" -ForegroundColor DarkGreen }
"4" {Write-Host "Mois d'Avril" -ForegroundColor DarkGreen }
"5" {Write-Host "Mois de Mai" -ForegroundColor DarkGreen }
"6" {Write-Host "Mois de Juin" -ForegroundColor DarkGreen }
"7" {Write-Host "Mois de Juillet" -ForegroundColor DarkGreen }
"8" {Write-Host "Mois d'Août" -ForegroundColor DarkGreen }
"9" {Write-Host "Mois de Septembre" -ForegroundColor DarkGreen }
"10" {Write-Host "Mois d'Octobre " -ForegroundColor DarkGreen }
"11" {Write-Host "Mois de Novembre" -ForegroundColor DarkGreen }
"12" {Write-Host "Mois de Décembre" -ForegroundColor DarkGreen }

Default {
    Write-Host "Erreur de saisie, veuillez saisir un chiffre entre 1 et 12" -ForegroundColor Red
}
}
```

# Les fonctions

Une fonction est un bloc de code réutilisable que l’on peut appeler autant de fois que nécessaire.

**Fonctionnement :**

- Déclaration de la fonction une seule fois
- Exécutable avec ou sans paramètres
- Celle-ci peut retourner une valeur, ou juste faire une action

**Utilité :**

- Organiser un  script
- Éviter les répétitions
- Clarifier les rôles de chaque partie d’un script
- Réutiliser facilement des traitements

**Syntaxe :** 

```
function mois {
$mois = Read-Host "Entrez un numéro de mois"

switch ($mois)
{
"1" {Write-Host "Mois de Janvier" -ForegroundColor DarkGreen }
"2" {Write-Host "Mois de Février" -ForegroundColor DarkGreen }
"3" {Write-Host "Mois de Mars" -ForegroundColor DarkGreen }
"4" {Write-Host "Mois d'Avril" -ForegroundColor DarkGreen }
"5" {Write-Host "Mois de Mai" -ForegroundColor DarkGreen }
"6" {Write-Host "Mois de Juin" -ForegroundColor DarkGreen }
"7" {Write-Host "Mois de Juillet" -ForegroundColor DarkGreen }
"8" {Write-Host "Mois d'Août" -ForegroundColor DarkGreen }
"9" {Write-Host "Mois de Septembre" -ForegroundColor DarkGreen }
"10" {Write-Host "Mois d'Octobre " -ForegroundColor DarkGreen }
"11" {Write-Host "Mois de Novembre" -ForegroundColor DarkGreen }
"12" {Write-Host "Mois de Décembre" -ForegroundColor DarkGreen }

Default {
    Write-Host "Erreur de saisie, veuillez saisir un chiffre entre 1 et 12" -ForegroundColor Red
}
}
}
```

# Gestions des erreurs : 

## **Erreurs non-critiques :**

Ce sont des erreurs que PowerShell signale, mais n'interrompent pas l’exécution du script. Le script continue après l’erreur.

- Les erreurs sont enregistrées dans la variable $error
- La majorité des cmdlets produisent ce type d’erreur
- Ces erreurs deviendront critiques si on utilise l’option des commandes : *\-ErrorAction Stop*

Exemple : 

```
Get-Item "C:\Test\fichier_inconnu.txt" #ceci est une erreur non-critique

Write-Host "Cette ligne s'affichera quand même."
```

## **Erreurs critiques :**

Ce sont des erreurs qui interrompent immédiatement l'exécution du script.

- Ces erreurs lancent une exception et arrêtent l’exécution du script
- Pour ne pas arrêter l’exécution du script il faut mettre en place un bloc try/catch
- Si on mets en place l’instruction « throw » dans un script, l’erreur générée sera critique

## TRY / CATCH / FINALLY : 

Blocs permettant d’encadrer du code risqué (assujetti à des erreurs), attraper les erreurs et éventuellement exécuter une action finale.

**Fonctionnement :**

- Le code dans try est tenté.
- Si une erreur se produit → le bloc catch est exécuté.
- Le bloc finally (optionnel) s’exécute quoi qu’il arrive.

**Syntaxe :** 

```
try {

# Code susceptibre d'échouer 

}
catch {

# Code qui s'exécute seulement en cas d'erreur

}
finally {

# Code qui s'exécute dans tout les cas

}
```

**Utilité :** 

- Capturer les erreurs
- Afficher des messages personnalisés
- Garantir l'exécution de certaines actions

## $Error : 

Variable automatique contenant l’historique des erreurs générées pendant l’exécution de commandes ou scripts sous forme de liste.

**Fonctionnement :** 

- $error stocke toutes les erreurs non critiques par défaut.
- La dernière erreur se trouve à l’index \[0\].
- PowerShell garde un certain nombre d’erreurs en mémoire (limité par la variable $MaximumErrorCount, par défaut 256).
- Il s’enrichit automatiquement dès qu’une commande échoue.

**Utilité :** 

- Permet de consulter les erreurs récentes dans un script ou en ligne de commande.
- Utile pour le débogage, l’analyse ou la gestion manuelle des erreurs.
- Peut être vidé ou manipulé si nécessaire ($error.Clear()).

## $? : 

Variable de type booléen (true ou false) qui indique si la dernière commande PowerShell a réussi ou non.

```
Get-Item "C:\test.txt"

# Si le fichier n'existe pas, une erreur sera générée, donc la variable $? sera à False

if ($? -eq $false) {

Write-Host "La commande a échouée"

}
else {

Write-Host "La commande n'a pas échouée"

}
```

## $LASTEXITCODE : 

Variable automatique contenant le code de sortie du dernier programme externe lancé (hors commandes PowerShell donc non utilisé pour les cmdlets PowerShell mais par des commandes de type ping ou autre)

**Fonctionnement :**

- Lorsqu’un exécutable retourne un code de sortie, PowerShell le capture dans $LASTEXITCODE.
- Une valeur 0 signifie généralement que tout s’est bien passé.
- Une valeur différente de 0 indique une erreur ou bien une condition spécifique.

**Utilité :**

- Permet de vérifier si une commande système s’est exécutée avec succès.
- Utile pour la gestion des erreurs lors d’appels de programmes externes.

## \-ErrorAction : 

Paramètre de commandes PowerShell qui contrôle la réaction aux erreurs générées par une commande

**Fonctionnement :**

Il permet de choisir la stratégie de gestion d’erreur. Les options disponibles sont :

- Continue : Valeur par défaut – Affiche l’erreur et continue l’exécution
- Stop : Arrête l’éxecution
- SilentlyContinue : Ignore l’erreur sans afficher de message (mais possibilité de la retrouver)
- Ignore : Ignore complétement l’erreur sans laisser de trace
- Inquire : Demande à l’utilisateur quoi faire
- Suspend : Suspend l’exécution

**Utilité :**

- Eviter que des erreurs n’interrompent l’exécution d’un script.
- Masquer ou gérer les erreurs proprement.

**Syntaxe :** 

```
Get-Item "C:\Test\fichier_inconnu.txt" -ErrorAction [Option]
```

## \-ErrorVariable :

Paramètre qui permet de capturer les erreurs d’une commande dans une variable spécifique.

**Fonctionnement :**

- Déclaration du nom de la variable (sans $), et PowerShell y stocke les erreurs.
- La variable est cumulative si elle existe déjà.

**Utilité :**

- Permet de consulter les erreurs plus tard dans le script.
- Utile pour la journalisation ou le débogage.

**Syntaxe :** 

```
Get-Item "C:\Test\fichier_inconnu.txt" -ErrorVariable variable_error

$variable_error 
# Cette variable contiendra les erreurs
```

## Throw : 

Instruction utilisée pour générer une exception de manière explicite. Elle interrompt immédiatement l'exécution du script ou de la fonction. 

**Fonctionnement :** 

- Lors de l’utilisation de throw, PowerShell lance une exception (erreur critique interrompant l’exécution).
- Par défaut, cela arrête l’exécution à l’endroit du throw, sauf s’il y a une gestion des erreurs combinée avec un bloc try/catch.

**Utilité :**

- Forcer une erreur lorsque certaines conditions ne sont pas remplies.
- Personnaliser la gestion d’erreur dans un script ou une fonction.
- Créer une logique robuste une fois combiné avec try/catch/finally.

**Syntaxe :**

```
$fichier = "C:\Test1\rapport1.log"
$archive = "C:\Test1\rapport.zip"
$dossierdesortie = "C:\Test1\Sortie"
$testfichier = Test-Path -path $fichier

#Si le fichier n'existe pas je lance une erreur critique et arrêt du script
if ($testfichier -eq false) {Throw "Une erreur s'est produite, le fichier n'existe pas"}

# Vérifie la taille
elseif ((Get-Item $fichier).Length -gt 1MB) {
    # Compression
    Compress-Archive -Path $fichier -DestinationPath $archive
    Write-Host "Fichier compressé."

    # Décompression
    Expand-Archive -Path $archive -DestinationPath $dossierdesortie -Force
    Write-Host "Fichier décompressé dans $dossierExtraction"
}
else {
    Write-Host "Fichier trop petit pour compression." -ForegroundColor Yellow
}
```

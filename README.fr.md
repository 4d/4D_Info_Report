[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_4dir.json)](https://github.com/4d/4D_Info_Report/releases/latest/)[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)](<>)[![Downloads](https://img.shields.io/github/downloads/4d/4D_Info_Report/total.svg)](https://GitHub.com/4d/4D_Info_Report/releases/latest/)![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)<br>[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)](<>)[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)](<>)

![info_report](https://raw.githubusercontent.com/4d/4D_Info_Report/main/images/4DIR.png)

-   [Anglais](README.md)
-   [Français](README.fr.md)
-   [Allemand](README.de.md)
-   [Japonais](README.ja.md)
-   [Espagnol](README.es.md)

# À quoi sert ce composant ?

Le composant `4D_Info_Report` sert à collecter un maximum d'informations :

* sur l'environnement système, matériel, 4D

* sur la base : structure, données, triggers, index, réglages personnalisés utilisés, etc.

* en temps réel et en production : mémoire, cache, utilisateurs connectés, process, etc.

<br>

# Comment utiliser ce composant ?

**_Procédure n°1:_**

> **Important**
>
> Nécessite une version 20 R6 ou supérieure

* Créer un fichier `dependencies.json` dans le dossier `/Project/Sources/`

* Copier coller le texte ci-dessous dans le fichier `dependencies.json`

```json
{
	"dependencies": {
		"4D_Info_Report": {
			"github": "4d/4D_Info_Report",
			"version": "20.*"
		}
	}
}
```

* Le composant se chargera automatiquement après la réouverture du projet 4D

> **Note**
>
> * Le composant sera téléchargé dans le dossier :
>   * ~/Library/Caches/4D/Dependencies/.github/4d/4D_Info_Report/ (sur Mac)
>   * ~\AppData\Local\4D\Dependencies\\.github\4d\4D_Info_Report\ (sous Windows)

**_Procédure n°2:_**

Créer un dossier `Components` à côté de la structure ou de l'application (si ce dossier n'existe pas), copier le composant désarchivé et redémarrer 4D ou 4D Server.

Vous pourrez directement exécuter la méthode partagée `aa4D_NP_Report_Manage_Display` depuis 4D Distant.

Un dialogue du composant vous permettra de démarrer la procédure stockée pour créer un rapport toutes les N minutes sur le Server.

Vous pouvez aussi implémenter dans votre base hôte cet exemple de code dans la méthode base `Sur démarrage serveur` pour exécuter toute méthode partagée (leur nom commence par `aa4D_`) :

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // pour démarrer la procédure stockée créant un rapport toutes les 5 minutes
  $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
End if
```

**_Procédure n°3:_**

Vous pouvez juste créer un rapport en exécutant la méthode partagée `aa4D_NP_Util_CreateReport_Serv`.

Les rapports (fichier texte) sont créés dans un nouveau dossier `Folder_reports` à côté du fichier de données.

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // pour créer un simple rapport dans le dossier `Folder_reports` à côté du fichier de données
  $NP:=New process("aa4D_NP_Util_CreateReport_Serv";0;"$4DIR_NP")
End if
```

<br>

# Comment analyser les rapports ?

Vous pouvez analyser ces rapports :

* à partir d'un 4D distant en exécutant la méthode `aa4D_NP_Report_Export_Display`,

* à partir d'un 4D monoposte en ouvrant le composant et en cliquant sur le menu `Fichier` puis sur `Local reports compare`.

> [!TIP]
> Démonstration vidéo sur l'utilisation du composant en français :
> 
> * [en Haute Définition sur le site de Vimeo](https://vimeo.com/32785939)

<br>

# Téléchargement

* documentation (en anglais) : [4D_Info_Report_v4_80_Ref_v40.pdf](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_80_Ref_v40.pdf)

* base hôte (4D 19) utilisant des méthodes hôtes à inclure dans votre base (merci d'ajouter le composant dans le dossier "Components" pour tester) : [4D_Info_Report_Host_T_v9_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v9_19.zip)

* composant en version 4D 20 R6 (compilé aussi pour processeur Apple Silicon) : [4D_Info_Report-20-R6.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report-20-R6.zip)

* composant en version 4D 20 LTS (compilé aussi pour processeur Apple Silicon) : [4D_Info_Report-20-LTS.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report-20-LTS.zip)

* composant en version 4D 19 R6 (compilé seulement pour processeur Intel/AMD) : [4D_Info_Report_v4_83_I_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19R6.zip)

* composant en version 4D 19 R6 (compilé aussi pour processeur Apple Silicon) : [4D_Info_Report_v4_83_IS_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19R6.zip)

* composant en version 4D 19 (compilé seulement pour processeur Intel/AMD) : [4D_Info_Report_v4_83_I_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19.zip)

* composant en version 4D 19 (compilé aussi pour processeur Apple Silicon) : [4D_Info_Report_v4_83_IS_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19.zip)

<br>

# Archives

* composant pour la version 4D 18 : [4D_Info_Report_v4_65_v18.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_65_v18.zip)

* composant en version 4D 17 (compilé uniquement en 64 bits) : [4D_Info_Report_v4_33_64-bit_v17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_64-bit_v17.zip)

* composant en version 4D 17 (compilé aussi en 64 bits) : [4D_Info_Report_v4_33_v17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_v17.zip)

* base hôte v17 utilisant des méthodes hôtes à inclure dans votre base (merci d'ajouter le composant dans le dossier "Components" pour tester) : [4D_Info_Report_Host_T_v8_v17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v8_v17.zip)

* composant en version 4D 16 (compilé aussi en 64 bits) : [4D_Info_Report_v4_9rZC_v16_rev3.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZC_v16_rev3.zip)

* composant en version 4D 15 (compilé aussi en 64 bits) : [4D_Info_Report_v4_9rZ8_v15_rev2.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

* composant en version 4D 14 (compilé aussi en 64 bits) : [4D_Info_Report_v4_9rZ2_v14_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

* composant en version 4D 13 (compilé aussi en 64 bits) : [4D_Info_Report_v4_9rZ2_v13_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

* composant en version 4D 12 (compilé aussi en 64 bits) : [4D_Info_Report_v4_9rZ_v12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ_v12.zip)

* base hôte v12 utilisant des méthodes hôtes à inclure dans votre base (merci d'ajouter le composant dans le dossier "Components" pour tester) : [4D_Info_Report_Host_T_v6_v12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v6_v12.zip)

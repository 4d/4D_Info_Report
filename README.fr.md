[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_4dir.json)](https://github.com/4d/4D_Info_Report/releases/latest/)
[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)]()
[![Downloads](https://img.shields.io/github/downloads/4d/4D_Info_Report/total.svg)](https://GitHub.com/4d/4D_Info_Report/releases/latest/)
![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)
![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)
<br>
[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)]()
[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)]()

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

# Comment installer ce composant ?

Il existe 2 manières d'installer ce composant :
* 1/ Automatiquement : en utilisant le gestionnaire des dépendances ([nouvelle fonctionnalité 4D, disponible à partir de la version 4D 20 R6](https://blog.4d.com/fr/integrate-4d-components-directly-from-github/))
* 2/ Manuellement : en copiant collant le composant 4D_Info_Report dans le dossier `Components` du projet 4D (fonctionne avec toutes les versions de 4D)

**_1/ Automatiquement_**

> Cette méthode nécessite d'utiliser la version 20 R6 de 4D minimum

* Créer un fichier `dependencies.json` dans le dossier `/Project/Sources/`

* Copier coller le texte ci-dessous dans ce fichier :

```json
{
	"dependencies": {
		"4D_Info_Report": {
			"github": "4d/4D_Info_Report",
			"version": "4d"
		}
	}
}
```

* Redémarrer 4D ou 4D Server, le composant se chargera automatiquement après la réouverture du projet 4D

> Pour information le composant sera téléchargé dans le dossier :
> * ~/Library/Caches/4D/Dependencies/.github/4d/4D_Info_Report/ (sur Mac)
> * ~\AppData\Local\4D\Dependencies\\.github\4d\4D_Info_Report\ (sous Windows)

* Suivre l'une des 2 manières d'utiliser le composant (voir paragraphe suivant) pour générer un ou plusieurs rapports

**_2/ Manuellement_**

> Cette méthode fonctionne avec toutes les versions de 4D

* Télécharger la version du composant correspondant à votre version de 4D (voir le paragraphe `Téléchargement` ou `Archives` de cet article)

* Créer un dossier `Components` dans le dossier du projet 4D (si ce dossier n'existe pas)

* Copier le composant désarchivé dans ce dossier `Components`

* Redémarrer 4D ou 4D Server

* Suivre l'une des 2 manières d'utiliser le composant ci-dessous pour générer un ou plusieurs rapports

<br>

# Comment utiliser ce composant ?

Il existe 2 manières d'utiliser ce composant :
* 1/ Générer des rapports toutes les N minutes
* 2/ Générer un rapport à la demande

> Les rapports (fichier texte) sont créés dans un nouveau dossier `Folder_reports` à côté du fichier de données.

Pour chacune d'elles, vous pouvez utiliser le composant :
* Sans modifier le code de la base hôte : Exécuter une méthode partagée du composant en créant `manuellement` une procédure stockée sur le serveur. L’avantage est qu’il n’est pas nécessaire de modifier le code de la base hôte, ce qui est particulièrement utile si l’application est déployée en version compilée, car cela évite une recompilation. Cependant, l’inconvénient est que vous devez exécuter à nouveau la méthode partagée après chaque redémarrage du serveur 4D pour que la procédure stockée soit active.
* En modifiant le code de la base hôte : Cette méthode consiste à ajouter du code directement dans la base hôte. Elle permet de créer la procédure stockée automatiquement lors du démarrage du serveur 4D, ce qui est très utile pour générer des rapports de façon autonome et sans intervention. C’est une solution `automatisée` où tout est en place dès que le serveur se lance.

> Ces deux approches ont chacune leurs avantages selon le contexte et les besoins en surveillance de l’application.

**_1/ Générer des rapports toutes les N minutes_**

**_Sans modifier le code de la base hôte :_**

* Exécuter la méthode partagée `aa4D_NP_Report_Manage_Display` depuis 4D Distant

* Un dialogue du composant vous permettra de démarrer la procédure stockée pour créer un rapport toutes les N minutes sur le serveur 4D

**_En modifiant le code de la base hôte :_**

* Copier coller l'exemple de code ci-dessous dans la méthode base `Sur démarrage serveur` de votre base hôte :

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // pour démarrer la procédure stockée en créant un rapport toutes les 5 minutes
  $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
End if
```

**_2/ Générer un rapport unique_**

**_Sans modifier le code de la base hôte :_**

* Créer un rapport en exécutant la méthode partagée `aa4D_NP_Util_CreateReport_Serv`

**_En modifiant le code de la base hôte :_**

* Copier coller l'exemple de code ci-dessous dans votre base hôte :

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

> Démonstration vidéo sur l'utilisation du composant en français :
> 
> * [en Haute Définition sur le site de Vimeo](https://vimeo.com/32785939)

<br>

# Téléchargement

* documentation (en anglais) : [4D_Info_Report_v4_90_Ref_v42.pdf](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_Ref_v42.pdf)

* base hôte (4D 19) utilisant des méthodes hôtes à inclure dans votre base (merci d'ajouter le composant dans le dossier "Components" pour tester) : [4D_Info_Report_Host_T_v9_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v9_19.zip)

* composant en version 4D 20 R10 (compilé aussi pour processeur Apple Silicon) : [4D_Info_Report_20R10](https://github.com/4d/4D_Info_Report/releases/latest/)

* composant en version 4D 20 LTS (compilé aussi pour processeur Apple Silicon) : [4D_Info_Report_20](https://github.com/4d/4D_Info_Report/releases/latest/)

* composant en version 4D 19 R6 (compilé seulement pour processeur Intel/AMD) : [4D_Info_Report_v4_83_I_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19R6.zip)

* composant en version 4D 19 R6 (compilé aussi pour processeur Apple Silicon) : [4D_Info_Report_v4_83_IS_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19R6.zip)

* composant en version 4D 19 (compilé seulement pour processeur Intel/AMD) : [4D_Info_Report_v4_83_I_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19.zip)

* composant en version 4D 19 (compilé aussi pour processeur Apple Silicon) : [4D_Info_Report_v4_90_2_IS_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_2_IS_19.zip)

<br>

# Archives

* composant pour la version 4D 18 : [4D_Info_Report_v4_90_2_18.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_2_v18.zip)

* composant en version 4D 17 (compilé uniquement en 64 bits) : [4D_Info_Report_v4_33_64-bit_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_64-bit_v17.zip)

* composant en version 4D 17 (compilé aussi en 64 bits) : [4D_Info_Report_v4_33_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_v17.zip)

* base hôte en version 4D 17 utilisant des méthodes hôtes à inclure dans votre base (merci d'ajouter le composant dans le dossier "Components" pour tester) : [4D_Info_Report_Host_T_v8_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v8_v17.zip)

* composant en version 4D 16 (compilé aussi en 64 bits) : [4D_Info_Report_v4_9rZC_16_rev3.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZC_v16_rev3.zip)

* composant en version 4D 15 (compilé aussi en 64 bits) : [4D_Info_Report_v4_9rZ8_15_rev2.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

* composant en version 4D 14 (compilé aussi en 64 bits) : [4D_Info_Report_v4_9rZ2_14_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

* composant en version 4D 13 (compilé aussi en 64 bits) : [4D_Info_Report_v4_9rZ2_13_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

* composant en version 4D 12 (compilé aussi en 64 bits) : [4D_Info_Report_v4_9rZ_12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ_v12.zip)

* base hôte en version 4D 12 utilisant des méthodes hôtes à inclure dans votre base (merci d'ajouter le composant dans le dossier "Components" pour tester) : [4D_Info_Report_Host_T_v6_12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v6_v12.zip)

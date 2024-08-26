[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_inforeport.json)](https://github.com/4d/4D_Info_Report/releases/latest/)[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)](<>)[![Downloads](https://img.shields.io/github/downloads/4d/4D_Info_Report/total.svg)](https://GitHub.com/4d/4D_Info_Report/releases/latest/)![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)<br>[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)](<>)[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)](<>)

# Outil 4D_Info_Report

![info_report](https://github.com/4d/4D_Info_Report/blob/main/images/4DIR.png)

## Traduction du fichier README

-   [Anglais](README.md)
-   [Français](README.fr.md)
-   [Allemand](README.de.md)
-   [japonais](README.ja.md)
-   [Espagnol](README.es.md)

## A propos de ce composant ?

Le composant`4D_Info_Report`fournit un grand nombre d’informations :

-   sur le système d'exploitation, l'ordinateur et l'application 4D

-   sur la base de données : description de la structure, fichier de données, taille, paramètres, etc.

-   pendant le fonctionnement du serveur, variation de la mémoire, utilisation du cache, utilisateurs connectés, processus, etc.

<br>

## Comment utiliser ce composant ?

**_Procedure n°1:_**

> [!NOTE]
> Si vous utilisez la version 20 R6 ou supérieure

-   Créer un`dependencies.json`fichier dans le`/Project/Sources/`dossier

-   Copiez et collez le texte ci-dessous dans le`dependencies.json`déposer

```json
{
	"dependencies": {
		"4D_Info_Report": {
			"github": "4d/4D_Info_Report",
			"version": "latest"
		}
	}
}
```

-   Le composant se chargera automatiquement après la réouverture de votre projet 4D

> [!NOTE]
>
> -   Le composant sera présent dans le dossier :
>     -   ~/Bibliothèque/Caches/4D/Dependencies/.github/4d/4D_Info_Report/ (sur Mac)
>     -   ~\AppData\Local\4D\Dependencies\\.github\4d\4D_Info_Report\ (sous Windows)

**_Procedure n°2:_**

Créer un dossier`Components`à côté de la structure ou du fichier d'application (s'il n'existe pas déjà), copiez le composant non archivé, et redémarrez votre 4D ou 4D Server.

Ensuite, vous pouvez exécuter directement la méthode shared :`aa4D_NP_Report_Manage_Display`depuis 4D Remote.

Une boîte de dialogue du composant vous permettra de démarrer la procédure stockée pour créer des rapports toutes les N minutes sur le serveur.

Vous pouvez également implémenter dans votre base de données Host, ce petit code dans votre`On Server startup`méthode pour exécuter l’une des méthodes partagées (elles commencent toutes par`aa4D_`):

<pre>
  <code class="4d">
    var $NP : Integer
    ARRAY TEXT($at_Components;0)
    COMPONENT LIST($at_Components)
    If(Find in array($at_Components;"4D_Info_Report@")>0)
      // to start the stored procedure creating report every 5 minutes
      $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
    End if
   </code>
</pre>

**_Procedure n°3:_**

Vous pouvez simplement créer un seul rapport en utilisant la méthode partagée`aa4D_NP_Util_CreateReport_Serv`.

Les rapports créés (fichiers texte) sont stockés dans un dossier créé`Folder_reports`à côté du fichier de données.

<pre>
  <code class="4d">
    var $NP : Integer
    ARRAY TEXT($at_Components;0)
    COMPONENT LIST($at_Components)
    If(Find in array($at_Components;"4D_Info_Report@")>0)
      // to create a single report in "Folder_reports" next to the Data file
      $NP:=New process("aa4D_NP_Util_CreateReport_Serv";0;"$4DIR_NP")
    End if
    </code>
</pre>

<br>

## Comment analyser les rapports ?

Vous pouvez analyser ces rapports :

-   depuis un 4D distant en exécutant la commande`aa4D_NP_Report_Export_Display`méthode

-   depuis un 4D mono-utilisateur en ouvrant le composant et en cliquant sur l'icône`File / Local reports compare`menu

<br>

## Télécharger

-   référence du composant :[ChD_Info_Report_vch_80_Ref_v40.pdf](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_80_Ref_v40.pdf)

-   base de données hôte (19) avec quelques exemples de méthodes partagées par l'hôte (veuillez ajouter le composant dans le dossier "Components" pour votre test :[4D_Info_Report_Host_T_v9_19.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_Host_T_v9_19.zip)

-   composant pour la version 4D 20 R5 (également compilé pour le processeur Apple Silicon) :[4D_Info_Report-20-R5.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report-20-R5.zip)

-   composant pour la version 4D 20 (également compilé pour le processeur Apple Silicon) :[4D_Info_Report-20-LTS.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report-20-LTS.zip)

-   composant pour la version 4D 19 R6 (compilé uniquement pour processeur Intel/AMD) :[4D_Info_Report_v4_82_I_19R6.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_82_I_19R6.zip)

-   composant pour la version 4D 19 R6 (également compilé pour le processeur Apple Silicon) :[4D_Info_Report_v4_82_IS_19R6.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_82_IS_19R6.zip)

-   composant pour la version 4D 19 (compilé uniquement pour processeur Intel/AMD) :[4D_Info_Report_v4_82_I_19.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_82_I_19.zip)

-   composant pour la version 4D 19 (également compilé pour le processeur Apple Silicon) :[4D_Info_Report_v4_82_IS_19.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_82_IS_19.zip)

<br>

## Archives

-   composant pour la version 4D v18 :[4D_Info_Report_v4_65_v18.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_65_v18.zip)

-   composant pour la version 4D v17 (compilé uniquement pour le 64 bits) :[4D_Info_Report_v4_33_64-bit_v17.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_33_64-bit_v17.zip)

-   composant pour la version 4D v17 (également compilé pour le 64 bits) :[4D_Info_Report_v4_33_v17.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_33_v17.zip)

-   base de données hôte (v17) avec quelques exemples de méthodes partagées par l'hôte (veuillez ajouter le composant dans le dossier "Components" pour votre test :[4D_Info_Report_Host_T_v8_v17.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_Host_T_v8_v17.zip)

-   composant pour la version 4D v16 (également compilé pour le 64 bits) :[4D_Info_Report_v4_9rZC_v16_rev3.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZC_v16_rev3.zip)

-   composant pour la version 4D v15 (également compilé pour le 64 bits) :[4D_Info_Report_v4_9rZ8_v15_rev2.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

-   composant pour la version 4D v14 (également compilé pour le 64 bits) :[4D_Info_Report_v4_9rZ2_v14_rev1.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

-   composant pour la version 4D v13 (également compilé pour le 64 bits) :[4D_Info_Report_v4_9rZ2_v13_rev1.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

-   composant pour la version 4D v12 (également compilé pour le 64 bits) :[4D_Info_Report_v4_9rZ_v12.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ_v12.zip)

-   base de données hôte (v12) avec quelques exemples de méthodes partagées par l'hôte (veuillez ajouter le composant dans le dossier "Components" pour votre test :[4D_Info_Report_Host_T_v6_v12.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_Host_T_v6_v12.zip)

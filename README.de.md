[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_4dir.json)](https://github.com/4d/4D_Info_Report/releases/latest/)
[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)]()
[![Downloads](https://img.shields.io/github/downloads/4d/4D_Info_Report/total.svg)](https://GitHub.com/4d/4D_Info_Report/releases/latest/)
![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)
![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)
<br>
[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)]()
[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)]()

![info_report](https://raw.githubusercontent.com/4d/4D_Info_Report/main/images/4DIR.png)

* [Englisch](README.md)
* [Französisch](README.fr.md)
* [Deutsch](README.de.md)
* [Japanisch](README.ja.md)
* [Spanisch](README.es.md)

# Über diese Komponente?

Die Komponente`4D_Info_Report`bietet zahlreiche Informationen:

* über das Betriebssystem, den Computer und die 4D-Anwendung

* zur Datenbank: Beschreibung der Struktur, Datendatei, Größe, Einstellungen usw.

* während der Server läuft, Variation des Speichers, Cache-Nutzung, verbundene Benutzer, Prozesse usw.

<br>

# Wie verwende ich diese Komponente?

**_Verfahren Nr. 1:_**

> Erfordert Version 20 R6 oder höher

* Erstellen Sie eine`dependencies.json`Datei in der`/Project/Sources/`Ordner

* Kopieren Sie den Text unten und fügen Sie ihn in die ein`dependencies.json`Datei

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

-   Die Komponente wird automatisch geladen, nachdem Sie Ihr 4D-Projekt erneut geöffnet haben

> * Die Komponente befindet sich im Ordner:
>   * ~/Library/Caches/4D/Dependencies/.github/4d/4D_Info_Report/ (auf Mac)
>   * ~\AppData\Local\4D\Dependencies\\.github\4d\4D_Info_Report\ (unter Windows)

**_Verfahren Nr. 2:_**

Erstellen Sie einen Ordner`Components`neben der Struktur- oder Anwendungsdatei (falls diese noch nicht vorhanden ist), kopieren Sie die nicht archivierte Komponente und starten Sie Ihren 4D oder 4D Server neu.

Dann können Sie die gemeinsam genutzte Methode direkt ausführen:`aa4D_NP_Report_Manage_Display`von 4D Remote.

Über einen Dialog der Komponente können Sie die gespeicherte Prozedur starten, um alle N Minuten Berichte auf dem Server zu erstellen.

Sie können diesen kleinen Code auch in Ihrer Host-Datenbank implementieren`On Server startup`Methode, um eine der gemeinsam genutzten Methoden auszuführen (sie beginnen alle mit`aa4D_`):

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // to start the stored procedure creating report every 5 minutes
  $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
End if
```

**_Verfahren Nr. 3:_**

Sie können mit der gemeinsamen Methode nur einen Bericht erstellen`aa4D_NP_Util_CreateReport_Serv`.

Die erstellten Berichte (Textdateien) werden in einem erstellten Ordner gespeichert`Folder_reports`neben der Datendatei.

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // to create a single report in "Folder_reports" next to the Data file
  $NP:=New process("aa4D_NP_Util_CreateReport_Serv";0;"$4DIR_NP")
End if
```

<br>

# Wie analysiert man Berichte?

Sie können diese Berichte analysieren:

* von einem entfernten 4D aus durch Ausführen von`aa4D_NP_Report_Export_Display`Verfahren

* von einem Einzelbenutzer-4D aus, indem Sie die Komponente öffnen und auf klicken`File / Local reports compare`Speisekarte

<br>

# Herunterladen

* Referenz der Komponente: [4D_Info_Report_v4_80_Ref_v40.pdf](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_80_Ref_v40.pdf)

* Host-Datenbank (4D 19) mit einigen Beispielen für gemeinsam genutzte Host-Methoden (bitte fügen Sie die Komponente für Ihren Test im Ordner „Components“ hinzu: [4D_Info_Report_Host_T_v9_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v9_19.zip)

* Komponente für Version 4D 20 R6 (auch für Apple Silicon Prozessor kompiliert): [4D_Info_Report_20R6](https://github.com/4d/4D_Info_Report/releases/latest/)

* Komponente für Version 4D 20 LTS (auch für Apple Silicon Prozessor kompiliert): [4D_Info_Report_20](https://github.com/4d/4D_Info_Report/releases/latest/)

* Komponente für Version 4D 19 R6 (nur für Intel/AMD-Prozessor kompiliert): [4D_Info_Report_v4_83_I_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19R6.zip)

* Komponente für Version 4D 19 R6 (auch für Apple Silicon Prozessor kompiliert): [4D_Info_Report_v4_83_IS_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19R6.zip)

* Komponente für Version 4D 19 (nur für Intel/AMD-Prozessor kompiliert): [4D_Info_Report_v4_83_I_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19.zip)

* Komponente für Version 4D 19 (auch für Apple Silicon Prozessor kompiliert): [4D_Info_Report_v4_83_IS_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19.zip)

<br>

# Archiv

* Komponente für Version 4D 18: [4D_Info_Report_v4_65_18.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_65_v18.zip)

* Komponente für Version 4D 17 (nur für 64-Bit kompiliert): [4D_Info_Report_v4_33_64-bit_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_64-bit_v17.zip)

* Komponente für Version 4D 17 (auch für 64-Bit kompiliert): [4D_Info_Report_v4_33_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_v17.zip)

* Host-Datenbank (4D 17) mit einigen Beispielen für gemeinsam genutzte Host-Methoden (bitte fügen Sie die Komponente für Ihren Test im Ordner „Components“ hinzu: [4D_Info_Report_Host_T_v8_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v8_v17.zip)

* Komponente für Version 4D 16 (auch für 64-Bit kompiliert): [4D_Info_Report_v4_9rZC_16_rev3.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZC_v16_rev3.zip)

* Komponente für Version 4D 15 (auch für 64-Bit kompiliert): [4D_Info_Report_v4_9rZ8_15_rev2.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

* Komponente für Version 4D 14 (auch für 64-Bit kompiliert): [4D_Info_Report_v4_9rZ2_14_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

* Komponente für Version 4D 13 (auch für 64-Bit kompiliert): [4D_Info_Report_v4_9rZ2_13_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

* Komponente für Version 4D 12 (auch für 64-Bit kompiliert): [4D_Info_Report_v4_9rZ_12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ_v12.zip)

* Host-Datenbank (4D 12) mit einigen Beispielen für gemeinsam genutzte Host-Methoden (bitte fügen Sie die Komponente für Ihren Test im Ordner „Components“ hinzu: [4D_Info_Report_Host_T_v6_12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v6_v12.zip)

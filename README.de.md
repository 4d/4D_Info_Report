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

# Wie installiert man diese Komponente?

Es gibt 2 Möglichkeiten, diese Komponente zu installieren:
* 1/ Automatisch: mithilfe des Abhängigkeitsmanagers ([neue 4D Funktionalität, verfügbar ab Version 4D 20 R6](https://blog.4d.com/integrate-4d-components-directly-from-github/))
* 2/ Manuell: Durch Kopieren und Einfügen der Komponente 4D_Info_Report in den Ordner `Components` des 4D Projekts (funktioniert mit allen 4D Versionen)

**_1/ Automatisch_**

> Diese Methode erfordert, dass Sie mindestens 4D Version 20 R6 verwenden

* Erstellen Sie eine Datei `dependencies.json` im Ordner `/Project/Sources/`

* Kopieren Sie den unten stehenden Text in diese Datei:

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

* Starten Sie 4D oder 4D Server neu, die Komponente wird nach dem erneuten Öffnen des 4D Projekts automatisch geladen

> Zur Information wird die Komponente in den Ordner:
> * ~/Library/Caches/4D/Dependencies/.github/4d/4D_Info_Report/ (auf dem Mac)
> * ~\AppData\Local\4D\Dependencies\\.github\4d\4D_Info_Report\ (unter Windows)

* Folgen Sie einer der beiden Möglichkeiten, die Komponente zu verwenden (siehe nächster Abschnitt), um einen oder mehrere Berichte zu erstellen

**_2/ Manuell_**

> Diese Methode funktioniert mit allen Versionen von 4D

* Laden Sie die Version der Komponente herunter, die Ihrer 4D Version entspricht (siehe Abschnitt `Herunterladen` oder `Archiv` in diesem Artikel)

* Erstellen Sie einen Ordner `Components` im Ordner des 4D Projekts (falls dieser Ordner nicht existiert)

* Kopieren Sie die eingecheckte Komponente in diesen Ordner `Components`

* 4D oder 4D Server neu starten

* Befolgen Sie eine der beiden Möglichkeiten, die Komponente unten zu verwenden, um einen oder mehrere Berichte zu erstellen

<br>

# Wie verwende ich diese Komponente?

Es gibt 2 Möglichkeiten, diese Komponente zu verwenden:
* 1/ Berichte alle N Minuten erstellen
* 2/ Auf Anfrage einen Bericht erstellen

> Die Berichte (Textdatei) werden in einem neuen Ordner `Folder_reports` neben der Datendatei erstellt.

Für jede von ihnen können Sie die Komponente :
* Ohne Änderung des Codes der Host-Datenbank: Ausführen einer gemeinsam genutzten Methode der Komponente durch `manuelles` Erstellen einer auf dem Server gespeicherten Prozedur. Der Vorteil ist, dass Sie den Code der Hostbasis nicht ändern müssen. Dies ist besonders nützlich, wenn die Anwendung als kompilierte Version bereitgestellt wird, da so eine Neukompilierung vermieden wird. Der Nachteil ist jedoch, dass Sie die gemeinsam genutzte Methode nach jedem Neustart des 4D Servers erneut ausführen müssen, damit die gespeicherte Prozedur aktiv ist.
* Durch Ändern des Code in der Host Datenbank: Bei dieser Methode wird Code direkt in die Host Datenbank eingefügt. Sie erstellt die Prozedur, die beim Starten des 4D Servers automatisch gespeichert wird, was sehr nützlich ist, um Berichte selbständig und ohne Eingreifen zu erstellen. Es ist eine `automatisierte` Lösung, bei der alles an seinem Platz ist, sobald der Server startet.

> Beide Ansätze haben je nach Kontext und Überwachungsbedarf der Anwendung ihre Vorteile.

**_1/ Berichte alle N Minuten erstellen_**

**_Ohne den Code der Hostbasis zu ändern:_**

* Führen Sie die gemeinsam genutzte Methode `aa4D_NP_Report_Manage_Display` aus 4D Distant aus

* Über einen Dialog der Komponente können Sie die gespeicherte Prozedur starten, um alle N Minuten einen Bericht auf dem 4D Server zu erstellen

**_Indem Sie den Code der Hostbasis ändern:_**

* Kopieren Sie den unten stehenden Beispielcode in die Datenbankmethode `Auf Serverstart` Ihrer Hostdatenbank:

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // to start the stored procedure creating report every 5 minutes
  $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
End if
```

**_2/ Einen einzelnen Bericht erstellen_**

**_Ohne den Code der Hostbasis zu ändern:_**

* Erstellen eines Berichts durch Ausführen der gemeinsam genutzten Methode `aa4D_NP_Util_CreateReport_Serv`

**_Indem Sie den Code der Hostbasis ändern:_**

* Kopieren Sie den folgenden Beispielcode in Ihre Hostdatenbank:

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

* Referenz der Komponente: [4D_Info_Report_v4_89_7_Ref_v41.pdf](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_89_7_Ref_v41.pdf)

* Host-Datenbank (4D 19) mit einigen Beispielen für gemeinsam genutzte Host-Methoden (bitte fügen Sie die Komponente für Ihren Test im Ordner „Components“ hinzu): [4D_Info_Report_Host_T_v9_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v9_19.zip)

* Komponente für Version 4D 20 R10 (auch für Apple Silicon Prozessor kompiliert): [4D_Info_Report_20R10](https://github.com/4d/4D_Info_Report/releases/latest/)

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

# The Format and content of the generated reports

## Overview

This page documents The Format and content of the generated reports in the 4D_Info_Report reference.

## 1/ All generated files have a structured name:

For example, if a report is created on July 31, 2025: “Report_2025_07_31__08_50_17.txt”

All reports name begins with “Report_”, followed by a Time stamp formatted this way:

“YYYY_MM_DD__HH_MM_SS” (Y=year, M=Month, D=day, H=hour, M=minute, S=second)

If a report is created during End of Daylight Saving Time, and detected as older than a previous daily report, it will have a “-2” added to its name: Report_2022_10_25__02_19_55-2.txt

To later process a report via the component, don’t change the name of the document.

## 2/ Each document is generated with a UTF-8 format, with all lines ending with CR+LF, or LF

They are Cross platform (macOS and Windows).

There was 3 byte BOM at the beginning of the document: No more the case in v4.50 (default settings)

## 3/ The content of the report is structured, allowing the component to find searched items.

Also, Reports created with French releases of 4D can have French labels, with parsing compatibility.

---

## A/ The Header: (general description of the computer):

### Overview

This section provides a comprehensive snapshot of the computer system where the report was generated.

```text
Information report version 4.90 (2025-07-31*) V_English
// *(Date of the version of the component)
Date:		31/07/2025	08:50:19  // (Date format depends of the O.S. language setting)
Computer name:                 	AMAZONA-NECV76L
Computer user:                 	Administrator
Manufacturer:                  	Xen
Computer Kind:                 	HVM domU
Total RAM:                     	32768 MB  (32 GB)
Number of Processors:          	1
Processor Name:                	Intel Xeon  E5-2665 0
CPU Speed:                     	2.40 GHz
Total number of Cores:         	8
Total number of CPU threads:   	16
Operating System:              	Windows Server 2016 Standard [1607] (14393.2339)
System language:               	French  (12) fr
IP Address:                    	10.62.43.60
Current System Web Browser:    	Microsoft Edge 138.0 (138.0.3351.109)
Current printer:               	Microsoft Print to PDF
Computer started since:        	4 days, 11 hours, 27 minutes.
```

### Key Information

- The date format in the report header depends on the operating system's language settings
- All timestamps are recorded in local server time
- CPU and memory information helps identify potential performance bottlenecks
- The browser and printer information reflects the system's current capabilities

---

## B/ Description of the 4D Application: (version and build of 4D, version of the built application)

### Overview

This section contains detailed information about the 4D application, including version numbers, build information, release details, and compilation mode.

```text
=========== 4D Information ===========
Application type:                  4D Volume Desktop  (US)
Application version:           	20.7 LTS (F0012006)
Version build of 4D:           	20.7 LTS (101824)
More info on 4D release:       	20.7 LTS Public release  (May 16, 2025)
Version build of Application:      20250731 (20.7 101824) // customized by developer.
Mode:                          	Compiled
(“More info on 4D release” line is added if the build number is identified as a Hotfix or a Public release).
Application:
«C:\4D\__4D_20_7_Product_Line\Bench_20_7\Server_build\Bench_20_7.exe»
PICTURE CODEC LIST: (13)
.4pct .jpg .png .bmp .gif .tif .emf .pdf .svg .wdp .dds .heic .JXL
```

### Notes

- **LTS (Long-Term Support)**: Indicates a stable, long-term support release
- **Build identifier** (F0012006): Internal 4D build reference for tracking
- **Compiled mode**: Application has been compiled (vs. interpreted)
- **Customized**: The version number indicates developer customization
- **Supported codecs**: 13 image formats are natively supported by this 4D version

---

## C/ Description of the Database (size, location, plugins, components, settings):

### Overview

This section provides comprehensive information about the 4D database structure, including file locations, sizes, plugins, components, backup settings, and system resources.

```text
========= 4D Database =========
Main UUID:  (Project)  (Application)
Main UUID: 	9F463893A87C478F9F3127EB3AA30DE0	 (Data)
Structure File:
« C:\4D\__4D_20_7_Product_Line\Bench_v20\Server_build\ Server Database\ Bench_v20.4DZ »
Size:   	6 476 KB		  Modif: 	2025_07_31__08_54_49
Data File:
« D:\4D_v20\4D 20.7\4D Server\Bench-v20.dbase\Bench-v20.4DD»
Size:   	14 589 248 KB		  Modif: 	2025_07_30__17_54_42
<------ Plugins -------
4D Internet Commands
------- Plugins ------>
<------- Plugins Bundle ------
--- Database ---
4D InternetCommands.bundle    Executable Key: 4D InternetCommands     Short Version Key: 20.7 (101824)

------- Plugins Bundle ------>

<------ Components ------- 

4D Labels // (in «Internal User Components», found in «Resources»)
4D Report // (in «Internal User Components», found in «Resources»)
… // Other components (found in «Components», in the Database folder or Application)
------- Components ------> 

<------- Components info ------ 

    --- Database ---
4D_Info_Report_v4.4dbase   release_tag (Manifest):  4.90 for 4D 20
--- Application ---
 4D NetKit.4dbase
4D Progress.4dbase
4D SVG.4dbase
4D ViewPro.4dbase
4D Widgets.4dbase
4D WritePro Interface.4dbase
------- Components info ------>
<------ Backup infos -------
Backup.4DSettings location:
« D:\4D_20\4D 20.7\4D Server\Bench-v20.dbase\Bench-v20\Settings\backup.4DSettings»
Backup.XML Scheduler: 
Daily, every 1 day

Log File: 
(No Log File found.)
Last Backup: 
«E:\_Backup_Files\Bench-v20 [0001].4BK»
Size:    14 589 248 KB     Modif:  2025_07_30__21_01_02

Last Backup Infos: 
( Last Backup date & time (in Backup.XML) : 2025_07_30__21_01_02 )

( GET BACKUP INFORMATION;2 : Err.: 0 : No detected error.)
( GET BACKUP INFORMATION;0 : 2025_07_30__21_01_20 ) 

Next Backup: 
( GET BACKUP INFORMATION;4 : 2025_08_01__21_00_00 )

Preferences Backup Advanced:

<BackupFailure>
TryBackupAtTheNextScheduledDate: False
TryToBackupAfter: 0000_00_00__00_01_00.000
AbortIfBackupFail: False
RetryCountBeforeAbort: 5

(Automatic Restore)
Restore last backup if database is damaged: False
Integrate last log if database is incomplete: True

AutomaticRestart: True

------- Backup infos ------>
---------------------------------------------------- 
Involved disk description:
Disk  NbPart.  Type  Status     Media Type                 Total Size      Description
0      2     SCSI   OK        Fixed hard disk media        102 398 MB    RHEL DISK SCSI Disk Device
Involved volume description:
Letter    Disk    NumPart.      Type             Total Size       FileSystem
C:        0         0          2 (Fixed)           35 837 MB        NTFS
D:        0         1          2 (Fixed)           66 558 MB        NTFS
Involved volume  (free space):
Volume	C:\ (Operating System)                  	      4 217 MB
Volume	D:\                                     	     47 959 MB
----------------------------------------------------
Description of the memory modules:
Locator            Capacity    Speed       Type         Manufacturer
ChannelA_Dimm1       4 GB      2133 MHz    DDR4         Undefined
ChannelB_Dimm1       4 GB      2133 MHz    DDR4         Undefined
ChannelC_Dimm1       4 GB      2133 MHz    DDR4         Undefined
ChannelD_Dimm1       4 GB      2133 MHz    DDR4         Undefined
===========================
<------ Comment -------
(content of a pointed text variable ($3) if passed).
```

### Key Information

- **Database Identifiers**: UUIDs uniquely identify the database project and data
- **Structure File (4DZ)**: Contains the database schema and method definitions
- **Data File (4DD)**: Contains the actual data records (~14.5 GB in this example)
- **Plugins**: Extend 4D with additional functionality (Internet Commands)
- **Components**: Pre-built packages (internal and application-level)
- **Backup settings**: Define automatic backup scheduling and recovery options
- **Disk information**: Shows available disk space and partition layout
- **Memory modules**: Details about installed RAM and specifications

---

## D/ Info on the Tables (num, name, nb records, fields, indexed fields, subtables, triggers):

### Overview

This section contains detailed information about all tables in the database, including record counts, field information, indexes, and trigger descriptions.

```text
========== TABLES ===========
(Triggers description: N = On saving New record, E = On saving Existing record,
D = On Deleting a record), L = On Loading a record (deprecated since v11 SQL).
Total number of records:			58 095 555
Number of tables:	167		Number of valid tables:	167
Total number of valid fields: 		1079
Total number of indexed fields: 	412
Num  Name                        Nb of Records Fields (Index) Trig
T.:    3  Cities  ---------------------      43 607     4  (   1 ) N---
T.:    2  Companies  ------------------      68 850     5  (   2 ) ----
T.:  110  Companies0005  --------------      40 000     5  (   0 ) NE--
T.:  247  Companies0006  --------------      70 000     5  (   0 ) ----
T.:  245  Companies0007  --------------      30 000     5  (   0 ) ----
T.:  243  Companies0008  --------------      40 000     5  (   0 ) --D-
T.:  241  Companies0009  --------------      60 000     5  (   0 ) ----
T.:  239  Companies0010  --------------      50 000     5  (   0 ) ----
T.:  237  Companies0011  --------------      80 000     5  (   0 ) ----
[…]
The table description is optional, you can avoid listing them, hide structure information (only showing the number of records), hide “Invisible” tables, etc.
See ContentMode Value in page 14 for the optional setting of the format of this list.
The total number of records will always be reported. (with option on Invisible tables).
```

### Key Information

- **Total records**: Cumulative count across all tables (over 58M records)
- **Tables**: 167 tables in database; all are valid (no orphaned tables)
- **Indexes**: 412 indexed fields across the database for performance
- **Triggers**: Codes indicate which save/delete events have triggers (N/E/D/L)
- **Table description**: Optional—listing can be hidden, abbreviated, or filtered by visibility
- **ContentMode**: See page 14 for format options (full listing, numbers only, etc.)
- The table listing can be abbreviated with [...] to show representative samples

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./06_pref_graph_svg.md) | [Summary](./01_introduction.md) | [Next](./08_changes.md)
<!-- NAV_BUTTONS_END -->

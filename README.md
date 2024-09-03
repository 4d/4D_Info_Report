[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_4dir.json)](https://github.com/4d/4D_Info_Report/releases/latest/)
[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)]()
[![Downloads](https://img.shields.io/github/downloads/4d/4D_Info_Report/total.svg)](https://GitHub.com/4d/4D_Info_Report/releases/latest/)
![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)
![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)
<br>
[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)]()
[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)]()

![info_report](https://raw.githubusercontent.com/4d/4D_Info_Report/main/images/4DIR.png)

* [English](README.md)
* [French](README.fr.md)
* [German](README.de.md)
* [Japanese](README.ja.md)
* [Spanish](README.es.md)

# About this component?

The component `4D_Info_Report` provides a large number of information:

* about the operating system, the computer and the 4D Application

* on the database: description of the structure, data file, size, settings, etc.

* while the server is running, variation of memory, cache usage, connected users, processes, etc.

<br>

# How to use this component?

**_Procedure n°1:_**

> **Important**
>
> Requires version 20 R6 or higher

* Create a `dependencies.json` file in the `/Project/Sources/` folder

* Copy and paste the text below into the `dependencies.json` file

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

* The component will load automatically after reopening your 4D project

> **Note**
>
> * The component will be present in the folder:
>   * ~/Library/Caches/4D/Dependencies/.github/4d/4D_Info_Report/ (on Mac)
>   * ~\AppData\Local\4D\Dependencies\\.github\4d\4D_Info_Report\ (on Windows)

**_Procedure n°2:_**

Create a folder `Components` next to the structure or application file (if it does not already exist), copy the unarchived component, and restart your 4D or 4D Server.

Then you can directly execute the shared method: `aa4D_NP_Report_Manage_Display` from 4D Remote.

A dialog from the component will let you start the Stored procedure to create reports every N minutes on the Server.

You can also implement in your Host database, this small code in your `On Server startup` method to execute any of the shared methods (they all begins with `aa4D_`):

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // to start the stored procedure creating report every 5 minutes
  $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
End if
```

**_Procedure n°3:_**

You can just create one report using the shared method `aa4D_NP_Util_CreateReport_Serv`.

The created reports (text files) are stored in a created folder `Folder_reports` next to the data file.

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

# How to analyze reports?

You can analyze these reports:

* from a remote 4D by executing the `aa4D_NP_Report_Export_Display` method

* from a single-user 4D by opening the component and clicking on the `File / Local reports compare` menu

<br>

# Download

* reference of the component: [4D_Info_Report_v4_80_Ref_v40.pdf](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_80_Ref_v40.pdf)

* host database (4D 19) with some host shared methods example (please add the component in the "Components" folder for your test: [4D_Info_Report_Host_T_v9_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v9_19.zip)

* component for version 4D 20 R6 (also compiled for Apple Silicon processor): [4D_Info_Report-20-R6.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report-20-R6.zip)

* component for version 4D 20 LTS (also compiled for Apple Silicon processor): [4D_Info_Report-20-LTS.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report-20-LTS.zip)

* component for version 4D 19 R6 (only compiled for Intel/AMD processor): [4D_Info_Report_v4_83_I_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19R6.zip)

* component for version 4D 19 R6 (also compiled for Apple Silicon processor): [4D_Info_Report_v4_83_IS_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19R6.zip)

* component for version 4D 19 (only compiled for Intel/AMD processor): [4D_Info_Report_v4_83_I_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19.zip)

* component for version 4D 19 (also compiled for Apple Silicon processor): [4D_Info_Report_v4_83_IS_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19.zip)

<br>

# Archives

* component for version 4D 18: [4D_Info_Report_v4_65_v18.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_65_v18.zip)

* component for version 4D 17 (only compiled for 64-bit): [4D_Info_Report_v4_33_64-bit_v17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_64-bit_v17.zip)

* component for version 4D 17 (also compiled for 64-bit): [4D_Info_Report_v4_33_v17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_v17.zip)

* host database (v17) with some host shared methods example (please add the component in the "Components" folder for your test: [4D_Info_Report_Host_T_v8_v17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v8_v17.zip)

* component for version 4D 16 (also compiled for 64-bit): [4D_Info_Report_v4_9rZC_v16_rev3.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZC_v16_rev3.zip)

* component for version 4D 15 (also compiled for 64-bit): [4D_Info_Report_v4_9rZ8_v15_rev2.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

* component for version 4D 14 (also compiled for 64-bit): [4D_Info_Report_v4_9rZ2_v14_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

* component for version 4D 13 (also compiled for 64-bit): [4D_Info_Report_v4_9rZ2_v13_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

* component for version 4D 12 (also compiled for 64-bit): [4D_Info_Report_v4_9rZ_v12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ_v12.zip)

* host database (v12) with some host shared methods example (please add the component in the "Components" folder for your test: [4D_Info_Report_Host_T_v6_v12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v6_v12.zip)
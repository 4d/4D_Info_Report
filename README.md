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

# How to install this component?

There are 2 ways to install this component:
* 1/ Automatically: using the dependency manager ([new 4D feature, available from version 4D 20 R6](https://blog.4d.com/integrate-4d-components-directly-from-github/))
* 2/ Manually: by copying and pasting the 4D_Info_Report component into the `Components` folder of the 4D project (works with all versions of 4D)

**_1/ Automatically_**

> This method requires at least version 20 R6 of 4D

* Create a `dependencies.json` file in the `/Project/Sources/` folder

* Copy and paste the text below into this file:

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

* Restart 4D or 4D Server, the component will load automatically after reopening the 4D project

> For your information, the component will be downloaded into the:
> * ~/Library/Caches/4D/Dependencies/.github/4d/4D_Info_Report/ (on Mac)
> * ~\AppData\Local\4D\Dependencies\\.github\4d\4D_Info_Report\ (on Windows)

* Follow one of the 2 ways of using the component (see next paragraph) to generate one or more reports

**_2/ Manually_**

> This method works with all versions of 4D

* Download the version of the component corresponding to your version of 4D (see the `Download` or `Archives` section of this article)

* Create a `Components` folder in the 4D project folder (if no such folder exists)

* Copy the unarchived component to this `Components` folder

* Restart 4D or 4D Server

* Follow one of the 2 ways of using the component below to generate one or more reports

<br>

# How to use this component?

There are 2 ways to use this component:
* 1/ Generate reports every N minutes
* 2/ Generate a report on demand

> Reports (text files) are created in a new `Folder_reports` folder next to the data file.

For each of them, you can use the component:
* Without modifying the code of the host database: Execute a shared method of the component by `manually` creating a procedure stored on the server. The advantage is that you don't need to modify the code of the host database, which is particularly useful if the application is deployed in a compiled version, as it avoids recompilation. However, the disadvantage is that you have to run the shared method again after each restart of the 4D server for the stored procedure to be active.
* By modifying the host database code: This method consists of adding code directly to the host database. It allows you to create the stored procedure automatically when the 4D server starts up, which is very useful for generating reports autonomously and without intervention. This is an "automated" solution, where everything is in place as soon as the server is launched.

> Both approaches have their advantages, depending on the context and monitoring needs of the application.

**_1/ Generate reports every N minutes_**

**_Without modifying the host code:_**

* Run shared method `aa4D_NP_Report_Manage_Display` from 4D Remote

* A component dialog will allow you to start the stored procedure to create a report every N minutes on the 4D server

**_By modifying the host code:_**

* Copy and paste the sample code below into the `On server startup` database method of your host database:

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // to start the stored procedure creating report every 5 minutes
  $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
End if
```

**_2/ Generate a single report_**

**_Without modifying the host code:_**

* Create a report by executing the shared method `aa4D_NP_Util_CreateReport_Serv`

**_By modifying the host code:_**

* Copy and paste the sample code below into your host database:

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

* reference of the component: [4D_Info_Report_v4_90_Ref_v42.pdf](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_Ref_v42.pdf)

* host database (4D 19) with some host shared methods example (please add the component in the "Components" folder for your test): [4D_Info_Report_Host_T_v9_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v9_19.zip)

* component for version 4D 21 R2 (also compiled for Apple Silicon processor): [4D_Info_Report_v4_95_1_21R2.zip](https://github.com/4d/4D_Info_Report/releases/download/4.95.1/4D_Info_Report_v4_95_1_21R2.zip)

* component for version 4D 21 LTS (also compiled for Apple Silicon processor): [4D_Info_Report_v4_95_1_21.zip](https://github.com/4d/4D_Info_Report/releases/download/4.95.1/4D_Info_Report_v4_95_1_21.zip)

* component for version 4D 20 R10 (also compiled for Apple Silicon processor): [4D_Info_Report_v4_95_1_20R10.zip](https://github.com/4d/4D_Info_Report/releases/download/4.95.1/4D_Info_Report_v4_95_1_20R10.zip)

* component for version 4D 20 LTS (also compiled for Apple Silicon processor): [4D_Info_Report_v4_95_1_20.zip](https://github.com/4d/4D_Info_Report/releases/download/4.95.1/4D_Info_Report_v4_95_1_20.zip)

<br>

# Archives

* component for version 4D 19 R6 (only compiled for Intel/AMD processor): [4D_Info_Report_v4_83_I_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19R6.zip)

* component for version 4D 19 R6 (also compiled for Apple Silicon processor): [4D_Info_Report_v4_83_IS_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19R6.zip)

* component for version 4D 19 (only compiled for Intel/AMD processor): [4D_Info_Report_v4_90_2_I_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_2_I_19.zip)

* component for version 4D 19 (also compiled for Apple Silicon processor): [4D_Info_Report_v4_90_2_IS_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_2_IS_19.zip)

* component for version 4D 18: [4D_Info_Report_v4_90_2_18.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_2_v18.zip)

* component for version 4D 17 (only compiled for 64-bit): [4D_Info_Report_v4_33_64-bit_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_64-bit_v17.zip)

* component for version 4D 17 (also compiled for 64-bit): [4D_Info_Report_v4_33_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_v17.zip)

* host database (4D 17) with some host shared methods example (please add the component in the "Components" folder for your test: [4D_Info_Report_Host_T_v8_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v8_v17.zip)

* component for version 4D 16 (also compiled for 64-bit): [4D_Info_Report_v4_9rZC_16_rev3.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZC_v16_rev3.zip)

* component for version 4D 15 (also compiled for 64-bit): [4D_Info_Report_v4_9rZ8_15_rev2.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

* component for version 4D 14 (also compiled for 64-bit): [4D_Info_Report_v4_9rZ2_14_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

* component for version 4D 13 (also compiled for 64-bit): [4D_Info_Report_v4_9rZ2_13_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

* component for version 4D 12 (also compiled for 64-bit): [4D_Info_Report_v4_9rZ_12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ_v12.zip)

* host database (4D 12) with some host shared methods example (please add the component in the "Components" folder for your test: [4D_Info_Report_Host_T_v6_12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v6_v12.zip)
# Installation and Usage Guide

This guide covers all installation and usage options for 4D_Info_Report, including legacy 4D versions and manual setup.

For the recommended modern quick start (4D 20 R6+ with Dependency Manager), see [README](../README.md).

## Installation Methods

### Method 1: Automatic install with Dependency Manager (4D 20 R6+)

This method requires at least 4D 20 R6.

1. Create a file named `dependencies.json` in `Project/Sources/`.
2. Copy the following content:

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

3. Restart 4D or 4D Server.
4. The component is loaded automatically when the project reopens.

Dependency cache locations:
- macOS: `~/Library/Caches/4D/Dependencies/.github/4d/4D_Info_Report/`
- Windows: `~\AppData\Local\4D\Dependencies\\.github\4d\4D_Info_Report\`

### Method 2: Manual install (all 4D versions)

1. Download the component version matching your 4D version.
2. Create a `Components` folder in your project root if it does not exist.
3. Copy the unzipped `4D_Info_Report` component into `Components`.
4. Restart 4D or 4D Server.

For all version-specific download links, see [DOWNLOAD](DOWNLOAD.md).

## Usage Modes

Reports are generated as text files in `Folder_reports` next to the data file.

There are 2 usage modes:
- Generate reports every N minutes
- Generate a single report on demand

For each mode, you can run:
- Without host code modification
- With host code modification (automated startup behavior)

### A) Generate reports every N minutes

#### Without modifying host code

From 4D Remote, run shared method:
- `aa4D_NP_Report_Manage_Display`

A component dialog lets you start a stored procedure that generates a report every N minutes on the server.

#### With host code modification

Add the following code to your host database `On server startup` method:

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // to start the stored procedure creating report every 5 minutes
  $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
End if
```

Why this can be useful:
- No manual restart of the stored procedure after each server restart
- Better fit for autonomous monitoring in production

### B) Generate a single report (on demand)

#### Without modifying host code

Run shared method:
- `aa4D_NP_Util_CreateReport_Serv`

#### With host code modification

Add this code in your host database:

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // to create a single report in "Folder_reports" next to the Data file
  $NP:=New process("aa4D_NP_Util_CreateReport_Serv";0;"$4DIR_NP")
End if
```

## Analyze Reports

You can analyze generated reports:
- From 4D Remote by executing `aa4D_NP_Report_Export_Display`
- From single-user 4D by opening the component and using `File / Local reports compare`

## Related Documentation

- [README](../README.md): modern quick start and production path
- [DOWNLOAD](DOWNLOAD.md): PDF and all component versions by status
- [STATS](STATS.md): download counts by file
- [ARCHIVED_RELEASES](ARCHIVED_RELEASES.md): legacy release references

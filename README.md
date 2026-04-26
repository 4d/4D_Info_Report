[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_4dir.json)](https://github.com/4d/4D_Info_Report/releases/latest/)
[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)]()
[![Downloads](https://img.shields.io/github/downloads/4d/4D_Info_Report/total.svg)](https://GitHub.com/4d/4D_Info_Report/releases/latest/)
![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)
![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)
<br>
[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)]()
[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)]()

![info_report](https://raw.githubusercontent.com/4d/4D_Info_Report/main/images/4DIR.png)

## ℹ️ About this component?

**Production monitoring for 4D environments.**

`4D_Info_Report` provides:
- System, computer, and 4D application details
- Database structure, data file, and settings overview
- Live runtime indicators (memory, cache, users, processes)

---

## 🚀 Quick Start (4D 20 R6+)

**How to add `4D_Info_Report` via the Dependency Manager interface:**

1. Go to **Design → Project Dependencies** on 4D (or **Window → Project Dependencies** on 4D Server)
2. Click the **[+]** button at the bottom of the Dependencies panel
3. Select the **GitHub** tab
4. Enter: `https://github.com/4d/4D_Info_Report`
5. In the dependency rule dialog, select **Follow 4D version** (recommended)
6. Click **Add** and restart 4D to activate the component

> For your information, the component will be downloaded into the:
> * ~/Library/Caches/4D/Dependencies/.github/4d/4D_Info_Report/ (on Mac)
> * ~\AppData\Local\4D\Dependencies\\.github\4d\4D_Info_Report\ (on Windows)

**Reference:** [Integrate 4D components directly from GitHub](https://blog.4d.com/integrate-4d-components-directly-from-github/)

---

## 🏭 Production Usage (Client/Server)

You can schedule recurring reports in client/server mode for continuous production monitoring.

This background reporting is optimized for production and does **not** impact application performance.

## Option A: No host code changes

From 4D Remote, run the shared method:
- `aa4D_NP_Report_Manage_Display`

A component dialog lets you start a stored procedure that will generate a report every N minutes on the 4D server.

**Note:** After each 4D Server restart, you must run this shared method again to reactivate automatic report generation.

## Option B: with host code automation

Add this to your host database `On server startup` method:

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // to start the stored procedure creating report every 5 minutes
  $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
End if
```

> **Important:** Whatever option you choose (**A** or **B**), reports are generated in `Folder_reports` next to the data file.

---

## 📊 Analyze Reports

You can analyze generated reports:
- from 4D Remote by running `aa4D_NP_Report_Export_Display`
- from single-user 4D via `File / Local reports compare`

---

## 📥 Downloads

For all component packages organized by official 4D lifecycle status (current, previous, obsolete/archives), including host samples:
- [Download Page](docs/DOWNLOAD.md)

---

## 📚 Documentation

- [Online Reference](docs/reference/01_introduction.md)

- [PDF Reference](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_97_Ref_v44.pdf)

## 🧭 Additional Resources

For older 4D versions, manual install, one-shot report generation and all advanced usage paths:
- [Installation and Usage Guide](docs/INSTALLATION.md)

For download counters per file:
- [Download Statistics](docs/STATS.md)

For compact archive index and official legacy references:
- [Archived Releases Index](docs/ARCHIVED_RELEASES.md)

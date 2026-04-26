# aa4D_M_Dialogs_Margins_Set

## Overview

This page documents aa4D_M_Dialogs_Margins_Set in the 4D_Info_Report reference.

## Syntax

```
aa4D_M_Dialogs_Margins_Set (topMargin {; leftMargin})
```

| Parameter | Var type | Description |
|---|---|---|
| topMargin | Integer | Minimal top margin (in pixels) for all component dialogs |
| leftMargin | Integer | *(Optional)* Minimal left margin (in pixels) for all component dialogs |

## Description

The `aa4D_M_Dialogs_Margins_Set` command *(invisible)* sets the minimal margins of all component dialogs (Report, Compare, Graph, Export) displayed in the MDI or current screen.

The left margin is an optional parameter. The set values are stored in `4DIR_Preferences.json` under the `<dialogs_margins>` node:

```xml
<dialogs_margins>dialogs_margin_top="56" dialogs_margin_left="8"</dialogs_margins>
```

This method should be executed at first usage of the component to configure dialog positioning for the current environment.

To read the current values, use [aa4D_M_Dialogs_Margins_Get](aa4D_M_Dialogs_Margins_Get.md).

To access the preferences file, execute the shared method [aa4D_M_Show_Preferences](aa4D_M_Show_Preferences.md).

---

## Note for the shared methods description

**«(invisible)»** next to the name of the shared method: This method is not visible in "Execute method…"

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./aa4D_M_Agent_Get_Records_Call.md) | [Summary](./01_introduction.md) | [Next](./aa4D_M_Dialogs_Margins_Get.md)
<!-- NAV_BUTTONS_END -->

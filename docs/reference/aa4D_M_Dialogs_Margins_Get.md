# aa4D_M_Dialogs_Margins_Get

## Overview

This page documents aa4D_M_Dialogs_Margins_Get in the 4D_Info_Report reference.

## Syntax

```
aa4D_M_Dialogs_Margins_Get -> Object
```

| Parameter | Var type | Description |
|---|---|---|
| Result | Object | Object containing the current dialog margin settings |

## Description

The `aa4D_M_Dialogs_Margins_Get` function *(invisible)* returns an object with the current dialog margin settings stored in `4DIR_Preferences.json`:

```json
{"Dialogs_Top_Margin": 56, "Dialogs_Left_Margin": 8}
```

These margins apply to all component dialogs (Report, Compare, Graph, Export) displayed in the MDI or current screen.

To set the margin values, use [aa4D_M_Dialogs_Margins_Set](aa4D_M_Dialogs_Margins_Set.md).

To access the preferences file, execute the shared method [aa4D_M_Show_Preferences](aa4D_M_Show_Preferences.md).

---

## Note for the shared methods description

**«(invisible)»** next to the name of the shared method: This method is not visible in "Execute method…"

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./aa4D_M_Dialogs_Margins_Set.md) | [Summary](./01_introduction.md) | [Next](./04_main_parameter.md)
<!-- NAV_BUTTONS_END -->

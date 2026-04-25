# Presentation

## Overview

This page documents Presentation in the 4D_Info_Report reference.

## Quick Navigation

- [Some information about this component:](#some-information-about-this-component:)
- [Supported language for the interface and the content of the reports:](#supported-language-for-the-interface-and-the-content-of-the-reports:)
- [Supported Operating Systems, processors:](#supported-operating-systems-processors:)
- [Naming convention:](#naming-convention:)

This information component is mainly designed to provide in readable text documents a description of:
- The computer (Hardware / Operating system)
- The version of the 4D Application
- The Host database settings (and tables summary)

---

- **Supported version of 4D (component updated in v4.96.x):**
    - 4D **20** version (up to 4D 21 versions, and later Feature release when available)
    - _4D 18 LTS and 19 LTS versions with similar features are available with v4.96.1_

*Archives of older versions :*
*For 4D 17: version v4.33 (one built for 64-bit only, another one also built for 32-bit)*  
*For 4D 16: version v4.9rZC rev3, for 4D 15: version v4.9rZ8 rev2,*  
*For 4D 14: version v4.9rZ2 rev1, for 4D 13: version v4.9rZ2 rev1,*  
*For 4D 13: version v4.9rZ2 rev1, for 4D 12: version v4.9rZ*

All versions of the component can handle reports created with 4D 21 Rx, 21, 20 Rx, 20, 19 Rx, 19, 18, 17, 16, 15, 14, 13, 12, with English or French description.

---

## Some information about this component:

- It does not require or use plug-ins or another component (including 4D SVG).
- It can be used with any Host database or as a stand-alone starting with **4D 20 (LTS or FR)**.  
  (it will ask for an initial creation of a data file when used stand-alone).
- This component does not create or use table / record in the Host database (or in an external DB).

**Confidentiality:**  
The component does not access or share any record content, resource content, etc...  
It will only describe some basic elements of the structure (number and name of the tables, number of fields or indexes (but not their name or their type), and the number of records for each table. (optional parameter values let you hide some details).  
It will get some details on the computer and operating system, and the path names used for the database and the application.

**Compatibility:**  
4D_Info_Report_v4 can handle reports created by aa4D_Report (since v3-2011), with French or English content (the two possible languages currently used in the reports).

## Supported language for the interface and the content of the reports:
(Based on the release of 4D used: in French with a French release of 4D, otherwise in English.  
The built menu bars of the dialogs match other foreign languages (except Japanese))

## Supported Operating Systems, processors:
All Operating systems compatible with 4D, Intel/AMD processors, Apple Silicon native (19.x, 19R6, 20 and later)

## Naming convention:
- **Name of the component:**  
  The current name of the component is **4D_Info_Report_v4**.  
  (« _v4_ » is for all v4.x versions and may be replaced later by “4D_Info_Report_v5”).

  The current v4.90.x update for 4D 20 LTS or upper are available via the free 4D Github section.  
  Also this pdf documentation, and archives of the components for older 4D versions:

  **Updated archives in January 13, 2026:**
  - 4D_Info_Report_v4.96_1_I_19.zip (I= built for Intel(+AMD) only, compatible Rosetta mode)
  - 4D_Info_Report_v4.96_1_IS_19.zip (IS = built for Intel+AMD+Silicon)
  - 4D_Info_Report_v4_65_18.zip (built for Intel(+AMD) only, compatible Rosetta mode)

  Not updated in January 13, 2026:
  - 4D_Info_Report_v4.83_1_I_19R6.zip (I= built for Intel(+AMD) only, compatible Rosetta mode)
  - 4D_Info_Report_v4.83_IS_19R6.zip (IS = built for Intel+AMD+Silicon)

  Older versions archives ends with the corresponding 4D version: <_12> to <_17>

- **Name of the shared methods** (not changed for historical reasons)  
  The name of the shared methods always begins with <aa4D_*>.

- **Name of the created processes or worker:** always begins with <4DIRReport_> ($ can lead)

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./01_introduction.md) | [Summary](./01_introduction.md) | [Next](./03_list_of_shared_methods.md)
<!-- NAV_BUTTONS_END -->

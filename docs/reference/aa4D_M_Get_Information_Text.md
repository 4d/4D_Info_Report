# aa4D_M_Get_Information_Text

## Overview

This page documents aa4D_M_Get_Information_Text in the 4D_Info_Report reference.

## Description

The **aa4D_M_Get_Information_Text** function lets you get the current text value depending on the selector. `vt_Selector` is a text parameter: it can contain either the string of a numeric integer, or a more explicit name. (If no Array_profiler.json & report were created, these results remain available). These text results are provided from 4D Server if called from 4D Remote.

**Available selectors:**

| Selector (Text or Number) | Description |
|--------------------------|-------------|
| "Array_Profiler" or "0"  | Get the content of the Array_profiler.json |
| "Manufacturer" or "1"    | Get the Manufacturer in the Array_profiler.json |
| "Model Identifier" or "2"| Get the Model Identifier in the Array_profiler.json |
| "Memory" or "3"          | Get the RAM value (MB) in the Array_profiler.json |
| "System" or "4"          | Get the System description in the Array_profiler.json |
| "Nb Processors" or "5"   | Get the Number of Processors in the Array_profiler.json |
| "Processor Name" or "6"  | Get the Processor Name in the Array_profiler.json |
| "CPU Speed" or "7"       | Get the CPU Speed in the Array_profiler.json |
| "Total Nb Cores" or "8"  | Get the Total number of Cores in the Array_profiler.json |
| "Nb CPU threads" or "9"  | Get the Total number of CPU threads in the Array_profiler.json |
| "System Web Browser" or "10" | Get the Default System Web Browser in the Array_profiler.json |
| "4D Internal Build" or "11" | Get the version and build of 4D in the Array_profiler.json |
| "More info 4D release" or "12" | Get More info on 4D (if available) in the Array_profiler.json |
| "Memory modules" or "13"  | Get the description of the Memory modules |
| "Disk" or "14"           | Get the description of the Disk |
| "Volume" or "15"         | Get the description of the Volume |
| "Disk & Volume" or "16"  | Get the description of Disk and Volume |
| "Plugin_List" or "17"    | Get the list of Plugin versions |
| "Component_List" or "18" | Get the list of Component versions |
| "MainUUID" or "19"       | Get the Data file Main UUID |
| "Cache Settings" or "20" | Get the Cache settings (v4.5+) |
| "Scheduler_SP_Minutes" or "21" | Get the number of minutes set for the stored procedure (=0 when run in stand-alone, new in v4.7) |
| "Agent_SP_Seconds" or "22" | Get the number of minutes set for the stored procedure (returns JSON results, =0 when run in stand-alone) |
| "Attention_file" or "23" | Get the text content of the Attention_report.txt file |
| "Cache_Memory_value" or "24" | Get info on the Cache |
| "IPv4" or "25"           | Get the IPv4 and Web Server port of 4D Server |
| "PID" or "26"            | Get the PID of the current 4D Application |

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./aa4D_M_Get_Component_Version.md) | [Summary](./01_introduction.md) | [Next](./aa4D_M_Show_Preferences.md)
<!-- NAV_BUTTONS_END -->

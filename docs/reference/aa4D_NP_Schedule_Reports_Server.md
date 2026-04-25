# aa4D_NP_Schedule_Reports_Server (secured)

## Overview

This page documents aa4D_NP_Schedule_Reports_Server (secured) in the 4D_Info_Report reference.

## Description
The **aa4D_NP_Schedule_Reports_Server** command allows you to manage a Stored procedure on 4D Server, that will create a new report every N minute (or tenth of minutes if <1), so you keep a trace of the usage of your 4D Server.

Later on, you can check the evolution of this usage by parsing the reports via the Compare dialog (called by the shared method: aa4D_NP_Report_Compare_Display)

If you pass no parameter, the default value of 5 minutes will be used.
To stop the stored procedure, just pass 0 as the first parameter when calling this method.

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./aa4D_M_Report_CreateOnServerSee.md) | [Summary](./01_introduction.md) | [Next](./aa4D_NP_Get_Last_Server_Report.md)
<!-- NAV_BUTTONS_END -->

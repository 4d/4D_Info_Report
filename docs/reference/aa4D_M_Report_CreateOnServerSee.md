
# aa4D_M_Report_CreateOnServerSee

## Overview

This page documents aa4D_M_Report_CreateOnServerSee in the 4D_Info_Report reference.

## Description
The **aa4D_M_Report_CreateOnServerSee** command allows you to create a report on the Server, and after a small wait, retrieve the last created report from 4D Server, and display it in the same dialog as when creating a report in Local mode. But from there, you will be able to save it locally.

(If no previous report was created on the Server, this command might miss the last created report and retrieve the previous one. This is because the first report created after the Startup of the application is doing more processing than for later reports, completing a small document named "Array_profiler.json".
In this case, just execute "aa4D_NP_Get_Last_Server_Report" to retrieve the last created report.)

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./aa4D_NP_Util_CreateReport_Serv.md) | [Summary](./01_introduction.md) | [Next](./aa4D_NP_Schedule_Reports_Server.md)
<!-- NAV_BUTTONS_END -->

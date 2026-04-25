# aa4D_NP_Reports_Max_Set_Limit

## Overview

This page documents aa4D_NP_Reports_Max_Set_Limit in the 4D_Info_Report reference.

## Description

The **aa4D_NP_Reports_Max_Set_Limit** command sets the maximum number of last reports to be kept in the folder «Folder_Reports» of the database.

If no value is passed as parameter, this value will not be changed compared to the last stored value. (The default value on 4D Server is 0 at startup).

When a positive value is set, a new worker is called to handle the deletion of the oldest reports. If the limit of existing reports in the folder is reached, the oldest reports will be deleted.

Be aware that the reduction of existing reports to the new limit is not done in one step. The worker will not delete more than 500 (maximum) reports at once to avoid too large disk activity.

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./aa4D_M_Show_Preferences.md) | [Summary](./01_introduction.md) | [Next](./aa4D_NP_Reports_Max_Get_Limit.md)
<!-- NAV_BUTTONS_END -->

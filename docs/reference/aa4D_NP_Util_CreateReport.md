# aa4D_NP_Util_CreateReport

## Overview

This page documents aa4D_NP_Util_CreateReport in the 4D_Info_Report reference.

## Description
The **aa4D_NP_Util_CreateReport** command allows you to display (or retrieve) the detail of the version and build number of an executable or a plug-in.
It works cross-platform, meaning that you can get the build number of an executable file on MacOS, or parse the «Info.plist» of a Mac Application on Windows.
(When you parse a file that contains a «/contents/info.plist», this is the file to select in the dialog to retrieve the information).
If no parameter is passed, a dialog to select the file is displayed, and the result is displayed in an Alert.
If you pass a pointer to a text variable as a first parameter, the content of the Alert will be redirected to the pointed text variable.
If you pass a pointer to a text variable as a second parameter, the pointed text variable must contain the full pathname of the file to be examined.

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./aa4D_M_CreateReport_faceless.md) | [Summary](./01_introduction.md) | [Next](./aa4D_NP_Util_CreateReport_Serv.md)
<!-- NAV_BUTTONS_END -->

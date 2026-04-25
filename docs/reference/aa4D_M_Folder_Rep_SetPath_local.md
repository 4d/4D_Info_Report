# aa4D_M_Folder_Rep_SetPath_local

## Overview

This page documents aa4D_M_Folder_Rep_SetPath_local in the 4D_Info_Report reference.

## Description

The **aa4D_M_Folder_Rep_SetPath_local** function lets you set a new location for the «Folder_Reports» (instead of its default location next to the Data file).

This method must be called after each restart of the Host database to not use the default location.

---

### Example Host method code to use this shared method:

```4d
// Method: aa4D_M_Host_Change_Folder
// (Thomas.Schlumberger@4d.com, February 2024, compatible v19)
#DECLARE($pathLocalFolder : Text)
Var $vb_FolderPath_OK : Boolean
Var $pathLocalFolder : Text
Var $oPathFolder : Object
ARRAY TEXT($at_Components; 0)
COMPONENT LIST($at_Components)
If (Find in array($at_Components; "4D_Info_Report@")>0)
	//$pathLocalFolder:="C:\Component Testing\Subfolder\Another folder\"
	If ((length($pathLocalFolder)>4) & (Position(Folder separator; $pathLocalFolder)>0))
		$oPathFolder:=Folder($pathLocalFolder; fk platform path)
		If ($oPathFolder.exists=True)
			$vb_FolderPath_OK:=True
		Else 
			$oPathFolder.create()
			If ($oPathFolder.exists=True)
				$vb_FolderPath_OK:=True
			End if
		End if
	End if
	If ($vb_FolderPath_OK=False)
		If (Application type=4D Server)
			$pathLocalFolder:=Select folder("Select a folder to store the created reports"; ""; Package open)
			If (OK=0) // dialog cancelled
				CONFIRM("Create a folder 'Folder_reports' on the Desktop?")
				If (OK=1)
					$oPathFolder:=Folder(fk desktop folder; *)
					$pathLocalFolder:=$oPathFolder.platformPath+"Folder_reports"
					$oPathFolder:=Folder($pathLocalFolder; fk platform path)
					If ($oPathFolder.exists=False)
						$oPathFolder.create()
					End if
				End if
			End if
		End if
	End if
	If (OK=1)
		EXECUTE METHOD("aa4D_M_Folder_Rep_SetPath_local"; $vb_FolderPath_OK; ->$pathLocalFolder)
	End if
End if
```

<!-- NAV_BUTTONS_START -->
## Navigation

[Previous](./aa4D_M_Get_Build_4D_Text_Call.md) | [Summary](./01_introduction.md) | [Next](./aa4D_M_Folder_Rep_GetPath_local.md)
<!-- NAV_BUTTONS_END -->

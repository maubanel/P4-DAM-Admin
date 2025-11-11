<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

### Perforce Helix Admin

<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

Tips for Perforce Admins

<br>

---

## LSU Changes Hostname
* It seems like that on Mac OSX the school is altering the result of HOSTNAME and make it look like a different computer when off the LSU network.  For example my mac hostname at home is: Marc’s MacBook Pro but at school my hostname is: 88-66-5a-0e-1c-d6.wlan.lsu.edu
  

## .p4ignore

Place in root folder above project directorty with `.uproject` project name.  Right click and download a linked file [copy here](.p4ignore). Because the folders have no slash in front of them it is any folder names `Saved/` not just root of the `.p4ignore` file.

```
Saved/
Intermediate/
DerivedDataCache/
*.pdb
obj/
*.vcxproj
*.sln
*-Debug.*
FileOpenOrder/
*.DS_Store
```

- Assign `.p4ignore` on each project by adding `p4 set P4IGNORE=.p4ignore`.  Add and submit to repository.

- Stop anyone from creating a new user by typing in command line: `p4 configure set dm.user.noautocreate=2`.  You should receive a response of _For server 'any', configuration variable 'dm.user.noautocreate' set to '2'_ if succesful.



# Issue regarding version control not loading by default
Not saving ini with version control
```
I had to change Saved/Config/Windows/SourceControlSettings.ini to this:

[SourceControl.SourceControlSettings]
UseGlobalSettings=True

It was set to false prior. Once that was done, I loaded the editor, then set up source control again.

[SourceControl.SourceControlSettings]
UseGlobalSettings=True
Provider=Perforce

[PerforceSourceControl.PerforceSourceControlSettings]
Port=[IP ADDRESS]:[PORT]
UserName=[Username]
Workspace=[Workspace]
HostOverride=
```

<br><br>

### Files Check Out by Depot
Someone has accidentally checkout files and will not check them back in.  You can force them to revert with admin privileges.

* `p4 revert -C WORKSPACENAME //DEPOTNAME/...`

### Project Files are Locked
Occasionally project files are locked and no one has them checked out in Unreal.
Run `p4 retype -t binary //DEPOT/...`.  This will unlock **ALL** the files in the repo

### Ignored Files in Depot
There are files/folders in the depot that should be ignored.

Run `p4 obliterate //DEPOTNAME/FilePaths...` to test what files will be obliterated.  If the results are correct then type

`p4 obliterate -y //DEPOTNAME/FilePaths...`

### If typemap is wrong (.uasset should be binary+l), retype all the files in the project by going to a root folder on a workspace and running

`p4 edit -t auto ...`

Submit changes to the server.

### Creating New Branch

Performs a copy and submit in one command when creating new streams.

`p4 populate //PROJECT NAME/BRANCH_SOURCE/... //PROJECT_NAME/BRANCH_DESTINATION/...`

### List All Checked Out Files
`p4 opened -a //depot/Your/Location/...`

### List all clients (Workspaces) on a stream:
`clients -a -S //DeportName/Stream`

### Current P4 Typemap
```
# Perforce File Type Mapping Specifications.
#
#  TypeMap:	a list of filetype mappings; one per line.
#		Each line has two elements:
#
#  		Filetype: The filetype to use on 'p4 add'.
#
#  		Path:     File pattern which will use this filetype.
#
# See 'p4 help typemap' for more information.

TypeMap:
	text //....asp
	text //....cnf
	text //....css
	text //....htm
	text //....html
	text //....inc
	text //....js
	text //....ini
	text //....config
	text //....cpp
	text //....h
	text //....c
	text //....cs
	text //....m
	text //....mm
	text //....py
	text+w //....log
	text+w //....pdm
	text+w //....modules
	text+l //....Unity
	text+l //....prefab
	text+l //....shadergraph
	text+l //....asset
	binary+FS2w //....zip
	binary+Fl //....bz2
	binary+Fl //....rar
	binary+Fl //....gz
	binary+Fl //....avi
	binary+Fl //....jpg
	binary+Fl //....jpeg
	binary+Fl //....mpg
	binary+Fl //....gif
	binary+Fl //....tif
	binary+Fl //....tga
	binary+Fl //....hdr
	binary+Fl //....ext
	binary+Fl //....mov
	binary+Fl //....jar
	binary+Fl //....blend
	binary+Fl //....fbx
	binary+Fl //....obj
	binary+Fl //....bmp
	binary+Fl //....mb
	binary+Fl //....m4a
	binary+Fl //....mp4
	binary+Fl //....aac
	binary+Fl //....wav
	binary+Fl //....wma
	binary+Fl //....docx
	binary+Fl //....pptx
	binary+Fl //....xlsx
	binary+Fl //....png
	binary+Fl //....raw
	binary+Fl //....psd
	binary+Fl //....uasset
	binary+Fl //....umap
	binary+Fl //....upk
	binary+Fl //....udk
	binary+Fl //....ubulk
	binary+l //....ico
	binary+l //....anim
	binary+l //....mtl
	binary+l //....exp
	binary+l //....btr
	binary+l //....doc
	binary+l //....dot
	binary+l //....xls
	binary+l //....ppt
	binary+l //....pdf
	binary+l //....tar
	binary+l //....bin
	binary+l //....class
	binary+l //....war
	binary+l //....ear
	binary+l //....so
	binary+l //....rpt
	binary+l //....cfm
	binary+l //....ma
	binary+l //....pac
	binary+l //....odt
	binary+l //....ods
	binary+l //....odg
	binary+l //....odp
	binary+l //....otg
	binary+l //....ots
	binary+l //....ott
	binary+l //....sxw
	binary+S2w //....exe
	binary+S2w //....exp
	binary+S2w //....dll
	binary+S2w //....lib
	binary+S2w //....app
	binary+S2w //....dylib
	binary+S2w //....stub
	binary+S2w //....ipa
```

* Best to save as a text file (.txt only) then import it: `p4 typemap -i < my_typemap.txt`
* To print and confirm it type `p4 typemap -o`


### DAM
* To limit DAM users from creating projects or repositories go to **Teams** dashboard and click on the user proflie on thg etop right.  Click on **Company settings**.  Go to **Features** and adjust the settings to limit projects.

![companySettings](https://user-images.githubusercontent.com/5504953/195142528-d632a1b8-c01c-47a1-848f-857427d5819d.png)

![restrictingAccess](https://user-images.githubusercontent.com/5504953/195142546-82713ce5-b5a6-4ce2-8d11-6519aeb30e10.png)


<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

### Perforce Helix Admin

<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

Tips for Perforce Admins

<br>

---

## .p4ignore

Place in root folder alongside `.uproject` project name.  Right click and download a linked file [copy here](.p4ignore). Because the folders have no slash in front of them it is any folder names `Saved/` not just root of the `.p4ignore` file.

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


### DAM
* To limit DAM users from creating projects or repositories go to **Teams** dashboard and click on the user proflie on thg etop right.  Click on **Company settings**.  Go to **Features** and adjust the settings to limit projects.

![companySettings](https://user-images.githubusercontent.com/5504953/195142528-d632a1b8-c01c-47a1-848f-857427d5819d.png)

![restrictingAccess](https://user-images.githubusercontent.com/5504953/195142546-82713ce5-b5a6-4ce2-8d11-6519aeb30e10.png)


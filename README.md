<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

### Perforce Helix Admin

<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>



Start-Up Procedure for Operator 1

<br>

---

## .p4ignore
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




<br><br>


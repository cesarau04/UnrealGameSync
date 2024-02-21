# Configuring Perforce
---------------------------

## Recommended Server Settings
The following server settings are recommended but not required for UnrealGameSync

### Set Password Security Level

1. Open P4Admin.
2. Login into your server using the SuperUser account.
3. On the top menu bar go to Administration->Password Security Level... and select 3 (ticket-based authentication required) and press OK.

![screenshot](https://i.imgur.com/blaIc8p.jpeg)

### Set Server Configurations. 

1. Open P4V
2. Login as the SuperUser Account. (Do Not Create A Workspace. leave it as default (optional))
3. On the top menu bar go to Connection->Enviroment Settings make sure it's set to the SuperUser account and press OK.
4. Open CMD (Command Prompt) and enter the following commands.

**Disable Public User Account Creation**

`p4 configure set dm.user.noautocreate=2`

>If everything was set correctly you should get: For server 'any', configuration variable 'dm.user.noautocreate' set to '2'

**Disable Unauthorized Viewing Of Perforce User List**

`p4 configure set run.users.authorize=1`

>If everything was set correctly you should get: For server 'any', configuration variable 'run.users.authorize' set to '1'

**Disable Unauthorized Viewing Of Perforce Config Settings**

`p4 configure set dm.keys.hide=2`

>If everything was set correctly you should get: For server 'any', configuration variable 'dm.keys.hide' set to '2'

>If all commands were successful you can close CMD (Command Prompt) and P4V.

## Configuring Type Map
In order for Perforce to handle the Unreal Engine Source code correctly, we have to tell it how to handle its files using a typemap.

1. Open P4V
2. Login as the SuperUser Account. (Do Not Create A Workspace. leave it as default (optional))
3. On the top menu bar go to Connection->Enviroment Settings make sure it's set to the SuperUser account and press OK.
4. Open CMD (Command Prompt)
5. Type: `p4 typemap` and press enter.
6. It will open a notepad file.
7. Copy the text below and paste it into the notepad file.
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
	binary+w //....exe
	binary+w //....dll
	binary+w //....lib
	binary+w //....app
	binary+w //....dylib
	binary+w //....stub
	binary+w //....ipa
	binary+Sw //....pdb
	text+w //....DotSettings
	text+w //....modules
	text+w //....target
	text+w //....version
	text //....ini
	text //....config
	text //....cpp
	text //....h
	text //....c
	text //....cs
	text //....m
	text //....mm
	text //....py
	text //....json
	binary+l //....uasset
	binary+l //....umap
	binary+l //....upk
	binary+l //....udk
	binary+l //....ubulk
	binary+l //....bmp
	binary+l //....fbx
	binary+l //....mp4
	binary+l //....png
	binary+l //....svg
	binary+l //....uasset
	binary+l //....umap
	binary+l //....wmv
```
8. Save and Close.
9. You should see the following message in the CMD (Command Prompt) window: `Typemap saved.`

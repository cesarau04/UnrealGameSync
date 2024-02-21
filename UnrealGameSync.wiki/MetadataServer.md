# MetadataServer
---------------------------
UnrealGameSync can communicate with a web service to share information between team members. While it can run without this being set up, some of the more powerful collaboration features will not be available:
* Surfacing build results and providing desktop notifications for build breakages
* Allowing users to mark changes as good and bad, and indicate to other team members that they're investigating a problem with the build
* Showing which users are synced to which changes

_**Source: [Epic Games Documentation](https://docs.unrealengine.com/en-US/ProductionPipelines/DeployingTheEngine/UnrealGameSync/Reference/index.html)**_

## Database Setup
1. Open MySQL WorkBench
2. Click on file, Open MySql Script, navigate to this Github project on your computer, under MetadataServer you will see a Setup.sql file select and click on Open.
3. Click on Execute.

![screenshot](https://i.imgur.com/WEhX0C6.jpg)

4. On the top bar click on Server->Users and Privileges
5. Click on Add Account, and Fill in `Login Name` and `Password`
6. Click on the tab `Schema Privileges` and add an Entry for the schema `ugs_db`
7. Under Object Rights Select the following options: SELECT, INSERT, UPDATE, DELETE, EXECUTE
8. Click On Apply

![screenshot](https://i.imgur.com/2axYZsT.jpg)

## Hosting On IIS (Recommended)
1. Open the UnrealGameSync.sln solution
2. Open `appsettings.json`
3. Set username and password in the `MySqlConnection` string that we created in [Database Setup](#database-setup) Step 5.
```
"ConnectionStrings": {
    "MySqlConnection": "server=localhost;UserId=YourUserName;password=YourPassword;"
  }
```
3. Right-click on the project MetadataServer and click on Publish
4. Select Folder as your Target, and click next
5. You can change the folder location of where the files will be exported but that's up to you, click on Finish.
6. Click on Edit Publish Profile (blue pen) behind Target Runtime, and set the following settings.
```
Deployment Mode: Framework-Dependent
Target Runtime: win-x64
```
7. Click on Publish.

![screenshot](https://i.imgur.com/OhFJAy5.gif)

8. Navigate to the directory you published the MetadataServer and Copy all files and folders.
9. Navigate to `C:/inetpub` and create a folder `sites`
10. Inside the folder `sites` create another folder called MetadataServer.
11. Paste all files and folders we copied from the published inside the MetadataServer.
12. Open IIS (Internet Information Services) Manager. (If you don't have IIS installed, you can google how to enable it under windows features I won't cover that in this guide)
13. Right-click on sites and press `Add Website`
14. Enter any name you want for the `Website Name`
15. Under `Physical Path` navigate to `C:/inetpub/sites/MetadataServer` and press OK
16. Under Binding set the Port you would like to use.
17. Leave IP Address to `All Unassigned` 
18. Under `Host Name` type `localhost` (This will only make it work locally, in order for it to work from the outside of the localhost change the IP Address from `All Unassigned` to the IP Address of the PC you are running it from, and leave `Host Name` blank, MetadataServer is not made to be exposed to the public, you can, however, it's not recommended you should use a VPN to access the MetadataServer locally but I will not cover that here)

![screenshot](https://i.imgur.com/NkhJxuP.jpg)

18. Press OK
19. Click on `Application Pools` and you will see the Website we just created.

![screenshot](https://i.imgur.com/RT62eSy.jpg)

20. Right-click the Application Pool that was created for your website.
21. Change the .Net CLR Version to `No Managed Code`

![screenshot](https://i.imgur.com/nwxDv5M.jpg)

22. Press OK
23. Navigate to `http://localhost:yourport/api/latest` in this example I would navigate to `http://localhost:40303/api/latest`
24. You should see something like `{"lastEventId":0,"lastCommentId":0,"lastBuildId":0}` means everything is working.


## Run Without IIS (Not Recommended)
1. Open the UnrealGameSync.sln solution
2. Open `appsettings.json`
3. Set username and password in the `MySqlConnection` string that we created in [Database Setup](#database-setup) Step 5.
```
"ConnectionStrings": {
    "MySqlConnection": "server=localhost;UserId=YourUserName;password=YourPassword;"
  }
```
4. Right-click on the project MetadataServer and click on Build
5. Navigate to `http://localhost:5000/api/latest`
6. You should see something like `{"lastEventId":0,"lastCommentId":0,"lastBuildId":0}` means everything is working.
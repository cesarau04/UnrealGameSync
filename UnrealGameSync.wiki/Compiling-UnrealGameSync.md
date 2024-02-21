# Compiling UnrealGameSync
---------------------------

### Required Software
* Wix 3.8
* ASP.NET 5 SDK (MetadataServer) [Optional]
* ASP.NET 5 Hosting Bundle (MetadataServer) [Optional]
* Game Development with C++ & .Net Framework 4.5 or higher.

## Install Wix Toolset Build Tools & Extension
1. Download and Install Wix Toolset Build Tools [https://wixtoolset.org/releases/](https://wixtoolset.org/releases/)
2. Download and Install Visual Studio Extension
- [Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2017Extension)
- [Visual Studio 2019](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension)

## Install ASP.NET 5 SDK & Hosting Bundle (MetadataServer) [Optional]
1. Download and Install ASP.NET 5 SDK & Hosting Bundle [https://dotnet.microsoft.com/download/dotnet/5.0](https://dotnet.microsoft.com/download/dotnet/5.0)

_**To compile the MetadataServer you need the SDK, if you are hosting the server somewhere else and only need to run it you only need the Hosting Bundle.**_

## Configuring UnrealGameSync
Open UnrealGameSync Solution `Engine\Source\Programs\UnrealGameSync\UnrealGameSync.sln`

### ApiUrl (MetadataServer) [Optional]
***
1. Open Project UnrealGameSync
2. Open file DeploymentSettings.cs
3. Set the ApiUrl variable to the URL from the MetadataServer IP:PORT `http://192.168.1.10:43404/`
![screenshot](https://i.imgur.com/VUzQhJj.jpeg)

### DefaultIssueApiUrls
***
`Coming Soon`

### UrlHandleIssueApi
***
`Coming Soon`

### DefaultDepotPath
***
1. Open Project UnrealGameSync
2. Open file DeploymentSettings.cs
3. Set the DefaultDepotPath variable to the correct Depot path `"//YourDepotGameName/UnrealGameSync"`
![screenshot](https://i.imgur.com/8AFfaxN.jpg)

### Compiling UnrealGameSync
1. Compile the solution in Release mode.
2. In the main directory you will see UnrealGameSync.msi this is the installer to install UnrealGameSync on your local pc & team members, how you transfer this installer is up to you, either thru Perforce or in a different way.

### Distributing UnrealGameSync & Updating UnrealGameSync
1. Create a folder named UnrealGameSync in your depot /YourDepotName/UnrealGameSync
2. Create 2 folders named Release & UnstableRelease inside the UnrealGameSync folder we created in step 1.
3. Place all compiled files in UnrealGameSync compile step x inside the Release folder.
![screenshot](https://i.imgur.com/pgHjpQn.gif)

### Recommended
> I recommend to create a local depot called UnrealGameSync and place your installer and place update folders in there as well as explained in [What We Us](creating-perforce-depots#what-we-use)
> So your path under [DefaultDepotPath](defaultdepotpath) will be `//UnrealGameSync` and for [Distributing UnrealGameSync & Updating UnrealGameSync](distributing-unrealgamesync--updating-unrealgamesync) you create the folders in the root directory of the depot `UnrealGameSync` and place the installer (.msi) in the root as well so it's easy'er for your team members to get.

> This doesn't apply if you're using a single (local) depot to store your project, you are not branching your project in that case.
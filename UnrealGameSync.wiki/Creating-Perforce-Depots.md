# Creating Perforce Depots
---------------------------
There are several ways you can set up Perforce Depots, choose what makes the most sense for your game and/or needs.

> We use a combination of both Multi Depot and Single Depot (Type Local), the Single Depot is used for UnrealGameSync Installer & Update mechanics, explained more in detail under [What We Use](#what-we-use).

## Single Depot (Type Local)

[Single Depot (Type Local)](#creating-single-depot-type-local)
This is the most simple of the three, you can see it as a folder with file/version control and recovery,
If you are working on your own and need a version control solution this works well.

Perforce comes by default with a single depot (type local) called Depot, if you wanna learn more about perforce depot type local take a look at the Perforce website.

## Single Depot (Type Stream/Branch)

[Single Depot (Type Stream/Branch)](#creating-single-depot-type-streambranch)
This is the same as [Single Depot (Type Local)](#single-depot-type-local) but instead, we use the type stream which means we can branch into different versions of the project, this is similar to how GitHub works with branches if you used that before.
>The only issue with this setup is that there is no easy or structured way to update the Unreal Engine source code, this could potentially break your game and push back development until the issues/conflicts are fixed, in case your team wants to keep up to date with Epic's changes and Unreal Engine's releases, the [Multi Depot (Type Stream/Branch)](#multi-depot-type-streambranch) is a better solution for that approach.

![screenshot](https://i0.wp.com/kahncode.com/wp-content/uploads/2019/11/p4_streams.png?w=727&ssl=1)
> Source: kahncode.com

This type of depot is recommended if you work in a team and works for a single release/shipped game or an active development continues game where you continue to add new features and content.

The idea behind this setup is that you have a single main depot where all changes go including new features/content, and bug fixes from your live game.

![screenshot](https://i.imgur.com/ci3fLw7.jpg)

You can have single or several Development branches where your team works, each team can have a depot they work on, like a coding team, and an artist team and you merge code from the dev branches into the main branch.

![screenshot](https://i.imgur.com/Xhd7hgl.jpg)

When you have a stable and/or want to make a release version ready you create a new depot based on the main with stream type release, you can base releases on release type depot this can be useful for staging. 

![screenshot](https://i.imgur.com/mWsY8ue.jpeg)

## Multi Depot (Type Stream/Branch)

[Multi Depot (Type Stream/Branch)](#creating-multi-depot-type-streambranch)
This is the same as [Single Depot (Type Stream/Branch)](#single-depot-type-streambranch) but instead, you don't have 1 main depot but 3 or several this approach works best if your working in a team and you would like to periodically update the Unreal Engine Release, this works also if you customize the Engine but would like to also migrate to bug fixes from Epic.

For this example, we are going to take the approach of having 3 Depots

The concept of this approach is described in Unreal Engines Documentation:
![screenshot](https://docs.unrealengine.com/Images/ProgrammingAndScripting/ProgrammingWithCPP/DownloadingSourceCode/UpdatingSourceCode/Perforce_IntegratingMergingBranching.webp)
> Source: [docs.unrealengine.com](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/ProgrammingWithCPP/DownloadingSourceCode/UpdatingSourceCode/index.html)

Instead of a single main depot we have 3
- Dev (Development Depot For Our Game/Engine)
- Epic (Holds an untouched version of Unreal Engines Source code)
- MergeTest (For testing the merge between our current Dev Depot and Epic Depot)

![screenshot](https://i.imgur.com/EaxBIS6.jpg)

We can create single or several Development depots just like the standard stream option.

![screenshot](https://i.imgur.com/jHLJIvm.jpg)

We can create several release depot just like the standard stream option.

![screenshot](https://i.imgur.com/OBYzQux.jpeg)

But now we have the option to migrate from `Epic` -> `MergeTest`
and from `Dev` -> `MergeTest` creating a version of your Game/Project with a newer version of the Engine.

We can then test the `MergeTest`for issues, if everything is oke we can merge `MergeTest` -> `Dev` and create a new development depot, and continue development using the new version, and repeat the cycle when needed.

![screenshot](https://i.imgur.com/nErj3e9.jpg)

## Creating Single Depot (Type Local)
1. Open P4Admin.
2. Login into your server using the SuperUser account.
3. Click on the tab called Depots
4. Right-click in the list view and click on `New Depot`
5. Enter the name of your depot, this can be anything you want.
6. Select local under the Depot Type

![screenshot](https://i.imgur.com/iPnbGYz.jpg)

## Creating Single Depot (Type Stream/Branch)
1. Open P4Admin.
2. Login into your server using the SuperUser account.
3. Click on the tab called Depots
4. Right-click in the list view and click on `New Depot`
5. Enter the name of your depot, this can be anything you want.
6. Select stream under the Depot Type

![screenshot](https://i.imgur.com/qeANd5Z.jpg)

## Creating Multi Depot (Type Stream/Branch)
There is no difference with [Single Depot (Type Stream/Branch)](#creating-single-depot-type-streambranch)

## What We Use.
We use a combination of [Multi Depot (Type Stream/Branch)](#multi-depot-type-streambranch) and [Single Depot (Type Local)](#single-depot-type-local).

![screenshot](https://i.imgur.com/4zCckuC.jpeg)

UnrealGameSync is a local type depot to host UnrealGameSync installer and to host the Update mechanics, the reason for this because UE4 is a [Multi Depot (Type Stream/Branch)](#multi-depot-type-streambranch) which means that each branch the path of UnrealGameSync will change which will cause problems for UGS to load the applications update mechanics, this way there is only 1 location and 1 path for UnrealGameSync using depot type local.

UE4 is a [Multi Depot (Type Stream/Branch)](#multi-depot-type-streambranch) and all the reason to use it, is explained earlier.


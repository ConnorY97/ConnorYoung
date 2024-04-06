---
Title: Age Of Empires
date: 2024-03-09 09:00:00
categories: [Portfolio, C#]
---
Working on creating a simple AOE clone!

The prompt for this idea was all the adds on TikTok of small games with lots of moving pieces on the screen. They are all money sinks where to make any real progress you just need to keep swiping ur card. So I thought I'd just make my own.

The current idea is to have some villagers who can collect resources, hardest part currently is getting a view/perspective that would allow fine control while showing everything on the screen.

Currently, I have two collectable resources that `Upgrade` the `Humans`. Wood allows for the `Humans` to move fast, logic? None. Ore allows them to `Interact` faster. Recently implemented a simple particle system when they `Interact` so I can actually tell things are happening. I am going to use some place holder object's but this could also be an opportunity to learn some more simple Blender so I can quickly whip together temp objects when I need to.

UI is a still a work in progress:
![AOE UI](/assets/img/AoeUI.png){: width="486" height="294" }

Things I am practicing:
1. Inheritance: I have the base [Resources](https://github.com/ConnorY97/AOE/blob/main/Assets/Scripts/Resource.cs) class which all interactable resources will inherit from. This is useful as I can put all the boilerplate code in the base class which all children will require. I have used this a few times, but never anything in depth.
2. Object Orientated programming: I can confirm I am not doing this well. There is a bit of spaghetti code going on, but things are slightly modular. I am trying to look forward when implementing solutions. The best examples of this is the `ResourceUI` 
```
public void IncrementResource(Dictionary<ResourceType, float> returnResources)
{
    // Pass over returned resources
    for (int i = 0; i < (int)ResourceType.MAX; i++)
    {
        mTotalResources[(ResourceType)i] += returnResources[(ResourceType)i];


        // Get rid of this once I have all the UI set up
        // Bandaid to stop out of bounds error
        if (i < mResourceCountUI.Count)
        {
            mResourceCountUI[i].text = mTotalResources[(ResourceType)i].ToString();
        }
    }

    CheckUpgradeAvailability();
}
```
Here I am using two lists, `mTotalResources` and `mResourceCountUI`. As long as I add the UI in the correct order, then I will be able to add un infinite amount of resources and UI without having to touch this code. I am quite happy with it.
3. Naming Conventions and Getters and Setters: I am using the `m` prefix for my member variables. I normally do not use this as I find it annoying when used in conjunction with Intlisense. As I will be thinking of `ore` so I type `ore` but of course I do not have `ore` I have `mOre`. However, it has been useful I have found in functions where I cannot come up with better names that what the member variable is called. But that is now fine as I can just use `mOre = ore`! In terms of Getters and Setters an example is
```
private Resource mTarget = null;
public Resource Target
{
    set
    {
        if (value != null)
        {
            mTarget = value;

            mAgent.SetDestination(mTarget.transform.position);

            mArrived = false;
        }
    }

    get { return mTarget; }
}
```
Here I can do error checking on the passed in value `if (value != null)` then followed by some code. This is very cool, I have never used this before and it has so far been super helpful.

I will update again when there is more progress!

[Github](https://github.com/ConnorY97/AOE)

|Commits|Message|
|-------|-------|
|[00](https://github.com/ConnorY97/AOE/commit/d5e7404325de290590a17934b66e8617b1a2cf30)|Inital Commit|
|[01](https://github.com/ConnorY97/AOE/commit/75c3b03cd29364728890e9a0afb30cbb54d56df7)|Adding Unity proj|
|[02](https://github.com/ConnorY97/AOE/commit/83dc69537b632e8805cda318b444c85e9f75e4fd)|Beginning work.<br>Added:<br>1. Game Manager<br>2. Tree<br>3. Prefabs for each<br><br>Need to work on:<br>Everything else|
|[03](https://github.com/ConnorY97/AOE/commit/e7b5bdd7b340bf380d37f13561c55da2544b0908)|Currently I am spawning 100 tree which are placed randomly on the ground. A single brave human is being spawned with them, he can currently walk up to any of the trees and merge with them (Not intended behavior).<br><br>Things to do:<br>Some how update the nav mesh when the trees are added to agent's avoid them.<br>Spawn more humans<br>Better trees<br>Better humans.<br><br>PROGRESS|
|[04](https://github.com/ConnorY97/AOE/commit/bf1a0cdc55928be8fb222a6a081f4e7f0d48e8b1)|Improvments,<br>I made some improvements to the UI. But, it is still very spaghetti and it has very little room for expansion. Will still need to look into inheritance again.<br><br>But making progress!|
|[05](https://github.com/ConnorY97/AOE/commit/627eff4c02ba05fc613f4303358ec4a75d312475)|The great refactoring has begun!<br>It is always easier to reactor as you go rather than doing it at the end. If any of my previous projects are to go by. Anyway, created inheritance for `resource` objects as it will improve expandability and I need to work on it. Removed a lot of the functionality for now but it will still be easer starting again. Lots to come!|
|[06](https://github.com/ConnorY97/AOE/commit/2bf0b28c571504eeec29c6652fc2114e107592750)|More work on Resources<br>Back to being able to chop down trees and return them to the `TownCentre`. Started setting up the UI for resource count, however the hitpoints are still not working as expected. Good work though.|
|[07](https://github.com/ConnorY97/AOE/commit/d894bf5fe070831a8fdffa1c94b8c808424c4989)|THE SPAGHETTI<br>So, I am not sure if things are getting better or worse lol.<br>Changed the Resource class to an `Abstract` class which I have never used before. I believe the benefit is that I can have empty functions?<br><br>I will continue to work on making things more modular which would be nice, but making good progress.<br><br>Implemented some nicer UI for when resources have been retrieved. Next it to use the retrieved resources to improve the Town Centre/Humans.<br><br>Looking good so far.|
|[08](https://github.com/ConnorY97/AOE/commit/c9fe87db4beddac0cf70a42d66106227723a5678)|RAYS<br>I have improved the way `Humans` return `Home` as I noticed they kept returning to the same point and it looked funny. Kinda like they were trying to que. Now they will raycast from their current position to the house so that they all get a different point to return to, makes it feel a lot better.|
|[09](https://github.com/ConnorY97/AOE/commit/810e053be9dbf61b4eb64e441093858de8945b7a)|SPACING<br>Implemented a spacing system for random tree spawning to prevent them from occupying the same space. Will need to to some clean up soon. Added some code comments.|
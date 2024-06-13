---
Title: Age Of Empires
date: 2024-03-09 09:00:00
categories: [Portfolio, C#]
image:
    path: /assets/img/AOE.png
    alt: AOE
---
Working on creating a simple AOE clone!

Play on itch IO here: [AOE](https://connory97.itch.io/aoe) or below!

<details><summary>Age Of Empires</summary>
<iframe frameborder="0" src="https://itch.io/embed-upload/10128116?color=333333" allowfullscreen="" width="1000" height="720"><a href="https://connory97.itch.io/aoe">Play AOE on itch.io</a></iframe>
</details>
<br>
The prompt for this idea was all the adds on TikTok of small games with lots of moving pieces on the screen. They are all money sinks where to make any real progress you just need to keep swiping ur card. So I thought I'd just make my own.

The current idea is to have some villagers who can collect resources, hardest part currently is getting a view/perspective that would allow fine control while showing everything on the screen.

Currently, I have two collectable resources that `Upgrade` the `Humans`. Wood allows for the `Humans` to move fast, logic? None. Ore allows them to `Interact` faster. Recently implemented a simple particle system when they `Interact` so I can actually tell things are happening. I am going to use some place holder object's but this could also be an opportunity to learn some more simple Blender so I can quickly whip together temp objects when I need to.

UI is a still a work in progress: <br>
![AOE UI](/assets/img/AoeUI.png){: width="486" height="294" }

### Things I am practicing:
1. Inheritance: I have the base [Resources](https://github.com/ConnorY97/AOE/blob/main/Assets/Scripts/Resource.cs) class which all interactable resources will inherit from. This is useful as I can put all the boilerplate code in the base class which all children will require. I have used this a few times, but never anything in depth.
2. Object Orientated programming: I can confirm I am not doing this well. There is a bit of spaghetti code going on, but things are slightly modular. I am trying to look forward when implementing solutions. The best examples of this is the `ResourceUI`
```c#
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
```c#
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

### Issues
I found an issue! Can you figure it out?
```c#
// Check again all the current existing resource positions
for (int y = 0; y < mResourcePositions.Count; y++)
{
    float dist = Vector3.Distance(newPos, mResourcePositions[y]);
    // While the distance is less than desired
    while (dist < mSpawnDistance)
    {
        // Keep looking for a new position till one is found
        newPos = new Vector3(UnityEngine.Random.Range(-x, x), yHeight, UnityEngine.Random.Range(-z, z));
        dist = Vector3.Distance(newPos, mResourcePositions[y]);
    }
}
mResourcePositions.Add(newPos);
```
The issue with the original function was, when a resource found it was too close to another. It would simply just be moved on top of another. Found a solution `Physics.OverlapSphere()`. Simple right? WRONG. So many issue, with my new Trees and Rocks being complex shapes that might have broken the check? The instantiate function not actually placing the objects? Unity not actually being able to keep up with placing the objects and checking if they are overlapping? No clue. But I did find a solution in the end.
1. I instantiate all the `Resources` at `Vector3(100,100,100)`.
2. Using an Enumerator to implement a delay between resource placement.
3. This seems to work?

This is the new function:
```c#
private Vector3 GetFreePosition(Bounds spawnBounds, float yHeight)
{
    float x = spawnBounds.extents.x;
    float z = spawnBounds.extents.z;
    // To stop resources spawning on top of each other
    //  First we give it a position
    Vector3 newPos = new Vector3(UnityEngine.Random.Range(-x, x), yHeight, UnityEngine.Random.Range(-z, z));

    // Trying a new method for spawning objects.
    // Rather than going through a list of position, I will shpere cast at the spawn location a check if there is anything other than the ground there.
    var checkResult = Physics.OverlapSphere(newPos, mSpawnDistance);

    // Recursion keep checking till we find a free stop.
    // Hopefully this will help with the debugging.
    if (checkResult.Length > 1)
    {
        newPos = GetFreePosition(spawnBounds, yHeight);
    }

    Debug.Log(checkResult.Length.ToString());
    // Assign the free position
    return newPos;
}

IEnumerator PlaceObjects()
{
    //Print the time of when the function is first called.
    Debug.Log("Started Coroutine at timestamp : " + Time.time);

    //yield on a new YieldInstruction that waits for 5 seconds.

    for (int i = 0; i < mObjects.Count; i++)
    {
        MeshCollider groundMesh = mGround.GetComponent<MeshCollider>();
        Bounds bounds = groundMesh.bounds;
        mObjects[i].transform.position = GetFreePosition(bounds, 0.0f);
        yield return new WaitForSeconds(0.125f);
    }
    //After we have waited 5 seconds print the time again.
    Debug.Log("Finished Coroutine at timestamp : " + Time.time);
}
```

### Fun Stuff
The fun stuff that I did do today was create a `Tree` and `Rock` in Blender! It is a good first attempt, I can put a lot more detail into the trees and add some actual ore lumps in the rocks but they are good for now!
<br>
![Tree](/assets/img/tree.png){: width="243" height="147" .normal}
![rock](/assets/img/rock.png){: width="246" height="200" .normal}

## GitHub Actions
I set up a GitHub actions like I did for [Balls](/posts/Balls#github-actions). Which means that the game is being updated on the build branch and posted to Itch.

[Github](https://github.com/ConnorY97/AOE)

|Commits|Message|
|-------|-------|
|[1](https://github.com/ConnorY97/AOEd5e7404325de290590a17934b66e8617b1a2cf30) | Initial commit|
|[2](https://github.com/ConnorY97/AOE75c3b03cd29364728890e9a0afb30cbb54d56df7) | Adding Unity proj|
|[3](https://github.com/ConnorY97/AOE83dc69537b632e8805cda318b444c85e9f75e4fd) | Beginning work.<br>Added:<br>1. Game Manager<br>2. Tree<br>3. Prefabs for each<br>Need to work on:<br>Everything else|
|[4](https://github.com/ConnorY97/AOEe7b5bdd7b340bf380d37f13561c55da2544b0908) | TREES!<br>Currently I am spawning 100 tree which are placed randomly on the ground. A single brave human is being spawned with them, he can currently walk up to any of the trees and merge with them (Not intended behavior).<br>Things to do:<br>Some how update the nav mesh when the trees are added to agent's avoid them.<br>Spawn more humans<br>Better trees<br>Better humans.<br>PROGRESS|
|[5](https://github.com/ConnorY97/AOE418aea5367fc32f16b6750ddf441767490f47144) | Good work!<br>The human can now interact with a tree and cut it down! When it has been cut down, it will disappear and the human will return to the house. Have some UI now which will let you know when you have correctly selected a human, need to add trees and other objects. There is HitPoints UI but it is very basic.<br>Very very spaghetti code right now, which is not great. But it currently works.<br>Things to do:<br>Improve UI<br>Look into refactoring early<br>Animations<br>Improve current assets|
|[6](https://github.com/ConnorY97/AOEbf1a0cdc55928be8fb222a6a081f4e7f0d48e8b1) | Improvements,<br>I made some improvements to the UI. But, it is still very spaghetti and it has very little room for expansion. Will still need to look into inheritance again.<br>But making progress!|
|[7](https://github.com/ConnorY97/AOE627eff4c02ba05fc613f4303358ec4a75d312475) | The great refactoring has begun!<br>It is always easier to reactor as you go rather than doing it at the end. If any of my previous projects are to go by. Anyway, created inheritance for `resource` objects as it will improve expandability and I need to work on it. Removed a lot of the functionality for now but it will still be easer starting again. Lots to come!|
|[8](https://github.com/ConnorY97/AOE2bf0b28c571504eeec29c6652fc2114e10759275) | More work on Resources<br>Back to being able to chop down trees and return them to the `TownCentre`. Started setting up the UI for resource count, however the hit points are still not working as expected. Good work though.|
|[9](https://github.com/ConnorY97/AOEd894bf5fe070831a8fdffa1c94b8c808424c4989) | THE SPAGHETTI<br>So, I am not sure if things are getting better or worse lol.<br>Changed the Resource class to an `Abstract` class which I have never used before. I believe the benefit is that I can have empty functions?<br>I will continue to work on making things more modular which would be nice, but making good progress.<br>Implemented some nicer UI for when resources have been retrieved. Next it to use the retrieved resources to improve the Town Centre/Humans.<br>Looking good so far.|
|[10](https://github.com/ConnorY97/AOEc9fe87db4beddac0cf70a42d66106227723a5678) | RAYS<br>I have improved the way `Humans` return `Home` as I noticed they kept returning to the same point and it looked funny. Kinda like they were trying to que. Now they will Raycasts from their current position to the house so that they all get a different point to return to, makes it feel a lot better.|
|[11](https://github.com/ConnorY97/AOE810e053be9dbf61b4eb64e441093858de8945b7a) | SPACING<br>Implemented a spacing system for random tree spawning to prevent them from occupying the same space. Will need to to some clean up soon. Added some code comments.|
|[12](https://github.com/ConnorY97/AOE2a75c8edb700ab1c42184d3cfa28b14fb29d02fe) | Code clean up and Uniqueness<br>Lots of clean up, using the private/public names of vars to reduce the number of functions and make things a bit easier to read.<br>Added a bit more uniqueness to the humans created. Their materials and icons will not have a different color assigned at creation to it is a bit easier to see which `Human` you have selected at any time.<br>I want to now work on the first improvement: movement speed! You will need 50 wood to increase the human move speed.|
|[13](https://github.com/ConnorY97/AOE01f536569e5c55218000896a6f6227be23856832) | SPEED<br>Implemented the first upgrade, SPEED. When the humans return 50 wood, it is possible to increase their speed. There is absolutely 0 juice. Maybe I could use some sort of sprite on each of the `Humans` when the upgrade is applied.<br>Things to investigate:<br>- Why when you increase the movement speed of the `NavMeshAgents` do they start to overshoot their destinations!??! Such fun.|
|[14](https://github.com/ConnorY97/AOE746052d722f78aa36d8acc9270a4fc93b73cc5fe) | Movement improvements.<br>So the `NavMesh Agent` is dumb. So I spent some time fixing that. Spawning the humans before the trees so they are higher in the Unity hierarchy and easier to find for debugging.|
|[15](https://github.com/ConnorY97/AOE9e642f789c3583b007f4b507efe672cb1379c4f1) | ORE!<br>Added a new collectable `Ore`! I think this will improve `Interaction` time, reducing the time it takes to collect resources. Also improved the villager icon, but it looks a bit funky with the color matching. Implemented a `mResourcePositions` for spawning checking rather than going through each resource list to make sure everything is spawning correctly. Did some more code clean up and added some more functions for boiler plate code. Happy with the progress!|
|[16](https://github.com/ConnorY97/AOE90687cce68dbd525467a3c818bb69a1e8acc3d77) | MORE UPGRADES!<br>The interaction speed can be improved after gathering ore! Improved the upgrade function, cleaned up some redundant functions and improved checking if upgrades are even available.|
|[17](https://github.com/ConnorY97/AOEb735b9c0fdc7619828f59e90e87e4c247aee2aea) | Improving Nav Agent Values|
|[18](https://github.com/ConnorY97/AOEd4099ca59dcf136ced30a8333337c2d6031cc389) | Pain!<br>Cools things first!<br>Created Trees and Rocks in Blender to replace the terrible Unity objects I was using before, which has greatly improved the look of the game already.<br>The not so cool stuff.<br>So, I found an issue with the `Resource` placement. The issue with the original function was, when a resource found it was too close to another. It would simply just be moved on top of another. Found a solution `Physics.OverlapSphere()`. Simple right? WRONG. So many issue, with my new Trees and Rocks being complex shapes that might have broken the check? The instantiate function not actually placing the objects? Unity not actually being able to keep up with placing the objects and checking if they are overlapping? No clue.<br>But I did find a solution in the end.<br>1. I instantiate all the `Resources` at `Vector3(100,100,100)`<br>2. Using an Enumerator to implement a delay between resource placement.<br>3. This seems to work?<br>This was very annoying but I got it working in the end!<br>Good stuff!|
|[19](https://github.com/ConnorY97/AOEe710f50391e73d704b59f38f98a2b97847a29144) | Create activation.yml|
|[20](https://github.com/ConnorY97/AOE1a71b807b62ea370ac931f4c7a87736723d1aec7) | Create main.yml|
|[21](https://github.com/ConnorY97/AOE74f422b74814c664957652652dab3e04b24f2612) | Testing WebGL build and set up Build action|
|[22](https://github.com/ConnorY97/AOE9a7e8cb1d20f990b9237a1d5c08bcf391f6f4b09) | Correcting branch name|
|[23](https://github.com/ConnorY97/AOE6361c95c9e8e666f50f4c4a1702cf7a554763b7c) | Correcting project path|
|[24](https://github.com/ConnorY97/AOEba53c52dc48f12b248f528bfa3a308b13edbac48) | Testing Itch.io Upload|
|[25](https://github.com/ConnorY97/AOE6b55bde6c1a4f8c3c2d18e63796a9ca15c5ccae4) | Correcting caching path|
|[26](https://github.com/ConnorY97/AOE5f146b7f2f483c01f92b5bef0f4daa97bf8b0920) | Trying to find correct build location|
|[27](https://github.com/ConnorY97/AOE4908b2e52d04c31d1a0dc1671c457157afc08b11) | Trying to fix caching|
|[28](https://github.com/ConnorY97/AOEde8a3e6ab7ddacebbaa97cd2012662812097ab4d) | Testing cache and build location|
|[29](https://github.com/ConnorY97/AOE55a4df0dbd09f5c97c5c908a3461038c5b007c08) | Trying a different restore key|
|[30](https://github.com/ConnorY97/AOE93c712467f435876793ff8c091e7412de89ffa73) | Trying a new path|
|[31](https://github.com/ConnorY97/AOE8faac8cca3ca6202625ede3abf026235e577fbd3) | Trying new build path|
|[32](https://github.com/ConnorY97/AOE3041a83fe3619ac1064081dd9ad9cbdcf84b6b96) | Download the artifacts duh|
|[33](https://github.com/ConnorY97/AOE890b8bc4a81e07f2e660240456f17325d93894bf) | Uploading to the correct itch page|
|[34](https://github.com/ConnorY97/AOE141d19053242c5ec641591c24018106afd521536) | Improvements<br>Improved camera placement, humans spawning and some code clean up.|
|[35](https://github.com/ConnorY97/AOE18e90d385818ddb66a6c75337cec0d31b7ba189d) | State of the game<br>I am happy wit the current state of the game.<br>You are now able to spawn humans when you have 150 of each resource. Might leave it here for a while.|
|[36](https://github.com/ConnorY97/AOEf6670e9c10ec85521da5e64f375525346054196f) | Fixing UI issue|
|[37](https://github.com/ConnorY97/AOEc1f76d09ed303d71b13b3d434bd4db9784c03c02) | Updating actions as suggested|
|[38](https://github.com/ConnorY97/AOE4edc498967920a27928f54b68d4cc2e34b4b309a) | Chat improvements and camera movement on PC|
|[39](https://github.com/ConnorY97/AOE5c86f3d68ca6b3904abcfd9d94c028d4aa748cbf) | Trying to implement some Unit testing|
|[40](https://github.com/ConnorY97/AOE028e4354cf460665e5fbd6cbef2342a2dbcf09cd) | Beautifying the game|
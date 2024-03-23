---
Title: Age Of Empires
date: 2024-03-09 09:00:00
categories: [Portfolio, C#]
---
Working on creating a simple AOE clone!

Progress! There is some cool UI:

Currently only have wood being incremented but will work on getting the rest working soon.

I will also take some time to properly set up this page as it has been a bit of an after thought so far.

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
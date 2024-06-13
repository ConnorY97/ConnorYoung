---
Title: Relentless Attack
date: 2024-04-28 09:32:00
categories: [Portfolio, C#]
image:
    path: /assets/img/relentlessattack.png
    alt: RA
---
This is the new game inspiration [The Army - Idle Strategy Game](https://play.google.com/store/apps/details?id=com.firestudios.thearmy&hl=en&gl=US).

## Scriptable Objects
For this project rather than creating the spawning grid each time the game starts, I thought I would rather create a [Scriptable Object](https://github.com/ConnorY97/RelentlessAttack/blob/main/Assets/CellsReference.asset). This way I was able to draw the grid out side of play time which was helpful for scaling to fit the screen. This was mostly done without tutorials which I am really proud of.

## Unit Testing
Following this tutorial [Unit Tests in Unity](https://www.youtube.com/watch?v=PDYB32qAsLU&t=611s) I set up *very basic* unit testing. Currently just checking if the `init()` function of my `EnemyBase` class is behaving as expected. But is has gotten me thinking more about what I should and shouldn't be testing.

With the help of Chat, I have further expanded the Unit tests to include the following:
```c#
public class GameManagerTesting
{
    [UnityTest]
    public IEnumerator ASoldierSetup_Test()
    {
        GameObject mGameObject = new GameObject();
        GameManager mGameManager = new GameManager();

        SceneManager.LoadScene("Soldier");

        yield return new WaitForSeconds(2);

        Assert.IsTrue(mGameManager.SetUpGameScene(), "Failed to set up the scene correctly");
    }
}
```
```c#
public class EnemyBaseTesting
{
    [Test]
    [TestCase(10, true, 10)]
    [TestCase(28, true, 100)]
    [TestCase(1, false, 1)]
    public void AInit_Test(int setHealth, bool isEnemy, int setSpeed)
    {
        GameObject mGameObject = new GameObject();
        EnemyBase mEnemy = mGameObject.AddComponent<EnemyBase>();
        Assert.IsNotNull(mEnemy, "Failed to create soldier");

        mEnemy.Init(setHealth, isEnemy, setSpeed);
        Assert.AreEqual(setHealth, mEnemy.HitPoints, "Failed to set health");
        Assert.AreEqual(isEnemy, mEnemy.IsEnemy, "Failed to set enemy");
        Assert.AreEqual(setSpeed, mEnemy.Speed, "Failed to set speed");
    }

    [Test]
    [TestCase(10)]
    [TestCase(-50)]
    public void BAttacked_Test(int attackAmount)
    {
        GameObject mGameObject = new GameObject();
        EnemyBase mEnemy = mGameObject.AddComponent<EnemyBase>();
        mEnemy.Init(100, true, 5.0f);

        mEnemy.Attacked(attackAmount);

        if (attackAmount > 0)
        {
            Assert.AreEqual(100 - attackAmount, mEnemy.HitPoints, "Failed to reduce hitpoint by accacking amount");
        }
        else
        {
            Assert.AreEqual(100, mEnemy.HitPoints, "Failed to filter incorrect attack amounts");
        }
    }
}
```
This [Medium Article](https://medium.com/codex/writing-unit-tests-for-my-game-in-unity-b0163e2c9b47) was a fantastic resource I found to add the `[TestCase(X,X)]` which just allows you to pass in variables to the testing functions. Even more than one!
So far this has successfully found 2 issues with code changes I have made. This was really cool! The tests only pass on as much information as you give them, so the more detail the better! <br>
![Successfullunittests](/assets/img/unittests.png){: width="486" height="294" }

[itch](https://connory97.itch.io/relentlessattack)

[Git](https://github.com/ConnorY97/RelentlessAttack)

|Commits|Message|
|-------|-------|
|[1](https://github.com/ConnorY97/RelentlessAttack/commit/9e423a0ca435e6ce0a44001926a0db956de7ec4d) | Initial commit|
|[2](https://github.com/ConnorY97/RelentlessAttack/commit/542f93b4c0c6b4d086ba812f961ebefe3be02257) | Adding the game|
|[3](https://github.com/ConnorY97/RelentlessAttack/commit/8650b3aec9e7e101d7f8cc2c2b9b2edb515d6285) | Continue working on enemy class<br>Implemented simple movement and fixed sprites not colliding.<br>To do:<br>Stop jittering when the enemies bunch up<br>Implement attacking|
|[4](https://github.com/ConnorY97/RelentlessAttack/commit/5f733e208aff45834013c6740493864f0f0b8fc3) | Code clean up|
|[5](https://github.com/ConnorY97/RelentlessAttack/commit/ec1b10bcf587903d4640d55332058fb0b991347c) | Adding Boundaries<br>Boundaries and continue work on enemy movement.|
|[6](https://github.com/ConnorY97/RelentlessAttack/commit/9e22d0fc23cfb9f430132f00f4f859ba243f5a3a) | Cont. work on enemies|
|[7](https://github.com/ConnorY97/RelentlessAttack/commit/e1f17f9bb36bbc9133874dae33d2d98edc863246) | Trying a character controller for movement|
|[8](https://github.com/ConnorY97/RelentlessAttack/commit/01eb315d28ef093e980ff61518cee62ffaf30718) | IT WAS CHARACTER CONTROLLER|
|[9](https://github.com/ConnorY97/RelentlessAttack/commit/215201c10b3610d883ca0d892b10bfcdb03d06ca) | Player spawn and improved code|
|[10](https://github.com/ConnorY97/RelentlessAttack/commit/41a0e8ba9269f2055a29c886af2de55fc203e95f) | Adding player movement|
|[11](https://github.com/ConnorY97/RelentlessAttack/commit/81037c9a4ef3cbcffb02a483a827b929912e5845) | ATTACKING<br>Implemented a very simple attack! But needs lots of work!|
|[12](https://github.com/ConnorY97/RelentlessAttack/commit/1eaa42894a87059d643663e2166344b8b09d3ef7) | Fixed attacking|
|[13](https://github.com/ConnorY97/RelentlessAttack/commit/466a32dc73ce4d0580f22bff7da0e99a91bb47fa) | Building and fixed editor scripts|
|[14](https://github.com/ConnorY97/RelentlessAttack/commit/09d3a87e5c0f0f3a670a7442093fad5daa1bc9dc) | Create main.yml|
|[15](https://github.com/ConnorY97/RelentlessAttack/commit/e9e2bee2ae0e0dc328d2212816ac9f457a29231f) | Testing updated actions|
|[16](https://github.com/ConnorY97/RelentlessAttack/commit/7430c3e15096250fbaac350f8acc49675685c7df) | Fix Ui and implement score|
|[17](https://github.com/ConnorY97/RelentlessAttack/commit/7adc0c052ce5e7c7988c9ccfd82bbb4402e01800) | Added a very simple game loop|
|[18](https://github.com/ConnorY97/RelentlessAttack/commit/9c44ad1396b07c4ca8ae427dbc505ef64d8f1c0b) | Testing Android build method|
|[19](https://github.com/ConnorY97/RelentlessAttack/commit/6e4afba3e387664e1d4992c589795b21f36d969a) | Merge branch 'build'|
|[20](https://github.com/ConnorY97/RelentlessAttack/commit/80fd1849bf222383f0fd7f830e1fd1d4a7771b64) | Closing untiy|
|[21](https://github.com/ConnorY97/RelentlessAttack/commit/fd295e436bdc3088f32c7841b775c56e86cc83ad) | Removing Android as it broke|
|[22](https://github.com/ConnorY97/RelentlessAttack/commit/e4d641ff0e2c1ed04e0a7a42d92d41f258022d26) | Local Android build|
|[23](https://github.com/ConnorY97/RelentlessAttack/commit/49938c163be8eaa7214aa582bd6b40ffa264dd56) | Update main.yml|
|[24](https://github.com/ConnorY97/RelentlessAttack/commit/62f26dfacbcebaa6df2ed09f6e21974007c71307) | Merge branch 'main' of https://github.com/ConnorY97/RelentlessAttack|
|[25](https://github.com/ConnorY97/RelentlessAttack/commit/0ddd6452a27e6eb9dbc3bbf6ee6dde3d2e3ed0f5) | Merge branch 'main' into build|
|[26](https://github.com/ConnorY97/RelentlessAttack/commit/474f389d69c8c01ae5f874d8fcc100c40659e3c6) | Cleaning up the workflow|
|[27](https://github.com/ConnorY97/RelentlessAttack/commit/c0c8e2bf8f47e0bbc4e8af9712ff89c5052dc656) | Setting up Unit Testing<br>Created a simple test for enemy set up.<br>Making sure all the member variables are being set correctly. Currently only testing the attack func.<br>I need to look into how I can make sure editor variables are being set as well. Very cool!|
|[28](https://github.com/ConnorY97/RelentlessAttack/commit/8f6d78f25f77becb0f20fe7d06e6981296f22414) | Adding test runner action|
|[29](https://github.com/ConnorY97/RelentlessAttack/commit/fe0ef0cf8e59aac9e179555f8fef28772361cc97) | Merge branch 'main' into build|
|[30](https://github.com/ConnorY97/RelentlessAttack/commit/d195a9b6c5260440b6bfd3a566ca83700de9cef6) | Testing as a project not as a package, duh|
|[31](https://github.com/ConnorY97/RelentlessAttack/commit/8f59c60248fa7cad5cde028cae76ee15b3b9c740) | Purposely failing unity test|
|[32](https://github.com/ConnorY97/RelentlessAttack/commit/48d61edd736564b55d815ddd632c06a87e87371c) | Merge branch 'main' into build|
|[33](https://github.com/ConnorY97/RelentlessAttack/commit/6b173ecf5144110a8e01520cb8c3f603e2f3cb0b) | Trying to improve logs|
|[34](https://github.com/ConnorY97/RelentlessAttack/commit/8bf90a3d4ab275f84e0ad43e13e0020ac1fdb210) | Fixing test break|
|[35](https://github.com/ConnorY97/RelentlessAttack/commit/b70aa41ed57da307dfdb194221379dd6af5c00da) | Lots of work!<br>1. Fixed the Game over UI<br>2. Improved attack: there is now a delay between each attach so it doesn't seem so funky<br>3. Added some more tests|
|[36](https://github.com/ConnorY97/RelentlessAttack/commit/3aec7bf38dd4d1f33ed3d83906d1849b0d422381) | Merge branch 'main' into build|
|[37](https://github.com/ConnorY97/RelentlessAttack/commit/ab21a8582ba7bce2db41ddc0e6cb074e22cfa7b8) | Fixing hanging test|
|[38](https://github.com/ConnorY97/RelentlessAttack/commit/3c9d0505ad2db71db623bb20f530adad3a86625e) | Merge branch 'main' into build|
|[39](https://github.com/ConnorY97/RelentlessAttack/commit/7cb7a7896db236f6ae33128249bf59d435f6aec8) | Trying to fix itch upload and android build|
|[40](https://github.com/ConnorY97/RelentlessAttack/commit/5f06e8517a72f169ec79b68b19f9f312c9abc96e) | Trying to solve windows build|
|[41](https://github.com/ConnorY97/RelentlessAttack/commit/5731a0c12561c012512573a6a84219c9a7c7fe06) | Maybe missing the matrix?|
|[42](https://github.com/ConnorY97/RelentlessAttack/commit/08e0ec3b62f12393828f6ad88361228041a48ed5) | Improving Testing and code clean up|
|[43](https://github.com/ConnorY97/RelentlessAttack/commit/e922dd59eef67338fe11901936252cb8f5639179) | Changed sprites to circles<br>So the sprites should have been circles the whole time. Lol|
|[44](https://github.com/ConnorY97/RelentlessAttack/commit/5f7a418788120ac3ee59ed59579205eb92c138c2) | Merge branch 'build'|
|[45](https://github.com/ConnorY97/RelentlessAttack/commit/2474beb1a876c5191097b59cbf806bff99b7d8f6) | Merge branch 'main' into build|
|[46](https://github.com/ConnorY97/RelentlessAttack/commit/0683c41edffc09ac0c1bdaa9c699df0c79611766) | Alex and Chat suggested code improvement|
|[47](https://github.com/ConnorY97/RelentlessAttack/commit/dd30df73028dc3cee6a83f8653d7c2b40eeab88f) | Merge branch 'build'|
|[48](https://github.com/ConnorY97/RelentlessAttack/commit/e93b0a144d843128b35b9430d6e5997ccc2cc598) | Fixing issue found but tests|
|[49](https://github.com/ConnorY97/RelentlessAttack/commit/9d10c96f0160e9b61baa106e3ea868206b40fb2b) | Lots of work!<br>1. Cleaned up the `EnemyBase` class more. Trying to encapsulate everything all of it inheritors may need.<br>2. Added the `Sniper` class. This is just a ranged enemy but it will be difficult to work this into the game play.<br>3. Improved on the unit testing but have not set any up for the sniper yet|
|[50](https://github.com/ConnorY97/RelentlessAttack/commit/ab8021b9225a3ebfaf87f8e7ac16a35abbb78302) | Creating a Main menu and levels<br>Removed some magic numbers and continued to work on different enemies|
|[51](https://github.com/ConnorY97/RelentlessAttack/commit/52114c05bfde1751b7559648911298d096a50f84) | Main menu main issues<br>Need to figure out how to assign all the required variables when the required scene loads. Lots of work to do.|
|[52](https://github.com/ConnorY97/RelentlessAttack/commit/ca63d03d2c0b5b094a81abaec6cedb36fb2883d9) | Fixed scene loading and added test<br>UI will still be broken on some resolutions though|
|[53](https://github.com/ConnorY97/RelentlessAttack/commit/0adae7fd87682bdfd37e387375cbce71022d2957) | Closing Unity|
|[54](https://github.com/ConnorY97/RelentlessAttack/commit/6bdfadb04c76e9a79f5344b14b743da48da43192) | Updated readme and did some work|
|[55](https://github.com/ConnorY97/RelentlessAttack/commit/e587bf084fe481b2c91a4a2dc768a1ae1f244323) | Bullet improvements and colours<br>Added Alex's suggested changes to the bullet and changed the background colour for the main camera to get rid of the terrible blue.|
|[56](https://github.com/ConnorY97/RelentlessAttack/commit/ce3c21e68ae2472a651ec4f08b3f4e82507d957a) | Fixing UI and Scaling issues... Hopefully|
|[57](https://github.com/ConnorY97/RelentlessAttack/commit/41b1909cdb3546ad560a152dd76c9b9477bc8752) | Build action set resolution|
|[58](https://github.com/ConnorY97/RelentlessAttack/commit/580209855093149b5a750c2344bf443bc5f1571d) | Trying a different template|
|[59](https://github.com/ConnorY97/RelentlessAttack/commit/720600b647357acce9b45c4438c99c76b5b17796) | Trying to copy more settings|
|[60](https://github.com/ConnorY97/RelentlessAttack/commit/b65417953059addd1f4cc2eafdc9292b197c48d7) | Removing hard code resolution|
|[61](https://github.com/ConnorY97/RelentlessAttack/commit/504a6c29c61cb9a27679e103b7f9d944836e29c2) | Downgrading Unity version|
|[62](https://github.com/ConnorY97/RelentlessAttack/commit/e8ed24806b5d5f16c4dd83fcb25d9c06b5774717) | Removing test runs for the time being|
|[63](https://github.com/ConnorY97/RelentlessAttack/commit/f48483eab7dc519c8e5127adaa831941ef5619e0) | Stop publishing to itch and just run tests|
|[64](https://github.com/ConnorY97/RelentlessAttack/commit/617211f653a0afb91e6e38266636c0ad8cafc694) | Adding bullet tests and improving movment|
|[65](https://github.com/ConnorY97/RelentlessAttack/commit/b4bb6c1dab2022d7796631a50839e7c906ef7a22) | You can now spawn snipers|
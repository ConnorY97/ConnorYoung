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
So far this has successfully found 2 issues with code changes I have made. This was really cool! The tests only pass on as much information as you give them, so the more detail the better!
![Successfullunittests](/assets/img/unittests.png){: width="486" height="294" }

[itch](https://connory97.itch.io/relentlessattack)

[Git](https://github.com/ConnorY97/RelentlessAttack)
---
Title: Relentless Attack
date: 2024-04-28 09:32:00
categories: [Portfolio, C#]
image:
    path: /assets/img/relentlessattack.png
    alt: RA
---
This is the new game inspiration [The Army - Idle Strategy Game](https://play.google.com/store/apps/details?id=com.firestudios.thearmy&hl=en&gl=US).

### This Project
# Scriptable Objects
For this project rather than creating the spawning grid each time the game starts, I thought I would rather create a [Scriptable Object](https://github.com/ConnorY97/RelentlessAttack/blob/main/Assets/CellsReference.asset). This way I was able to draw the grid out side of play time which was helpful for scaling to fit the screen. This was mostly done without tutorials which I am really proud of.

# Unit Testing
Following this tutorial [Unit Tests in Unity](https://www.youtube.com/watch?v=PDYB32qAsLU&t=611s) I set up *very basic* unit testing. Currently just checking if the `init()` function of my `EnemyBase` class is behaving as expected. But is has gotten me thinking more about what I should and shouldn't be testing.

[itch](https://connory97.itch.io/relentlessattack)

[Git](https://github.com/ConnorY97/RelentlessAttack)
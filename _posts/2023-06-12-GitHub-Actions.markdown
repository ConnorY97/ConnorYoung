---
Title: GitHub Actions
date: 2023-06-12 7:15:19
categories: [Learning, Devops]
image:
    path: /assets/img/actions.png
    alt: Actions
---
GitHub Actions is a robust CI tool that allows you to define processes for various tasks. I've primarily used it for Unity builds, but I'm currently experimenting with uploading build projects to ItchIO. My goal is to create a build branch for my Unity projects, making it easy to update and share my games for testing without requiring downloads.

Next, I plan to explore implementing some form of code review for my commits. I'm unsure if this will involve AI, but it's an exciting prospect to try out!

For the build part of the Git action, I've found [Game CI](https://game.ci/) to be my preferred option. While the build aspect is straightforward, it can get a bit muddy when it comes to the rest of the set up process.

For the first time I've used `actions/download-artifact@v3`, which allows me to retrieve artifacts created but `game-ci/unity-builder@v4` and upload them using `actions/upload-artifact`. Before this, I hadn't considered the file structure of the Ubuntu virtual machines used in these actions.
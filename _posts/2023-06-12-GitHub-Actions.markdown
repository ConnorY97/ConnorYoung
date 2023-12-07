---
Title: GitHub Actions
date: 2023-06-12 7:15:19
categories: [Learning, Devops]
image:
    path: /assets/img/actions.png
    alt: Actions
---
GitHub provides a powerful CI tool in the form of actions. This are process you can define to do a range of things!

I have only used them for Unity builds so far, but I am currently testing uploading a build project to ItchIO. The hope is I can have a build branch for my Unity projects that I will easily be able to update and have my games accessible for anyone to test for me without them having to download anything!

The next thing I hope to look into is some sort of code review for commits I make. I am not sure whether this is going to involve some sort of AI but it will be exciting to test!

[Game CI](https://game.ci/) has so far been my go to for the build portion of the Git action.

The build aspect is very clear, however testing the builds is a bit more vague. I have not successfully implemented the [activation step](https://github.com/marketplace/actions/unity-activate). As my license is now working consistently, I do not think I will have to implement this step.

This was also the first time I have used the `actions/download-artifact@v3`, which can download artifacts created and uploaded with the `game-ci/unity-builder@v4` and `actions/upload-artifact` actions. I have never really thought about the file structure of the `ubuntu` virtual machines used in these actions. But obviously whenever you spin up a new one it will not have any of the files or artifacts created by its predecessors. I an now able to retrieve what I have spent so long building and do something with it! 
---
Title: Learning Docker
date: 2024-03-23 09:00:00
categories: [Learning, Devops]
---
Docker? Images? Containers? What does all of this mean?!?!

Well I had no idea, but now I kind of have an idea: I followed this tutorial for setting up the basic Linux Docker Image: [UE Tutorial](https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-for-using-container-images-in-unreal-engine)

### Docker
This is the application that allows you to quickly create `virtual machines` with a kind of foundation which allows you to quickly start working rather than having to spend time setting it up your self.

### Image
This is the foundation of the `VM` you are going to be working in. So in my case I am using the Epic Unreal Engine Linux 5.3 image: [GitHub Image Repo](https://github.com/orgs/epicgames/packages/container/package/unreal-engine). I do want to build to Windows, but for the time being building to Linux is fine.

### Container
This is the running `VM` with the structure defined by the image. Since this is most of the time a very basic `VM` you will have to transverse the machine via the command line which is a nightmare.

The next step is to get GitHub and my Docker image talking to each other so that I can trigger a build from the `VM` on a push to the build branch. Then the next issue is trying to upload the build and upload it as an artifact to the GitHub repo.

Fun times.
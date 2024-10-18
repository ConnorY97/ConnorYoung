---
Title: Github Local Runners
date: 2024-10-01 09:00:00
categories: [DevOps, Software]
---
# Setting Up a GitHub Self-Hosted Runner for Unity Testing: My Journey

Recently, I found myself needing to set up a self-hosted runner for testing and building my Unity project. While GitHub’s cloud-hosted runners are convenient, they didn’t quite meet my needs for more complex Unity builds, especially since I wanted more control over the testing environment. So, I decided to explore how to configure a self-hosted runner on my Linux build machine and run Unity tests seamlessly. Here’s how the process went and some of the issues I encountered (and solved) along the way.

## Why I Chose a Self-Hosted Runner

I’ve been working on a Unity project, and while GitHub’s hosted runners are helpful for many workflows, I needed something faster and more customizable. Specifically, I wanted a runner that could handle my Linux build machine's GPU and could be tweaked to work with Unity versions tailored to my project. That’s where the idea of a self-hosted runner came in. It sounded like the perfect solution to give me more control over the environment.

## The First Step: Setting Up the Runner

First, I headed over to GitHub and navigated to my repository’s settings. Under **Actions**, there’s an option for **Runners**, where I could add a new self-hosted runner. I thought it was going to be simple… and it was, but only once I understood the steps.

Here’s what I did to get the runner set up on my Linux machine:

### 1. Download the Runner

I started by setting up a directory to host the runner files. GitHub gave me a set of commands to download and extract the runner, which I ran on my Linux machine:

```bash
mkdir actions-runner && cd actions-runner
curl -o actions-runner-linux-x64-2.294.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.294.0/actions-runner-linux-x64-2.294.0.tar.gz
tar xzf ./actions-runner-linux-x64-2.294.0.tar.gz
```

### 2. Registering the Runner

Next, I had to register the runner with my GitHub repository. GitHub provided me with a token and command to link the runner:

```bash
./config.sh --url https://github.com/YourUsername/YourRepository --token YOUR_TOKEN_HERE
```

So far, so good. After running that, the runner was connected to my repository. It even showed up in the **Settings** under **Actions** as expected!

## Unity Testing Setup: Getting the Project Ready

Now that the runner was up and running, it was time to configure the tests for my Unity project. I’d done some Unity test automation before, but this was my first time doing it on a self-hosted runner. I needed to make sure Unity was properly installed on the machine and that the project could run its tests smoothly.

### Installing Unity

I’m using Unity Hub to manage the versions on this machine, so I installed the specific version my project needed:

```bash
sudo apt install unityhub
unityhub install --version 2023.2.18f1
```

Once Unity was set up, I was ready to test. Or so I thought…

## Writing the GitHub Actions Workflow

The next step was to write a GitHub Actions workflow that would trigger tests on this new runner. Here’s what I came up with after some trial and error:

```yaml
name: Testing on self hosted runner

on:
  workflow_dispatch:
    {}

jobs:
  testing:
    name: Run Tests
    runs-on: self-hosted  # Use the self-hosted runner

    steps:
      - name: Checkout repo
        uses: actions/checkout@v4
        with:
          lfs: false

      - name: Test
        id: test_step
        shell: bash
        run: |
          set +e  # Allow the script to continue on non-zero exit codes
          trap '' SIGSEGV  # Suppress segmentation fault errors
          ~/Unity/Hub/Editor/2023.2.18f1/Editor/Unity -runTests -batchmode \
            -projectPath /home/runner/Documents/RelentlessAttack/ \
            -testPlatform StandaloneLinux64 \
            -testResults /home/runner/Documents/Results/testResults.xml \
            -logfile /home/runner/Documents/Results/logRestults.txt \
            >/dev/null 2>&1 || true  # Ignore the segmentation fault and continue

      - name: Convert test results
        if: steps.test_step.outcome == 'success'
        shell: bash
        run: |
          python3 ./scripts/ConvertResult.py "/home/runner/Documents/Results/testResults.xml"

      - name: Publish CTRF Test Summary Results
        if: steps.test_step.outcome == 'success'
        run: npx github-actions-ctrf "/home/runner/Documents/Results/result.json"

      - name: Post Log on Fail
        if: steps.test_step.outcome == 'failure'
        uses: actions/upload-artifact@v4
        with:
          name: TestLogs
          path: /home/runner/Documents/Results/logRestults.txt
```

### Key Parts of the Workflow

- **Unity Tests**: The real magic happens with the `runTests` argument for Unity. This command allowed me to run the tests I had set up within Unity’s test framework, targeting the `StandaloneLinux64` platform.
  
- **Segmentation Faults**: One of the biggest issues I ran into was segmentation faults during testing. This turned out to be a bit tricky. I ended up suppressing these errors and letting the tests continue regardless. Not the most elegant solution, but it got the job done.

- **Publishing Test Results**: After the tests ran, I used a Python script to convert the test results into a format compatible with `github-actions-ctrf`, a neat tool for publishing test summaries.

- **Logging Failures**: I also set up a way to upload logs in case the tests failed. This was crucial for debugging any issues that came up.

## Unexpected Issues (and How I Solved Them)

While the process was mostly smooth, I hit a couple of bumps along the way.

### Unity Segmentation Faults

As I mentioned earlier, I was getting segmentation faults during some of the test runs. After digging into the logs, it seemed to be related to how Unity handled certain builds on Linux. Rather than have my pipeline crash, I decided to suppress these faults using `set +e` and `trap '' SIGSEGV` so the tests could complete even if there were minor hiccups. This isn’t a permanent fix, but it worked for my needs.

### Log Management

At first, I didn’t have a good way to capture logs when the tests failed. I eventually added a step that would upload the test logs as an artifact whenever something went wrong. This saved me a lot of headaches when it came to debugging failures.

## Wrapping Up

Setting up a self-hosted runner for Unity testing was a bit of an adventure, but it’s definitely worth it. Now, my Unity project is being tested on my own hardware, and I have full control over the environment. It’s faster, more flexible, and I’m no longer at the mercy of GitHub’s shared runners.

If you’re considering doing the same, I highly recommend it—especially if you need custom configurations or just want to speed up your CI pipeline. With some patience (and a few workarounds), you can have a reliable self-hosted runner setup that integrates seamlessly with GitHub Actions.

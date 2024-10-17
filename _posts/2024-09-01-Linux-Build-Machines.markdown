---
Title: Linux Build Machines
date: 2024-09-01 09:00:00
categories: [DevOps, Hardware]
image:
    path: /assets/img/buildmachine.png
    alt: Build Machines
---
### Fixing an HP Compaq 8100 Elite: From OS Installation to Self-Hosted GitHub Runner

Recently, I had the opportunity to repurpose an old HP Compaq 8100 Elite at work for a new purpose: setting it up as a self-hosted GitHub Actions runner. The process was both challenging and rewarding. In this blog post, I'll walk you through the steps I took—from OS installation to configuring it for remote access and setting it up for GitHub Actions.

#### Step 1: Initial Hurdle - No OS Installation on an External SSD

The HP Compaq 8100 Elite is an older machine, and my initial plan was to install the OS onto an external SSD as the original hard drive was destroyed. However, I quickly ran into a brick wall. After plugging in the external SSD and starting the OS installation process, I realized that the BIOS did not support booting from USB-connected external drives. Some modern PCs support this, but this machine didn't play along.

After some research and tinkering, I concluded that installing the OS directly on the internal hard drive was the best (and only) route to go. So, I went to Centre Com, asked for the cheapest and smallest drive they had and happily left with a $32 SSD.

#### Step 2: Installing Ubuntu 22.04

Next, I grabbed the latest LTS version of Ubuntu, 22.04. Installation was smooth once I decided to use the internal drive. Ubuntu recognized all the necessary hardware components, and in no time, I had the system up and running.

The HP Compaq 8100 Elite might be old, but with Ubuntu 22.04, it was quite snappy, which was a pleasant surprise.

#### Step 3: Setting Up xRDP for Remote Access

Since the machine would be stashed away in a corner, I wanted to access it remotely rather than connect a monitor, keyboard, and mouse every time. My tool of choice for remote access is **xRDP**, which allows me to use the standard Windows Remote Desktop Protocol (RDP) to connect to the Ubuntu system.

I followed this tutorial to get it set up: https://www.digitalocean.com/community/tutorials/how-to-enable-remote-desktop-protocol-using-xrdp-on-ubuntu-22-04.

With this setup, I was able to remote into the machine from my Windows laptop using the built-in Remote Desktop Connection tool. I could easily run administrative tasks and configure the system without being physically near it.

#### Step 4: Setting It Up as a GitHub Actions Self-Hosted Runner

The next step was to turn the HP Compaq 8100 Elite into a self-hosted GitHub Actions runner for our CI/CD pipelines. Here’s how I configured it:

1. **Create a new GitHub Actions runner:**
   - In your GitHub repository, navigate to **Settings** → **Actions** → **Runners** → **New self-hosted runner**.
   - Follow the instructions to download the runner package.

2. **Install and configure the runner:**
   ```bash
   # Download the runner package (as instructed by GitHub)
   mkdir actions-runner && cd actions-runner
   curl -o actions-runner-linux-x64-2.292.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.292.0/actions-runner-linux-x64-2.292.0.tar.gz
   tar xzf ./actions-runner-linux-x64-2.292.0.tar.gz

   # Configure the runner with the provided token and URL
   ./config.sh --url https://github.com/<your-org>/<your-repo> --token <your-token>

   # Install necessary dependencies
   sudo apt install libicu-dev libssl-dev
   ```

3. **Set the runner as a system service:**
   This ensures that the runner starts automatically even after a reboot.
   ```bash
   sudo ./svc.sh install
   sudo ./svc.sh start
   ```

4. **Tagging the Runner**: I gave the runner a custom tag (e.g., `compaq8100-runner`) to differentiate it from cloud-hosted runners. This way, I could easily assign specific jobs to this runner using the `runs-on` key in GitHub Actions workflows:
   ```yaml
   jobs:
     build:
       runs-on: self-hosted
       tags: compaq8100-runner
   ```

#### Step 5: Running Simple Tests

Once everything was set up, I ran a few test workflows to ensure that the runner was working as expected. Here's a simple GitHub Actions workflow I used to test it:

```yaml
name: Test Runner

on: [push]

jobs:
  test:
    runs-on: self-hosted
    steps:
      - name: Check out code
        uses: actions/checkout@v2

      - name: Run a script
        run: echo "Self-hosted runner is working!"
```

The runner picked up the job, executed it, and reported back success. Mission accomplished!

#### Conclusion

Turning the HP Compaq 8100 Elite into a self-hosted GitHub Actions runner was a fun and satisfying project. From battling the external SSD installation issue to setting up remote access and running test workflows, it was a great way to breathe new life into this old machine. Now, it's happily chugging along, running CI jobs for our team's projects.

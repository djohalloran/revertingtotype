---
title: "Digitizing Mini DV Tapes"
subtitle: Struggling to convert old camcorder tapes 
draft: false
summary: How to convert Mini DV Tapes to MPEG4 Files
author: "Dermot"
date: 2020-06-03T21:01:00+01:00
tags: ["mini DV", "samsung", "camcorder", "tapes"]
toc: true
# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 3
  caption: ''
  focal_point: "Center"
  preview_only: false

# View.
#   1 = List
#   2 = Compact
#   3 = Card
view: 2

# Optional header image (relative to `static/img/` folder).
header:
  caption: ""
  image: "/img/antora-01.jpg"

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---


OVERVIEW
--------

Not as straight forward as you'd think.

Not just a matter of connecting a camera to the laptop via USB. 

Many of these cameras are limited to just firewire connectors.

Last computer with a firewire connector was:

Video showing multiple connectors!

Luckily lenovo T420 and T430s have express card slots.

Ordered a dodgy lookinig express card with 2 Firewire ports.

Accompanying CD promised to include the necessary driver but this would not install and the video capture software requried a serial number that was not included.

Windows 10 recgnized the card in device manager

HDVSplit and MiniDV apps failed to recognize the camera.

Eventually I tried Premiere Pro and it worked.

Export options, bitrate: 4 quality, size files MP4



i'm in the process of digitizing a lot of old svhs and vhs tapes.

the tapes are run through a minidv camera with a firewire connection to a pc that captures the video in premiere pro 5.0.

the resulting files are quite large. 45 minutes of video takes up 10GB space.

i want to compress those files as much as possible, without loosing quality, and still be able to edit the files.

how should i do it?

DV runs at 25MbPS which is, as /u/greenysmac pointed out, 13GB/hour. That's not all that large, when you consider that modern HD video cameras run at 50-100MbPS, and ProRes and DNxHD (modern editing formats) are up to 220MbPS (closer to 70-80 GB per hour). Space is cheap. 

https://www.reddit.com/r/VideoEditing/comments/2ay2ki/minidv_compression/


MINIDV

1) The data on the tapes will be in standard-definition DV format which is 720x480 in NTSC countries and 720x576 in PAL/SECAM. It's likely to be interlaced, although some camcorders were capable of recording progressive video. The audio will normally be 16-bit 48kHz stereo PCM (although other sample rates are permissible). When you read them in, you will most likely end up with either a raw DV file or an AVI file containing DV data, at 25Mbps for the video stream. The transfer will be a lossless process, although the DV format is itself lossy - it's a bit like a more advanced version of Motion JPEG (in other words, the file should contain exactly what is on the tape with no further quality loss).

2) In theory, it should make no difference to quality what device is used to read the tapes (as long as they are still in good condition) - they are pure digital media so the data returned should be identical to what was originally recorded (just like burning a CD/DVD on one PC then reading it on another). The only problem that could conceivably occur would be if the original recording device had gone "out of alignment" in some way (head azimuth, etc.) or the recordings have "faded" or become damaged in some other way over time in which case different playback devices may cope better or worse with them - this would vary from being unable to read them at all to returning occasional corrupt frames.
https://forums.tomsguide.com/threads/preserving-quality-of-mini-dv-sd-cassettes-for-long-term-storage-camcorder-vs-dedicated-player.422150/




[Antora](https://antora.org/) is an open source documentation site generator. It allows you to host your product documentation in a version control system like GitHub, GitLab or Bitbucket and build a pretty documentation site using an easily configurable "playbook" that controls the presentation and content versioning.

Installing Antora on a desktop machine requires a number of pre-requistive tools and libraries like Node Version Manager (NVM) and Node itself. In my experience, trying to get Antora installed on both Windows and Linux ended up being a bit of a pain.

An easier way is to run Antora in a [Docker container](https://www.docker.com/products/docker-desktop) so you don't have to worry about installing the various tools required and wrestle with OS and hardware incompatibilities. All you need to do is install Docker and tell it to run the official Antora container designed especially for Docker.

You can think of a Docker container image as a box with everything you need to run an application: the code, the runtime, the settings, and even the operating system itself. Docker containers isolate software from your machine's environment so you can get up and running more quickly. So rather than installing and running Antora on your own computer, you install Docker and run Antora on its container image.

In this example we're going to go a step further and instead of running Docker on a local machine, we're going to run it within a [DigitalOcean](https://www.digitalocean.com/products/droplets/) virtual environment hosted in the cloud.

STEP-BY-STEP
------------

1. Create a new Droplet in your DigitalOcean account. 

{{< figure caption="" src="antora-docker-droplet-02.png" >}}

In my case I opted for a one consisting of Docker 19.03.12 running on Ubuntu 20.04 with a regular shared CPU running 1GB RAM and basic block storage. I also just used password authentication.

{{< figure caption="" src="antora-docker-droplet-01.png" >}}

2. Connect to the Droplet using a Terminal tool. In my case I usedd PuTTy for Windows:

{{< figure caption="" src="antora-docker-droplet-03.png" >}}

3. Update Ubuntu in the Droplet:
```
sudo apt -y upgrade
```

4. Create a directory for the Antora project:
```
mkdir antora
```

5. Navigate to the new antora directory and clone the Antora demo site. This will create a docs-site directory containing the Antora demo site and playbook file:
```
git clone https://gitlab.com/antora/demo/docs-site.git 

root@docker-ubuntu-s-1vcpu-1gb-lon1-01:~/antora/docs-site# ls -la
total 52
drwxr-xr-x 4 root root  4096 Jun  3 10:21 .
drwxr-xr-x 3 root root  4096 Jun  2 19:25 ..
drwxr-xr-x 8 root root  4096 Jun  2 19:39 .git
-rw-r--r-- 1 root root    35 Jun  2 19:25 .gitignore
-rw-r--r-- 1 root root   291 Jun  2 19:25 .gitlab-ci.yml
-rw-r--r-- 1 root root 16725 Jun  2 19:25 LICENSE
-rw-r--r-- 1 root root  1901 Jun  2 19:25 README.adoc
-rw-r--r-- 1 root root   775 Jun  3 10:21 antora-playbook.yml
drwxr-xr-x 3 root root  4096 Jun  2 19:49 build
```
The *antora-playbook.yml* file contains all the details relating to the documentation site such as the various Markdown pages and the UI bundle that controls the HTML rendering of the site.

6. The official Antora Docker image for running Antora inside a container is published in the *antora/antora* project on Docker Hub. To use this, run the following docker run command to invoke the Antora Docker image with the playbook file:
```
docker run -u $(id -u) -v $PWD:/antora:Z --rm -t antora/antora antora-playbook.yml
```

This command creates a new container using the Antora Docker image, mounts the current directory as the path */antora* inside the container, runs the *antora* command on the Antora playbook, then stops and removes the container. It’s just like running a locally installed Antora command. 

Because we're running this in Linux we need to add the *:Z* or *:z* modifier to the volume mount, and the -*u $(id -u)* option to instruct Docker to run the entrypoint command as the current user. Otherwise, files will be written as root and become hard to delete. The *-t* flag allocates a pseudo-TTY required to display see the progress bars for Git operations.

The generated documentation site files will appear in the *build/site* directory. 

To view the site properly in a web browser you'll need to install a web server to host the site. You'll also need to open up the Droplet's firewall so you can actually access it. We'll do this in the following steps.

7. The simplest web server is the one that comes installed with Python 3 and the easiest way to install Python 3 in a droplet is to installed *X-Tools* which you can do using the following commandL:
```
apt install golang-golang-x-tools
```

8. By default, all ports except 22 (SSH), 2375 (Docker) and 2376 (Docker) are blocked by a Droplet's UFW firewall. So to allow HTTP requests to pass in and out, we need to open up a port like 8088 for example. Do this using the following command:
```
ufw allow 8088
```

9. Now launch the Python HTTP Server within the *build/site* directory using the following command:
```
python3 -m http.server 8088
```

10. Navigate to the droplet's IP address on port *8088* to see the Antora test site:

{{< figure caption="" src="antora-docker-droplet-04.png" >}}

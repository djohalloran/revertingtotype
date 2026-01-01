---
title: "Mount NAS in Ubuntu VM running in Synology NAS"
subtitle: ...
draft: false
summary: ...
author: "Dermot"
date: 2020-06-03T21:01:00+01:00
tags: ["synology", "nas", "cif", "mount"]
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

ACCESSING LOGITECH ON VM ON NAS
===============================

1. Log into NAS
2. Open VM Manager
3. Click on Connect
4. Log into Ubuntu
5. Open browser and navigate to localhost:9000



OVERVIEW
--------

5c0ElTTUW0s1!



https://www.youtube.com/watch?v=j625yzl78nA

https://www.youtube.com/watch?v=P7eq7nnpURs

Logitech Multimedia Server

Step 1.

Set up CIFS in Synology and share music folder.

Step 2. Test mount command to see that everyhting is working and the directory is populated.

sudo mount -t cifs -o username=dohalloran,	password=Dynam0Dynam1,uid=1000 //192.168.1.1/music /mnt/Multimedia

sudo mount -t cifs -o username=dohalloran,password=Dynam0Dynam1,uid=$(id -u),gid=$(id -g),forceuid,forcegid, //192.168.1.1/music /mnt/Multimedia

Step 3. Edit fstab file so it will autmoatically mount the music directory each time Ubuntu starts.

sudo su
touch /root/.smbServer
vim .smbServer
	username=
	password=
chmod 700 /root/.smbServer

sudo vim /etc/fstab

//192.168.1.1/music /mnt/Multimedia cifs credentials=/root/.smbServer.uid=1000 0 0

sudo mount -a

sudo reboot

Rebooting the NAS, what happens to Mediaserver?


Maybe it should be:

//192.168.1.1/music /mnt/Multimedia cifs ro, auto,credentials=/root/.smbServer 0 0



 

Step 2. Test mount command to see that everyhting is working and the directory is populated.

sudo mount -t cifs -o username=dohalloran,	password=Dynam0Dynam1,uid=dohalloran,gid=users //192.168.1.1/music /mnt/Multimedia

sudo mount -t cifs -o username=dohalloran,password=Dynam0Dynam1,uid=$(id -u),gid=$(id -g),forceuid,forcegid, //192.168.1.1/music /mnt/Multimedia



Docker approach?
------
https://www.youtube.com/watch?v=xzMhZoUs7uw



<iframe src="https://www.youtube.com/embed/yUTDFpiPFzQ" title="YouTube video player" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" width="656" height="369" frameborder="0"></iframe>





Squeezebox Touch Artwork Issue
------------------------------

If the artwork is displaying for songs on the local server but not displaying the artwork for internet radio or Spotify music then try:

- Changing the Advanced > Performance > Artwork Resizing setting from "Use mysqueezebox.com to resize artwork" to "Use Logitech Media Server to resize artwork"

If that doesn't work then try:

- Enable the Song Info plugin
- Changing the following Advanced > Performance settings for the Logitech Server:
	Artwork pre-caching























ANTORA

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

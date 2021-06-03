---
title: "Running Antora through Docker in a DigitalOcean Droplet"
subtitle: Experiment in building an Antora documentation site using Docker
draft: false
summary: Experiment in building an Antora documentation site using Docker
author: "Dermot"
date: 2020-06-03T21:01:00+01:00
tags: ["antora", "documentation", "DigitalOcean", "docker"]
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

[Antora](https://antora.org/) is an open source documentation site generator. It allows you to host your documentation in a version control system like GitHub, GitLab or Bitbucket and from it build a pretty documentation site using an easily configurable "playbook" that allows you to control the presentation and content versioning.

Installing Antora on a desktop machine requires a number of pre-requistive tools and libraries like NVM and Node. In my experience trying to get Antora installed in either Windows or Linux ended up being a bit of a pain.

An easier way is to run Antora in a Docker container so you don't have to worry about installing the various tools required and wrestle with various OS incompatibilities. All you need to do is install Docker and tell it to run the relevant Antora container.

Docker is a tool for running container images. You can think of a container image as a box with everything you need to run an application: the code, the runtime, the settings, and even the operating system itself. Containers isolate software from your host environment so you can get up and running more quickly. Rather than installing and running Antora on your own computer, you install Docker and run the Antora command through its container image.

In this example we're going to go a step further. Instead of running Docker on my local machine, I'm going to create and use a DigitalOcean environment in the cloud.

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
The antora-playbook.yml file contains all the details relating to the documentation site such as the various Markdown pages and the UI bundle that controls the HTML rendering of the site.

6. The official Antora Docker image for running Antora inside a container is published in the antora/antora project on Docker Hub. To use this, run the following docker run command to invoke the Antora Docker image with the playbook file:
```
docker run -u $(id -u) -v $PWD:/antora:Z --rm -t antora/antora antora-playbook.yml
```

This command creates a new container using the Antora Docker image, mounts the current directory as the path /antora inside the container, runs the antora command on the Antora playbook, then stops and removes the container. It’s just like running a locally installed Antora command.

The generated documentation site files will now appear in the build/site directory. 

To view the site properly in a web browser you'll need to install a web server to host the site. You'll also need to open up the Droplet's firewall so you can actually access it. We'll do this in the following steps.

7. Install X-Tools which will include Python 3:
```
apt install golang-golang-x-tools
```

8. By default all ports except 22 (SSH), 2375 (Docker) and 2376 (Docker) are blocked by the Droplet's UFW firewall. To allow HTTP request we're going to open up port 88. Do this using the following command:
```
ufw allow 8088
```

9. Now launch the Python HTTP Server within the build/site directory:
```
python3 -m http.server 8088
```

10. Navigate to the droplet's IP address on port 8088 to see the Antora test site:

{{< figure caption="" src="antora-docker-droplet-04.png" >}}

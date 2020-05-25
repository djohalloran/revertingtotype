---
title: "Rural Broadband Woes"
subtitle: Grappling with Mobile Broadband
summary: 
author: "Dermot"
date: 2015-02-25T11:23:25Z
draft: false
tags: ["broadband", "router"]

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
  image: "/img/ftth-01.jpg"

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Until recently, Eircom's fixed-line ADSL service was just about adequate for my broadband needs. But at over 4km from the exchange the average speeds of around 1.5Mbps download and 0.4Mbps upload have become primitive in comparison to what's available from the newer fibre and mobile broadband services starting to roll out across the country. Things took a turn for the worse a few weeks ago when, despite repeated calls to Eircom support, the best stable speeds I could get dropped to about 0.54Mbps. I even took a screenshot. Something to show the grandchildren in years to come:

{{< figure caption="Eircom ADSL Speeds" src="/img/rural-broadband-woes-01.jpg" >}}

The main contender as an alternative to Eircom fixed line is Vodafone Mobile Broadband. We've been lucky to have a really good Vodafone 3G signal in the area where I live (the village of Dualla) the past few years. Fortune shone again about 6 months ago when a 4G signal became available - despite it still being unattainable in more built-up areas close to us, like Thurles, for example.

Other providers such as 3 and O2 offer plans with more data but their signal is non-existent in our area. And while there are other wireless alternatives available in the area, such as Premier Broadband for instance, their packages are currently not much ahead of Eircom in terms of bandwidth (around 2MB up/down) and there's also no guarantee their service will work due to line-of-sight issues.

So I decided to experiment with two possible solutions: Vodafone and Meteor. Both plans have cooling off periods meaning I could try them both for 7 days (14 days in the case of Vodafone) with the option of a "no quibble" return and refund if they proved unsuitable.

### Vodafone

Vodafone have easily the best quality signal and the Huawei R215 device that came with the package detected a 4G connection almost anywhere in the house.

{{< figure caption="Huawei R215" src="/img/rural-broadband-woes-02.jpg" >}}

The best location however was the attic where I could get speeds of around 18Mbps and ping times of 30 - 45ms.

{{< figure caption="Vodafone 4G Speeds" src="/img/rural-broadband-woes-03.jpg" >}}

So what's the problem? The main impediment so far with moving to a 3G or 4G service has been the lack of a plan with unlimited data. Because I do a lot of work from home I could easily go through 40-60GB of data a month. But the best Vodafone can offer at the moment is a plan with a data usage limit of 20GB. This is paltry; especially in terms of 4G bandwidth. Another annoying factor is that Vodafone require a minimum 12 month contract at about €30 per month -- I don't want to be tied into something for this long.

The real deal breaker however is that I want to hook the modem into a TP-LINK MR3220 3G/4G router I have so I can distribute the signal around the house. Try as I might I could not get it to detect the R215 device no matter what settings I used.

So, while a great performer in terms of speed, the Vodafone solution had just too many niggly issues to make it a runner.

### Meteor

The Meteor router came in the form of a Huawei E5377. The package is branded as XXL and costs 24 euro per month including VAT and the data usage limit is 30GB.

{{< figure caption="Huawei E5377" src="/img/rural-broadband-woes-04.jpg" >}}

When I initially turned it in I could only get a 2G signal. I had feared this as my understanding was that Meteor shared the O2 network which has a very poor reception around here. To my surprise, however, when I took the router into the attic I was able to get a strong 3G signal. Here's a sample speedtest:

{{< figure caption="Meteor 3G Speeds" src="/img/rural-broadband-woes-05.jpg" >}}

So while Meteor's 3G speeds were around half the speed and double the ping times of the Vodafone router's 4G signal, it was still more than adequate for my requirements. And at 6 euro cheaper per month and only a 6 month contract it was starting to look like a runner. The best was yet to come. The TP-LINK 4G router detected it within moments of plugging the E5377 into its USB port.

The only concern was that even at 30GB a month, it may not be enough before incurring excess charges. So I tried it for a few days and found that I was averaging around 1GB a day. This included a few Webex sessions with work and almost constant VPN connectivity to the office. So with some care it would certainly be possible to keep things within the 30GB limit if I avoided streaming video and the like. And if I did need more data Meteor offer an add-on of 20GB for 20 euro which would bring my limit up to 50GB; all for €44 a month.

So I returned the Vodafone router and opted for the Meteor package.

### The Setup

As mentioned already, the wifi signal on a small mobile broadband router like the Huawei E5377 or R215 is never going to be strong enough to broadcast around the entire house. You can get around this by using a dedicated 4G router that will greatly extend your wifi capacity and provide ethernet ports for additional devices such as file servers, printers etc.

I already had a TP-LINK MR3220 3G/4G router I picked up some time ago and until now was lying unused.

{{< figure caption="TP-LINK MR3220 3G/4G" src="/img/rural-broadband-woes-06.jpg" >}}


This router has a USB port on its side that will take the connection from the Huawei E5377 and automatically relay its internet connection.

Because these devices must reside in the attic in order to catch the best reception, I also need a way of bringing the signal downstairs to another router under my stairs where my file server resides and where I broadcast another wifi signal. To do this I got a set of TP-LINK 300Mbps AV200 Powerline Extenders.

{{< figure caption="TP-LINK 300Mbps AV200 Powerline Extenders" src="/img/rural-broadband-woes-07.jpg" >}}

One plugs into an attic socket. It takes an ethernet cable from the MR3220 and sends the data down to the second plug downstairs. This second home plug broadcasts the data it gets from the attic over its own wifi. It also has two ethernet ports, one of which connects to a NAS server.

Below is a schematic of how it all hangs together. A bit convoluted, no doubt, but it works well. I'm hoping there's a way I use WPS to perhaps cut out the TP-LINK router from the chain but I've had no joy so far trying to get the powerline adapter play nice with the Huawei E5377.

{{< figure caption="The Full Setup" src="/img/rural-broadband-woes-08.jpg" >}}

### Update #1

The setup has been in place a few months now and is generally working well and the 3G/4G speeds are a much needed improvement over the miniscule 1MB speeds were were living with. There's been no huge downsides apart from the odd day or two where the 3G signal in the area went AWOL. I'm also finding it virtually impossible to stay within the data 30GB limit. It's a lot closer to 50MB and sometimes even more. I've therefore had to purchase a monthly 20GB add-on giving me 50GB a month by default. Some months I've had to buy an extra 15GB on top of all that just to get me over the line. This brings the cost up to roughly €60.

One interesting thing to note was that the MR3220 had some trouble dealing with the Huawei E5377 switching between 3G and 4G signals depending on the network quality on a particular day. This caused the MR3220 to lose its connection entirely with the E5377 entirely and required a restart. This problem was resolved by configuring the E5377 to only use the 3G network so no switching occurred thereby stopping the MR3220 from getting confused.

In addition, the 4G signal in the area seems to have strengthened and I'm now getting on average 25Mb download speeds. Happy days.

{{< figure src="/img/rural-broadband-woes-09.jpg" >}}

### Update #2

[Andrew L](https://twitter.com/langerslangford) got in touch to say that an external antenna he purchased for use with his E5377 made a huge difference to the signal reception. Prior to using the antenna he was barely getting a 3G signal indoors and could only get 4G when the dongle was held out an upstairs window. His speeds went from approximately 1Mb to almost 40Mb.

{{< figure src="/img/rural-broadband-woes-10.jpg" >}}

Also worth noting is that Andrew uses a [Netgear N900 (WNCE4004) 4-Port Wi-Fi adapter](http://www.netgear.ie/home/products/connected-entertainment/gaming-home-theater/wnce4004.aspx) to connect to his Meteor broadband router wirelessly instead of via USB. I think this is a better solution than the TP-LINK MR3220 as it bypasses any compatibility issues you might get connecting a mobile broadband dongle to a router via a USB cable.
---
title: "Cannot Communicate With Battery"
subtitle: Fixing an issue with a Canon 7D
summary: 
author: "Dermot"
date: 2018-02-11T20:20:55Z
tags: ["camera", "battery"]
# View.
#   1 = List
#   2 = Compact
#   3 = Card
view: 3

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
  image: "ftth-01.jpg"

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

My secondhand Canon 7D suddenly developed a "Cannot Communicate with Battery" warning recently. I didn't think much of it at the time as the camera still worked perfectly. The only minor annoyance was that the battery power indicator no longer appeared on the top LCD window or in the battery details screen in the main options panel. However, the problem became far greater when a week later I grabbed my camera to head to a local event only to realise that the previously fully charged battery was now empty despite next to no usage.

{{< figure src="https://live.staticflickr.com/4723/28431036859_f0957e0d96_w_d.jpg" link="https://live.staticflickr.com/4723/28431036859_6e06066277_k_d.jpg" >}}

{{< figure src="https://live.staticflickr.com/4616/39313059985_3ac70f907a_w_d.jpg" link="https://live.staticflickr.com/4616/39313059985_bd3822ac9f_k_d.jpg" >}}

After some quick searching online I found that this problem is quite common with the Canon 7D: it's due to a motherboard screw becoming lose and eventually coming to rest somewhere that causes a short that not only blocks the camera from communicating with the battery but also causes the battery to discharge even when the camera is powered off.

{{< figure src="https://live.staticflickr.com/4607/28431037129_08ab36a600_w_d.jpg" link="https://live.staticflickr.com/4607/28431037129_863b9b40df_k_d.jpg" >}}

{{< figure src="https://live.staticflickr.com/4671/39313059335_53471225b5_w_d.jpg" link="https://live.staticflickr.com/4671/39313059335_bf8d9a34fd_k_d.jpg" >}}

Both the videos I watched online showed the offending screw as being located on the underside circuit board next to the camera chamber. However, when I opened up my camera the same screw was intact. Taking off the entire back panel of the camera so I could get a better look at the main motherboard showed no missing screws either. Neither was there any rattle or sound of any loose screws when I shook the camera.

Dejected, I began to doubt the "loose screw" theory. But further reading only offered alternative options that involved putting the camera in a freezer for "6 or 7" minutes as some people maintained the problem was due to temperature related expansion and contraction of battery connector components. This didn't seem to be a very scientific approach so I decided I wasn't going to go down that route, at least just yet.

About the give up and resort to flying blind with my battery indicator plus the added awkwardness of having to take the battery out each time I finished with the camera to stop it discharging; I decided to have one last look around the inside of the camera. Thankfully, I spotted a screw that had lodged itself next to the motor's magnet. Where this screw came from, I have no idea - all the obvious screw holes were intact. This must have come from somewhere out of sight, perhaps from behind the main motherboard. I plucked the offending screw out and did a quick battery test: everything was back to normal. The camera was once again communicating with the battery.

I decided to leave the screw out entirely instead of dismantling the camera any further to locate its rightful place. Perhaps this is a risky tactic and could make an inner component prone to movement or vibration. I'll just monitor the camera for the next few weeks and months and see how it performs. If additional problems start to crop up at least I'll know the likely issue. For now, I've got a fully working camera again so all is right with the world.

Here are the videos I found useful:

{{< youtube DQaejgJM1Rc >}}


Another video of how to dismantle the camera:

{{< youtube z7uUmaAAe7w >}}


I also found this link useful:

https://photo.stackexchange.com/questions/16152/how-can-i-fix-a-cannot-communicate-with-battery-error-on-canon-7d	
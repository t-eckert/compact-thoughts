---
title: Wading into Homelab
published: 10 April 2024
tags:
  - Homelab
  - Kubernetes
  - Talos Linux
  - Debian
  - Postgres
---

import { Image } from "astro:assets"
import Homelab from "@/images/notes/wading-into-homelab.jpeg"
import HomelabAnnotated from "@/images/notes/wading-into-homelab-annotated.jpg"
import HomelabCompute from "@/images/notes/wading-into-homelab-compute.jpg"

I want to be a homelabber. I'm inspired by people running their own compute at home and I want to join them. I've toyed with the idea for several years, picking up aspirational Raspberry Pis. Now, I'm really digging in and feeling both overwhelmed with ideas and stymied at what to do next.

<Image
  src={Homelab}
  alt="An overhead shot of my homelab of Raspberry Pis."
  class="object-cover rounded-md mx-auto w-full mb-4"
/>

<div class="grid grid-cols-1 sm:grid-cols-2 sm:gap-4">
  <div>
    My homelab is four Raspberry Pis of varying vintages, a 5 port Gigabit switch, my Google Wifi, and an ancient 1 TB external hard drive. It exists to be a playground for learning and sharing what I'm learning. Rather than a lab, I call this my _Homecluster_, in part because it's based around [Talos Linux](https://www.talos.dev/) and Kubernetes.

    All of the Pis are wired into the switch which is connected to a node of my Google Wifi mesh router. The external hard drive just sits there for now. I have thought about plugging it in to one of the Pis, but I'm not really sure what I'd want to do with it yet. I have a feeling it's too slow and small to be useful as part of a NAS.

    Right now, the lab is more of a platform for me to start building on. I'm not 100% sure what I want to do with it. I have some avenues I want to explore like running an [ADS-B Receiver](https://flightaware.store/) (though I may not be able to when I move to Canada) and hosting my own weather app.

  </div>
  <Image
    src={HomelabAnnotated}
    alt="An overhead shot of my homelab of Raspberry Pis."
    class="object-cover rounded-md mx-auto w-full mb-4"
  />
</div>

<div class="grid grid-cols-1 sm:grid-cols-2 sm:gap-4">
  <Image
    src={HomelabCompute}
    alt="An overhead shot of my homelab of Raspberry Pis."
    class="object-cover rounded-md mx-auto mb-4"
  />
  <div>
    The heart of Homecluster is the Kubernetes cluster running across two Pi 4s. One acts as a control plane, the other is a worker node. As I explore this hobby more, I have set up the cluster so that I can easily add more compute to this cluster with more worker nodes.

    I've deployed Kubernetes to the Pis using Talos Linux. Talos is a Linux distribution that only runs Kubernetes on bare metal. There is some amount of learning curve associated with the install, but overall the experience has been enjoyable. The documentation is well done, especially for such a small team taking on a big project. Talos makes setting up Kubernetes on bare metal way easier than it has ever been in the past.

    Outside of the Kubernetes cluster, the two older Pis both run Debian. I call these my "agents".

    The Pi 3 is a dedicated 120 GB Postgres database. I gave it the moniker `quadratic-crab`. Having a Postgres database on my network is fantastic. It means as I develop my own apps for the cluster, I can reliably have database available. I'd like to build some form of backup for this that saves snapshots to cloud storage or a NAS eventually.

    The Pi 2B is the most computationally restrictive machine I'm running. I call this agent `advocate-cardinal`. It runs Debian and I shell into it on occasion. It's powerful enough to run some sensors and report data back to the rest of the cluster. I can see it playing a role in a weather station or the ADS-B receiver. It will definitely be some kind of satellite node.

  </div>
</div>

As for applications, there is a lot of room to grow. In the Kubernetes cluster, I am running four things:

- A Minecraft server
- [Memos](https://github.com/usememos/memos), a kind of open-source Twitter
- [Pihole](https://pi-hole.net/)
- A Debian installation so I have a 64-bit Linux OS available to shell into

Everything on the Homecluster can be found in [this repository](https://github.com/t-eckert/homecluster/tree/main). Just as I've been inspired by others, I want people to take from what I build for themselves. I'm excited to see what I'll end up building and sharing with everyone.

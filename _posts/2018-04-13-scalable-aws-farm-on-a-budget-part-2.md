---
title: Scalable AWS On A Budget - Part 2
layout: post
date: '2018-04-13 09:59:37'
categories: aws linux memory optimization swapfile ubuntu
---

**Free RAM on your AWS t2.nano. Sounds too good to be true? Doctors hate this one secret!**

The t2.nano and t2.micro instances are perfectly suited to what we need, which is unexpected burst of CPU power. 

However, most of the things I want to do are going to need a bit more breathing room in RAM than 0.5gb / 1gb... Which is where the first, and arguably most important, change to all base images comes in.

We can triple our available RAM and guard a little against system OOM process-killing by configuring a cross-reboot persistant swapfile for each image.

**Install RAM pls**

The exact copy/pasteable commands I used to install a swapfile which will persist across reboots are as follows:

```
sudo mkdir -v /var/cache/swap
cd /var/cache/swap
sudo dd if=/dev/zero of=swapfile bs=1K count=1M # this creates 1gb of swap for t2.nano instances, use 2M here for 2gb of swap on t2.micro
sudo chmod 600 swapfile
sudo mkswap swapfile
sudo swapon swapfile
echo "/var/cache/swap/swapfile none swap sw 0 0" | sudo tee -a /etc/fstab
```

I chose 1gb / 2gb based on [redhat's reccomendations (scroll to **Table 8.3. Recommended System Swap Space**)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/installation_guide/sect-disk-partitioning-setup-x86#sect-recommended-partitioning-scheme-x86) and I haven't had any major headaches thus far.

Next post (when I get around to it) I'll dive into some microservice-specific individual optimizations, suited to run smoothly on our resource-starved base image above.

[<< Previous Post](/aws/scaling/cost/optimizations/ec2/microservices/2018/04/13/scalable-aws-farm-on-a-budget-part-1.html)
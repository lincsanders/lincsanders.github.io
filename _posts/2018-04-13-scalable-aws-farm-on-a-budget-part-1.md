---
title: Scalable AWS On A Budget - Part 1
layout: post
date: '2018-04-13 09:59:37'
categories: aws scaling cost optimizations ec2 microservices
---

**Autoscaling, microservices and running everything on a CPU/RAM diet**

I recently rewrote the entire server architecture for an auto-scaling microservice farm which handles 15,000-25,000 requests a day (and needs to handle well over 200,000 on a busy day).

The microservices consist of a PHP web app, PHP background worker, standalone Java server application, a Ruby on Rails app and Redis server.

I am forever in search of how to get the most bang for my buck on AWS. With any of the above microservices needing to support any given amount of load at any point in time, the most important part of the farm is that daily costs are manageable even under heavy load.

**The baseline**

Lets start with some parameters I arbitrarily imposed upon myself with which we'll create our farm around. Keep in mind this is only for application servers which are ephemeral by nature; servers hosting persistent storage .

- Instances can't be more powerful than t2.nano or t2.micro
- A single 8gb gp2 HDD per instance
- All microservices should auto-scale based on load.

I didn't see the need to re-invent the wheel when it came to auto-scaling and uptime monitoring, so I went with an established service. I'd strongly advise the same e.g. [Scalr](https://www.scalr.com/){:target='blank'} or [AWS OpsWorks](https://docs.aws.amazon.com/opsworks/latest/userguide/welcome.html){:target='blank'}

Each microservice has specific needs and tweaks to it's own base image, but there's also a lot of shared optimizations I made to get the most out of minimal CPU power and 0.5gb of RAM. 

[Lets see exactly what some of those optimizations are in the next post >>](/aws/linux/memory/optimization/swapfile/ubuntu/2018/04/13/scalable-aws-farm-on-a-budget-part-2.html)
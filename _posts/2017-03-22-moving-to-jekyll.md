---
layout: post
title: "Migrating to Jekyll"
date: 2017-03-27 12:28
author: "Thomas Smart"
comments: false
categories: [Web]
tags: [Jekyll, Web, Lets-Encrypt, AWS, nginx]
---

A lightweight blog such as this should be many things, small, fast, secure and simple. Unfortunately wordpress was missing the beat with most of these. Even on wordpress' hosting the site was still slow to load, and bloated. Too easy was it to install plugins after plugins that did meaningless tasks and provided no real benefit to the visitor. Plain and simple, plugins are insecure. Regardless of their source they will be exploited and provide a mechanism for unwanted access. This was reason enough to move on to better days and newer tech.

## Project Plan
They key to a smooth migration is planning, given this was personal, and the blog was empty, I did minimal planning. Even with this minimal planning the migration was smooth, with only minor hiccups. I knew that the end result was as follows:
* Amazon AWS tiny instance
* TLS Encryption using Lets Encrypt certificates
* Github management for posts 
* nginx web server
* Jekyll content manager

## Amazon AWS Instance
I evaulated a couple of different options before arriving at an AWS EC2 Instance.

| **Provider**    | **Pro**                          |  **Con**                 |
| --- | --- | --- |
| Azure VM         | - Robust <br> - Already using for other services  | - Only 1 month trial <br> - VM's more expensive |
| GitHub Pages     | - Free <br> - Mature offering                     | - No native ssl            |
| EC2 AWS Instance | - 12 month trial (Free Tier) <br> - Full VM       | - Additional mgmt overhead |

So lets begin, this is part recall of what happened, part guide.

1. Login or create an account for [AWS](http://aws.amazon.com)
2. Open up the management portal and head over to the EC2 instances
3. Under `Create Instance` click the `Launch Instance` ![Create Instance Button]({{ site.url }}/assets/jekyll-migration/create-instance.png)
4. Select the `Amazon Linux AMI` ![Choose AMI]({{ site.url }}/assets/jekyll-migration/choose-ami.png)
5. Select `t2.micro` instance ![Choose AMI]({{ site.url }}/assets/jekyll-migration/choose-instance-size.png)
6. 

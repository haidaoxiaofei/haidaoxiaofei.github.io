---
layout: post
category: "linux"
title:  "Linux Network Commands"
tags: [linux, network]
---

####1.List The Open Ports And The Process That Owns Them

So how do you list the network open ports on your Linux server and the process that owns them? The answer is simple. Use the following command (must be run as the root user):


	sudo lsof -i
	sudo netstat -lptu
	sudo netstat -tulpn
	

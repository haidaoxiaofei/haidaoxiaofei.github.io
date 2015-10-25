---
layout: post
category: "program"
title:  "Export figures in Powerpoint as an EPS figure to use in latex"
tags: [latex]
---

Sometime, I need to draw figures in Powerpoint then use them in my latex projects. However, Microsoft does not provide a function as "Export as eps" in Powerpoint. Here, I record how I attempted to make this happen.

1. JPG to EPS
---
Use some screenshot software to capture the figures as JPG files, then convert them to eps with some online services. 

Here is the one I like most:http://image.online-convert.com/convert-to-eps

2. PDF to EPS
---
The first option is easy, however the quality of the final eps file is low.

The other choice may be exporting the figure as PDF file first, then convert it to EPS file. As PDF is vector file, the quality lost is very small. 

To export the figure as PDF file is easy. You may either export the whole file as PDF or print some particular page as PDF.

To convert PDF to EPS is a little more complex. Use either pdftops or the online services (in option 1) is ok.
However, pdftops sometimes fail to finish the converting process accurately, like fulfil the whole page with some color.

The most promising procedure is:

*Use online services to convert PDF to EPS first, then use ps2epsi to crop the outputted EPS file*

ps2epsi automatically calculates the bounding box required for all encapsulated PostScript files, so most of the time it does a pretty good job.

`ps2epsi <input.eps> <output.eps>`
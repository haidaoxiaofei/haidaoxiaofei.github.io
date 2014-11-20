---
layout: post
category: "gis"
title:  "how to use an image as map in TileMill"
tags: [Map Generator]
---

TileMill is an open source tools to generate a personal map, which can then be used in OpenStreetMap or MapBox.

Here is a tutorial about how to use GDAL to warp an image into GIS system required formation. [link](http://www.macwright.org/2012/08/13/images-as-maps.html)

Before run the python script, you need to install GDAL. To install GDAL on Ubuntu is quite easy, just type in below command:
`sudo apt-get install gdal-bin`

After a GeoTIFF file is generated, insert it as a layer in TileMill. Then insert below code to the script part.

``
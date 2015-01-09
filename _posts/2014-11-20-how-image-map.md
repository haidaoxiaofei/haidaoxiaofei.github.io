---
layout: post
category: "gis"
title:  "How to Use an Image as Map in TileMill"
tags: [Map Generator]
---

[TileMill](https://www.mapbox.com/tilemill/) is an open source tools to generate a personal map, which can then be used in OpenStreetMap or MapBox.

Here is a [tutorial](http://www.macwright.org/2012/08/13/images-as-maps.html) about how to use GDAL to warp an image into GIS system required formation. 

Before run [the python script](http://haidaoxiaofei.me/d/togeo.py), you need to install GDAL. To install GDAL on Ubuntu is quite easy, just type in below command:

	sudo apt-get install gdal-bin

After a GeoTIFF file is generated, insert it as a layer in TileMill (SRS choose 900913, leave Class blank). Assume the id of your layer is "image" Then insert below code to the mss script.
	
	#image {
		raster-opacity:1;
		raster-scaling:lanczos;
	}

Then, if nothing wrong, you can see your image on a particular latlng position of the map. 

If you like, you can upload it to MapBox server or export it as mbtiles file.

Good luck~

	

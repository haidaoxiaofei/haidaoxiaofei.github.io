---
layout: post
category: "linux"
title:  "Basic Linux Commands for Text Processing"
tags: [text processing]
---

Linux command line tools are really useful for text processing. This article will conclude some basic commands for that purpose.

####1. wc : count lines and words

	#count how many lines a file has.
	wc -l filename
	
	#count how many words a file has.
	wc -w filename
	
	#count how many bytes a file has.
	wc -c filename
	
####2. sort : sort the lines of a file
	#sort the lines of a file
	sort filename
	
####3. uniq : delete the duplicated line of a *sorted* file
	#In general, we use sort command before uniq. The result can be output to some file
	sort filename | uniq > outputFile
####4. expand : expand each tab to four spaces (unexpand can do reverse, but I did not success..)
	expand filename
####5. cut : the cut utility cuts out selected portions of each line (as specified by list) from each file and writes them to the standard output.
	#Extract users' login names and shells from the system passwd(5) file as ``name:shell'' pairs:
    cut -d : -f 1,7 /etc/passwd
    
    #Show the names and login times of the currently logged in users:
    who | cut -c 1-16,26-38

This command may be a little bit hard to use. Try awk instead. For example:

	wc -l filename | awk {'print $1'}


My Pocket has one Chinese [article](http://getpocket.com/a/read/158283999) that introduces some more commands.
---
layout: post
category: "program"
title:  "Convert .eps File to .pdf File Automatically with pdflatex on OS X"
tags: [latex, osx]
---

TexStudio is a amazing tool to edit latex. However one thing annoying me a lot is how to automatically convert .eps file to .pdf file. 

On ubuntu, I just include 'epstopdf' package and append '-shell-escape' to pdflatex command. Then everything goes well. Something looks like:

	/usr/texbin/pdflatex  -synctex=1 -interaction=nonstopmode -shell-escape %.tex

On OS X, this problem really makes me headache a while. After all, I solved it at last through one not delegate method. Here is the notes:

By checking the tex's log, I found that epstopdf was not located in system searched PATH, so I created the link manully

	ln -s /usr/local/texlive/2014/texmf-dist/scripts/epstopdf/epstopdf.pl /usr/local/bin/epstopdf
Also, the epstopdf complained that ghostscript is not installed. So I made it satisfied with

	brew install ghostscript
	
WHooo, texstudio generated pdf as I expected.

PSPS: requiring epstopdfpackage declared and -shell-escape appended.

On 10.10, there is a bug when opening texstudio from GUI. Environment Variants cannot be loaded rightly. Thus, open it from command line will work well.

	/Applications/texstudio.app/Contents/MacOS/texstudio
	
Maybe, adding this command to alias is a good choice in current. Hope apple can solve this [bug](https://code.google.com/p/mactlmgr/issues/detail?id=102) soon.

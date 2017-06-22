---
layout: post
title:  "Diable/Enable Printing to Screen"
date:   2017-06-22
categories: python
---

A way to disable printing to the screen and then restore it later. 

{% highlight ruby %}

import os, sys

STDOUT = sys.stdout

# Disable Print
def disablePrint():
    sys.stdout = open(os.devnull, 'w')

# Restore Print
def enablePrint():
    sys.stdout = STDOUT
    
{% endhighlight %}     
    



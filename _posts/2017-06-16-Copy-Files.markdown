---
layout: post
title:  "Copy files to a new directory"
date:   2017-06-16
categories: python
---
Using glob to locate files within a sub-directory and copy the files to a new directory.

{% highlight ruby %}
import os
import glob

burst       = 'bn080916009'
method      = 'BXA'
det         = 'L'
detdir      = ('GBMwLAT' if 'L' in det else 'GBM')

direc = '/Users/KimiZ/GRBs2/analysis/LAT/%s/%s/%s/'%(burst, method, detdir)
newdir = '/Users/KimiZ/Python/Github/%s/images/%s/'%(burst, method)
os.chdir(direc) 
curdir = os.getcwd()

AllFiles = glob.glob('*/*marg.pdf')

for File in AllFiles:
    f = os.path.join(direc, File)
    #print('cp %s %s'%(f, newdir))
    os.system('cp %s %s'%(f, newdir))

{% endhighlight %}

If I'm editing my directories or contents of directories with python, I always print out my steps first to make sure my code does what I intend.
You don't want to mass delete (or move) things that weren't ment to be deleted (or moved).



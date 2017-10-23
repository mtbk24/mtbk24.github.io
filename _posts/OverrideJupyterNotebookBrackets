---
layout: post
title:  "Override Jupyter Notebook's auto completion of brackets and quotation marks"
date:   2017-10-23
categories: python
---
If you want to get Jupyter Notebook to stop auto completing your quotation marks and brackets, paste the following snippet in your cutom.js file found in your .ipython folder.
{% highlight ruby %}
if (IPython.CodeCell) {
IPython.CodeCell.options_default.cm_config.autoCloseBrackets = false;
}
{% endhighlight %}

your folder can be found here:

/Users/HomeName/.ipython/profile_default/static/custom/custom.js

Where HomeName is your computers name. If you use more than one ipython, as I do, your .ipython folder may be in another place. For the Fermi Science Tools I use for research, the python I use is the Mac’s pre-installed version in /usr/bin/python.

My .ipython folder is in /opt/local because I had to download another ipython that would work with this python version.



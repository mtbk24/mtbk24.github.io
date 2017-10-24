---
layout: post
title:  "Fix for issues with JSON files containing more than one dictionary, but saved improperly."
date:   2017-10-23
categories: python
---

In my research, I've ran into an annoying issue several times because the author of a program I've used did not crate the JSON dictionary properly and it can not be loaded for use. 

For example, if we create two dictionaries:
{% highlight ruby %}
values = {“alpha”:-1.234, “beta”: -2.563, “tem”: 592.502, “norm”: 0.000192}
errors = {“alpha”:[“nan”, -1.21], “beta”: [“nan”,”nan”],  “tem”: [552.948, 601.193], “norm”: [0.000188, 0.000199]}
{% endhighlight %}
to store in the same JSON file, the proper way to save them is:
{% highlight ruby %}
json.dump((values, errors), open(‘test1.json’, ‘w’))
{% endhighlight %}
instead of in two separate steps, like this:
{% highlight ruby %}
json.dump(values, open(‘test1.json’, ‘a’))
json.dump(errors, open(‘test1.json’, ‘a’))
{% endhighlight %}
** I’d like to note that this doesn’t work either:
{% highlight ruby %}
json.dump(values, open(‘test1.json’, ‘a’), separators=’, ‘)
json.dump(errors, open(‘test1.json’, ‘a’), separators=’, ‘)
{% endhighlight %}
because it breaks down the dictionary format in the file giving:
{% highlight ruby %}
“alpha” -1.234,“beta” -2.563, instead of 

“alpha”: -1.234,“beta”: -2.563,
{% endhighlight %}
and it does not use the separator between the dictionaries as desired.

However, for some obvious reasons, appending to a JSON file may be unavoidable and we’ll need a fix for when it is used.

Within the file, the dictionaries will be separated by }{ instead of },{ so we will need to replace the }{ with an identifier to split the data on.
{% highlight ruby %}
with open(‘test1.json’) as data: 
    raw = data.read()
{% endhighlight %}

# replace the }{ with }*@*{ (or any identifier of your choice, as long as it doesn’t show up anywhere in your file) and then split the raw data on that identifier.
{% highlight ruby %}
adjusted_data = raw.replace(‘}{‘, ‘}*@*{‘) 
parts_of_data = adjusted_data.split(‘*@*’)

good_data = [json.loads(part) for part in parts_of_data]
{% endhighlight %}
good_data will now be read in as two separate dictionaries.

If the file was written properly, you’d only need to use:
{% highlight ruby %}
test1_data = json.load(open(‘test1.json’, ‘r’))
{% endhighlight %}

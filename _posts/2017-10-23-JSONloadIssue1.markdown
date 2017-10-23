---
layout: post
title:  "Fix for issues with JSON files containing more than one dictionary, but saved improperly."
date:   2017-10-23
categories: python
---

In my research, I've ran into an annoying issue several times because the author of a program I've used did not crate the JSON dictionary properly and it can not be loaded for use. 

For example, if we create two dictionaries:

values = {“alpha”:-1.234, “beta”: -2.563, “tem”: 592.502, “norm”: 0.000192}
errors = {“alpha”:[“nan”, -1.21], “beta”: [“nan”,”nan”],  “tem”: [552.948, 601.193], “norm”: [0.000188, 0.000199]}

to store in the same JSON file, the proper way to save them is:

json.dump((values, errors), open(‘test1.json’, ‘w’))

instead of in two separate steps, like this:

json.dump(values, open(‘test1.json’, ‘a’))
json.dump(errors, open(‘test1.json’, ‘a’))

** I’d like to note that this doesn’t work either:
json.dump(values, open(‘test1.json’, ‘a’), separators=’, ‘)
json.dump(errors, open(‘test1.json’, ‘a’), separators=’, ‘)

because it breaks down the dictionary format in the file giving:

“alpha” -1.234,“beta” -2.563, instead of 

“alpha”: -1.234,“beta”: -2.563,

and it does not use the separator between the dictionaries as desired.

However, for some obvious reasons, appending to a JSON file may be unavoidable and we’ll need a fix for when it is used.

Within the file, the dictionaries will be separated by }{ instead of },{ so we will need to replace the }{ with an identifier to split the data on.

with open(‘test1.json’) as data: 
    raw = data.read()

# replace the }{ with }*@*{ (or any identifier of your choice, as long as it doesn’t show up anywhere in your file) and then split the raw data on that identifier.

adjusted_data = raw.replace(‘}{‘, ‘}*@*{‘) 
parts_of_data = adjusted_data.split(‘*@*’)

good_data = [json.loads(part) for part in parts_of_data]

good_data will now be read in as two separate dictionaries.

If the file was written properly, you’d only need to use:

test1_data = json.load(open(‘test1.json’, ‘r’))

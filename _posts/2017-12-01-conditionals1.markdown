---
layout: post
title:  "Conditionals in Python"
date:   2017-12-01
categories: python
---
This code makes random data of choices 'A' or 'B'.
It then takes the choices and assigns a drink choice to them.
Choice A will be associated with 'water' and choice 'B' will be associated with 'milk'.


The typical way to write this:
{% highlight ruby %}
import numpy as np
import time

choices = ['A', 'B']
data    = np.random.choice(choices, size=10000000)

start = time.time()
result = []
for i in data:
    if 'A' in i:
        result.append('water')
    else:
        result.append('milk')
stop = time.time()
print(stop-start) # 5.26572608948
{% endhighlight %} 
This took 5.27 seconds. For a smaller data set of size=100, this took 0.000281810760498 seconds to run.

A shorter and better way to write the same function, that is also faster!
{% highlight ruby %}
import numpy as np
import time

choices = ['A', 'B']
data    = np.random.choice(choices, size=10000000)

start = time.time()
result2 = [('water' if 'A' in i else 'milk') for i in data]
stop = time.time()
print(stop-start) # 3.59431600571
{% endhighlight %} 
This took about 3.59 seconds.  For a smaller data set of size=100, this took 0.000203847885132 seconds to run.


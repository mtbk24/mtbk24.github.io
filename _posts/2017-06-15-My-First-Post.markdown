---
layout: post
title:  "My First Post"
date:   2017-06-15
categories: python
---
For my first post, I just want to test out posting a snippet of code.

{% highlight ruby %}

from __future__ import division
import numpy
import matplotlib.pyplot as plt

def polynomial(x, *coeff):
    '''
    polynomial(x, *coeff)
    
    x:      int or float. One x data point at a time.
    coeff:  list or array of polynomial coefficients.    
    '''
    order       = len(coeff) - 1
    answer      = []
    for i in range(order+1):
        answer.append( coeff[i] * (x**[i]) )
    return float(sum(answer))


x = numpy.linspace(0, 1, 100)
coefficients = [1., 0.5, -0.5]    
y = [polynomial(i, *coefficients) for i in x]
plt.plot(x,y)
plt.xlabel('x')
plt.ylabel('y')
plt.title('Polynomial')

{% endhighlight %}

<p>
<img src="/images/poly.png" style="width: 400px;"/>
 <em> </em>
</p>


This is a polynomial function that will return the `y` values, given an `x` value and a list with the polynomial coefficients `*coeff`.



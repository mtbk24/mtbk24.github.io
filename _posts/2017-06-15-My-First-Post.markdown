---
layout: post
title:  "My First Post"
date:   2017-06-15
categories: testing
---
For my first post, I just want to test out posting a snippet of code.

{% highlight ruby %}
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
{% endhighlight %}

This is a polynomial function that will return the `y` values, given an `x` value and a list with the polynomial coefficients `*coeff`.



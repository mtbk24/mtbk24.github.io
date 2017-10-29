---
layout: post
title:  "Properties in Python"
date:   2017-10-29
categories: python
---

I provide a better example of using properties on my GitHub page. I include the use of the property decorator.  Here is an example of what you’ll see on [my GitHub page here](https://github.com/mtbk24/PythonBasics/blob/master/Properties%20in%20Python.ipynb)

{% highlight ruby %}

class PropsOfX(object):
 
    def __init__(self, x=None): # default for x is None.
        self._x = x 
 
    @property
    def x(self):     # get_x
        return self._x 
 
    @x.setter
    def x(self, x):  # set_x
        self._x = x
 
    @x.deleter
    def x(self):
        del self._x
{% endhighlight %} 

*I highly recommend checking out the Github site, as it is more advanced and better written than this blog post.

{% highlight ruby %}

class GetandSet(object):
 
    def __init__(self):
        # default value x.
        self._x = 24  
 
    def get_x(self):
        return self._x
    getx = property(get_x)  
 
    def set_x(self, x):
        self._x = x
    setx = property(set_x) 

 
# test is an instance of the GetandSet class.
test = GetandSet()  
 
test.get_x()    # 24
test.getx       # 24
 
test.set_x(12)  # set x to 12
test.get_x()    # 12
test.getx       # 12

 {% endhighlight %}
 
The default value here for x is 24.  test.getx will return it immediately.  If you’d rather not have a default, you can either replace self._x = 24 with self._x=None, or replace self._x = 24 with self._x = x and change the init(self) to init(self, x=None)

{% highlight ruby %}

class GetandSet(object):
    # default for x is None.
    def __init__(self, x=None):
        self._x = x 
 
    def get_x(self):
        return self._x
    getx = property(get_x)  
 
    def set_x(self, x):
        self._x = x
    setx = property(set_x) 
 
test = GetandSet(22)  
 
test.get_x()    # 22
test.getx       # 22
test.set_x(33)
test.get_x()    # 33
test.getx       # 33
 
test2 = GetandSet()
test2.getx
# nothing returned because x is None.
# But no error!
 {% endhighlight %}
 
Because x=None in the init, you can choose to enter a number at initialization or not. If you leave it blank, the test.getx will return nothing instead of raising an error. But if you put in a number ( i.e. test = GetandSet(22) ), that value will become the default. test.getx will return that number.

{% highlight ruby %}
class A(object):
    def f(self):
        print "f in class A"
        return 15
    get = property(f)
 
class B(A):
    def f(self):
        print "f in class B"
        return 99
 
test = B()
test.get    # output:  f in class A, 15
test.f()    # output:  f in class B, 99

{% endhighlight %}
The get property here uses the f function in class A and returns the number 15.  test.f() however returns the f function from class B.


{% highlight ruby %}
class A(object):
    def f(self):
        print "f in class A"
        return 15
    def f_getter(self):
        return self.f()
    get = property(f_getter)
 
class B(A):
    def f(self):
        print "f in class B"
        return 99
 
test = B()
test.get # output:  f in class B, 99
test.f() # output:  f in class B, 99

 {% endhighlight %}
The get property here uses the f function in class B and returns the number 99.

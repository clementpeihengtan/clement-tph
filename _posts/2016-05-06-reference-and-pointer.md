---
layout: post
title:  "Reference and Pointer"
date:   2016-05-06
categories: mediator feature
tags: featured
image: /assets/article_images/2016-05-06-reference-and-pointer/night-view.jpg
---
When it comes to C or C++, the most confusing parts are pointer and reference. Although it looks complicated, if you mastered them, they really help a lot in programming as they are very powerful tools.  

# Reference

Reference variable is a variable that refers to another variable or object that is existed in your program.  

It is actually a duplicate of a variable in a memory location. Therefore, you can access the value of the variable either through the original value or the reference variable.

* Reference cannot be later made to reference other objects once it is created  

* References cannot be NULL

{% highlight ruby %}
int &r = NULL; //this is wrong, give you error
{% endhighlight %}

* Reference must be initialized when declared

{% highlight ruby %}
int x = 5;
int y =9;
int &r = x;
{% endhighlight %}

# Pointer

First of all, we know that variable is actually a memory location, and this location has its own address. A pointer is a variable which takes an address of another variable.

* Pointers can be used to re-assigned
* Pointers can be null to indicate it is not pointing to any valid thing.
* Pointers need not to be initialized when it is declared.

Re-assigned pointer

{% highlight ruby %}
int x = 6;
int y = 7;
int *k;  // a null pointer
k = &x;
k = &y;
*k = 10;

assert(x == 6);
assert(y == 7);
{% endhighlight %}

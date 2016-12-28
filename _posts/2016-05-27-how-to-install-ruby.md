---
layout: post
title: "How to install Ruby in Ubuntu"
date: 2016-05-27
image: /assets/article_images/2016-05-27-how-to-install-ruby-ubuntu/city.jpg
---
When I was creating my website using Jekyll, I encountered some problem about installing Ruby in my machine. It’s kind of frustrated when you are stucked in a particular procedure and unable to proceed the next step.

Today, I am going to share the way to install Ruby on Rails on Ubuntu using RVM.

# Step1-Install RVM

RVM stands for Ruby Version Manager. It helps to manage Ruby version independently and gives us an easy way to install Ruby. This command will help you to install latest version of RVM and also automatically download all required files and install on your system.

Install CURL
We need to install curl in order to install RVM.

{% highlight ruby %}
$ apt-get install curl
{% endhighlight %}

Install RVM
The first command import a public key into our system, the second command install RVM using curl.

{% highlight ruby %}
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys D39DC0E3
$ curl -sSL https://get.rvm.io | bash -s stable
{% endhighlight %}

Install Ruby Dependencies
This command install all the dependencies for installing Ruby automatically on our system

{% highlight ruby %}
$ rvm requirements
{% endhighlight %}

# Step2-Check the list of available Ruby Versions

Use the following command to check the list of ruby available.

{% highlight ruby %}
$ rvm list known
{% endhighlight %}

# Step3-Install Ruby Version

Just write the version of Ruby you want to install and hit enter using the command below
Right now, I am going to install Ruby version 2.2.4

{% highlight ruby %}
$ rvm install 2.2.4
{% endhighlight %}

# Step4-Setup Ruby Version as Default

RVM command enable us to set up default Ruby version to our application.

{% highlight ruby %}
$ rvm use 2.2.4 --default.
{% endhighlight %}

If you are unable to set as default, try run this.

{% highlight ruby %}
$ /bin/bash --login
{% endhighlight %}

This command change terminal emulator preferences to allow login shell

And run the RVM command again.

# Step5-Check Ruby Version

After you have set the default Ruby Version, you can check the version of Ruby you have now using the command below.

{% highlight ruby %}
$ ruby --version
{% endhighlight %}

There you go, you got the Ruby version that you want.

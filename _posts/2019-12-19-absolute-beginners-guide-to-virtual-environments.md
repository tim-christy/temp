---
layout: post
title: "Absolute Beginner's Guide to Virtual Environments"
Author: Tim Christy
---
# Introduction
When I first started in coding in Python, I had no idea what virtual environments were. They were never immediately necessary for me in my coding projects, because for the most part I just used Jupyter Notebooks in Anaconda. Over time, I grew to dislike Anaconda because I didn't understand what it was doing. It just looked like a mess of file installations on my computer and I didn't know what did what. It seemed like a lot was going on and in order to understand it I had to explore it manually. I don't really know how true that is, I probably could have been able to figure out Anaconda just as well, but the approach I took was to start with a text editor and use Ipython. Later that grew to include Jupyter Notebooks. In the blog that follows, you'll find an introduction to what virtual environments are, several ways to manage them, and the way I currently manage them.   

There is also information about pyenv at the end which, simply put, is a package that allows for easy switching between different versions of Python.   



# Virtual Environments   
Often for a project, a fresh installation of Python is not enough. Library imports are needed to add functionality (numpy, pandas, scikit-learn, etc). Using pip, packages containing these library imports can be downloaded to your computer and imported from your computer into your code. But where are these packages being installed? When I first started, I didn't even know enough to care about it. I just wanted to get going on projects with my new text editor/IPython set-up.

So you start a project. You pip install what you need for that project and carry on with it, finish up, and everything works fine. Then you do it again for another project, pip install some new packages for it, and still everything is fine. And then another project, and another, and on like this until bam, you're getting problems importing packages into your latest project. You go ahead and fix it but then other packages start messing up. It feels like everything is going wrong and you have no idea why. Certain packages can't be found and others are creating errors. Eventually you're frustrated enough to completely reinstall everything and waste a lot of time doing so. This is how you learn about virtual environments the hard way.   

When pip installs say pandas, pandas comes with libraries upon which it is dependent. That is to say, those dependencies are automatically installed right alongside pandas. So when you write ``` pip install pandas ``` you are actually installing several packages. Below are the names of the libraries that are installed with pandas.

![](absolute_beginner_imgs/pandas_dependencies.png)

---
layout: post
title: "Absolute Beginner's Guide to Virtual Environments"
Author: Tim Christy
---

<br>

### Introduction
When I first started in coding in Python, I had no idea what virtual environments were. They were never really necessary for me to learn in my coding projects because I just used [Anaconda; which automatically handles virtual environments for you](https://www.anaconda.com/) so you don't have to really learn any of this. In retrospect, this is pretty cool, but I didn't think so several months ago. It just looked like a mess of file installations on my computer and I didn't know what anything did other than take up space. In an effort to understand it all I deleted Anaconda and tried to control everything manually. I started simple with a text editor and IPython from the terminal, but later that grew to include Jupyter Notebooks. In the blog that follows, you'll find what I learned about virtual environments and a good routine for setting up project environments with Jupyter Notebooks (or a text editor).

<br>


### Virtual Environments   
Say you’re starting with a new Mac (or restored from factory settings) and you have a fresh installation of Python. You start a project with this installation, but quickly realize it is not enough to code with. You have to add packages that extend Python’s functionality (like numpy, pandas, scikitlearn, etc). So you install pip, install the packages you need, carry on with the project, finish it up, and everything works fine. Then you do another project, pip install some new packages for it, and still everything is fine. And then another project, and another, and on like this until eventually, you start having problems importing packages into your latest project. You go ahead and fix it but then other packages start messing up. Everything is going wrong and you have no idea why. Every line of code you write seems to produce an error. Certain packages can’t be found and you just installed them. This is all very frustrating and it’s why virtual environments exist.

Here's what's going on: when pip installs pandas, pandas comes with packages upon which it is dependent. Those dependencies are automatically installed right alongside pandas. So when you write ``` pip install pandas ``` you are actually installing several packages - pandas, as well as all the packages pandas depends on.

![](../../../../assets/imgs/blogs/2019-12-18/pandas_dependencies.png)  

The problems described above are due to these dependencies. To generalize, when main_package1 depends on packageA version 2.2.0 and main_package2 depends on the same packageA but with version 1.9.9 you will have problems using main_package2 after updating packageA to version 2.2.0. You probably could explicitly install both versions, but these problems compound when you begin to install many difference packages and all their dependencies for multiple projects. Maybe you could explicitly install every version of every package you've ever used on your computer, but it's way easier just to use a virtual environment for each project.

Virtual environments isolate the packages you use for specific projects and have all the packages you install dedicated only to that project. When you start a virtual environment for a project, it is like starting with a clean slate; nothing outside of a typical download of Python is installed. You have to install all the packages you need for the project in the virtual environment. When you are finished with your project you can output the package names you used to a text file that others can then use later. Once you have this text file, you can delete the virtual environment from your computer.  

Virtual environments are isolated from each other because in order to use them you have to activate them before going into your project. Fail to do so and your project will use the packages that are pointed to by default; which can lead to problems, but they can be fixed again by activating the virtual environment and installing the correct packages.    

<br>

So the basic process is as follows: I want to start a project, so I create a new project folder on my Desktop and cd into it. Then I activate a virtual environment inside this folder. Once the virtual environment is activated, I can start coding my project, using pip installs as needed. With the environment activated, all pip installs will be stored within the environment. If I need to come back to the project later, I can deactivate the virtual environment and reactivate it again later when I want to work on my project again. When I am finished with my project, I create a requirements text that lists all the packages I used in my project. This requirements text will show up in my project folder. Then I push everything up to github, deactivate the virtual environment and delete it from my computer. I typically delete the whole project once it's finished and on github.

<br>
If you found that above description to be lacking in specifics, that is because there are many different virtual environment managers that each have their own specific code to start, activate, deactivate a virtual environment, and different pip installs as well. Some of these are listed below.

<br>

### venv, virtualenv, pipenv  

Initially, I began managing virtual environments with virtualenv. As far as I know, venv and virtualenv do the same thing in that you can use them to create virtual environments for projects. These are fine and they work, but it seems that pipenv is the better way to go.
The reason is due to how you share the packages you used with others. When you are finished with a project, you will want to output a text document that contains a list of all the packages you used for the project and their version numbers. venv and virtualenv do this but they do so in a manner that is harder to understand because the list contains everything used, including development packages, like flake8, and it does not distinguish between low-level and high-level dependencies so it is hard to see what you used for your project without going into it. With pipenv this list is called a pipfile, and it contains the packages a project used in an easier-to-read manner. You can still output a requirements.txt file as well with pipenv.

<br>

### pyenv  
Putting virtual environments aside for a moment, you may want to install pyenv. pyenv is a way to control which version of python is being used for a project. You can also use pyenv-virtualenv to control virtual environments with it, but again, I think pipenv is better due to the aforementioned pipfiles.  
Mac automatically comes with Python 2 and 3 installed on it but I highly suggest not touching anything to do with those installations. Instead, if you install pyenv, you can control everything that has to do with python through it.  How to install this is located here: [https://github.com/pyenv/pyenv](https://github.com/pyenv/pyenv).

In short what this does is hijack your PATH variable through a "shims" directory so that anytime your system does something Python-related, it is directed through the shims path where pyenv lives.

(Real quick: if you don't know what a path variable is, open your terminal and type ```bash echo "$PATH"```. This will print out the all the paths that your computer searches through separated by a ":". When you type "python" in the terminal, your computer goes through each of these paths to look for python and activates the first instance of it it sees. So when shims gets placed on the front of this path, it essentially will always be the first instance of python your computer sees. You can type ``which python`` in your terminal to see the default python your computer is using)


<br>

### pipenv  
You can install pipenv from here [https://pypi.org/project/pipenv/](https://pypi.org/project/pipenv/). This will be your new pip installer and will keep everything contained in a virtual environment dedicated to a project. All you have to do before starting a project is make sure you are in your project folder and type  

``pipenv shell``

This will create a virtual environment specific to the folder you are in. You should see the name of your virtual environment appear above your prompt in the terminal. Then use  

``pipenv install package_name_here``  

to begin installing packages you need for your project. When you are finished with your project, you can write  

``pipenv lock``  

and this will save all the information about the packages used in a pipfile. This file can then be pushed to a repo with your project.  You can also output a requirements.txt file by writing  

`` pipenv lock -r > requirements.txt``

To exit the virtual environment just type ``exit``. To enter it again, go to the folder and type ``pipenv shell``. You can then resume your work like you never left.  

When you are all finished with a project and have already pipenv locked, you can write ``exit`` and then ``pipenv --rm`` to remove the virtual environment.  

To install a virtual environment from a requirements.txt file write  

``pipenv install -r requirements.txt``  

Those are the basics. Some other commands I use somewhat frequently are ``pipenv --venv`` which will show you the path to your virtual environment and  ``pipenv graph`` to see every package that has been installed including all its dependencies.   

More information here: [https://pipenv-fork.readthedocs.io/en/latest/basics.html](https://pipenv-fork.readthedocs.io/en/latest/basics.html)  


<br>
### Using Virtual Environments with Jupyter Notebooks  
When you start your project folder and create a virtual environment in it (``pipenv shell``), you can ``pipenv install jupyter notebooks`` or ``pipenv install jupyterlab``. Once this is done write  

``python -m ipykernel install --user --name=environment_name``  

where enviroment_name is the name of your virtual environment (I don't think it has to be but it's good to know why you made the kernel). When you open up Jupyter, the option to use this kernel should be there. Click on it. Work your project, using pipenv to install packages you need, and then when all is finished, deactivate the kernel by writing  

``jupyter kernelspec uninstall environment_name``

To see a list of all available kernels write  

``jupyter kernelspec list``  

<br>


### My Current Project Workflow  
Below is a quick synopsis of what I am essentially doing followed by code written in my .zshrc file that automates all of this.  

Quick Synopsis:  
For the most part, I start a github repo from a desired template, clone it to my desktop, then use pyenv to choose which version of python I want to work with. Then I use pipenv to start my virtual environment via the process described above (write ``pipenv shell`` in the cloned directory in the terminal).  

I then ``pipenv jupyterlab`` to install Jupyter Lab and create a kernel from my project by following the steps outlined in the previous section. I start my project in Jupyter Lab, use ``!pipenv install package_name_here`` to install packages as I need them in the notebook and work on my project.   

When my project is finished, I exit out of the Jupyter Notebook, write ``pipenv lock``, and ``pipenv lock -r >requirements.txt`` . Then I exit out of the virtual environment (by writing ``exit``) and push everything up to github. Then I delete my virtual environment and remove the kernel I was using for it. And that's it.  

Automation:  
You can automate a lot of the above processes by writing functions in your .zshrc file (cd to your home directory and open your .zshrc file). My functions are shown below.  

![](../../../../assets/imgs/blogs/2019-12-18/zshrc2.png)  
![](../../../../assets/imgs/blogs/2019-12-18/zshrc3.png)  

<br>
In order to use the start_project() function listed above, you need to [go to github and get a repo token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line). This repo token can then be stored as an [environment variable](https://youtu.be/5iWhQWVXosU).  To use this function, type  

``start_project project_name``  

in the command line where ``project_name`` is the name of your project. This function will automatically create a repo with a template in github and on your desktop (I hardcoded this template and it's easy to change).  Then to start a virtual environment you can use the pipenv shell command once inside the directory. Or you can use the function below called ``make_env`` to do this and add autopep8, flake8, and set up the requirements.txt   


<br>

![](../../../../assets/imgs/blogs/2019-12-18/make-env.png)  

After the project is finished, you can use the end_project() function below to remove all kernels, remove the virtual environment, and push to github.  Note to use this function, you must write the project name after end_project, like so  

``end_project project_name``  

where again, ``project_name `` is the name of your project.


![](../../../../assets/imgs/blogs/2019-12-18/end-proj.png)  


---


<br>
<br>
<br>





### References   

1) [Cory Schafer's video on pipenv](https://youtu.be/zDYL22QNiWk).
I highly recommend watching his videos in general. He covers all of this as well as virtualenv, venv, pipenv, and pyenv. I owe a lot of what I understand about this to his explanations.  

2) [Dmitry Figol](https://youtu.be/rRkcMCQoCIo)
This video helped me to understand these topics more as well, but it is very long. About 5 hours.  

3) [This answer by Flimm on Stack Exchange](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)  
Bit of a rabbit hole, but helped me to understand the differences between all of these packages.

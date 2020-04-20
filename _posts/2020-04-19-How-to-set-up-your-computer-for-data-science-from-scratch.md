---
layout: post
title: "Setting up a new Mac for Data Science"
Author: Tim Christy
---
By Tim Christy

The purpose of this post is to document how my computer is set up for data science in case I ever have to do it again. There are a lot of different ways to do this, but the following is the way I'm most comfortable with for the time being.   


1. [Install Homebrew](#install-homebrew)
2. [iTerm2 Set Up](#iterm2-set-up)
3. [Pyenv](#pyenv)
4. [Pipenv](#pipenv)
5. [Postgresql](#Postgresql)
6. [Setting Up Atom with Jekyll Serve](#setting-up-atom-with-jekyll-serve)
7. [Project Workflow](#project-workflow)

<br>

## Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
<br>

## iTerm2 Set Up

- Install iTerm2 by navigating to the [website](https://www.iterm2.com/) or by typing
```bash
brew cask install iterm2
```

- Customize iTerm2 Colors
Go to [this github page](https://github.com/mbadolato/iTerm2-Color-Schemes), download the font you want under the xfce4terminal/colorschemes folder, and follow the steps below but only selecting your desired scheme. To download all of them:

  - Clone the repository
  - Open iTerm2
  - Click on the iTerm2 menu in the upper left corner
  - Select Preferences
  - Click on Profiles
  - Click on the Colors submenu
  - Click on the dropdown box in the bottom right corner
  - Click import
  - Navigate to the iTerm2-Color-Schemes folder you cloned
  - Navigate to Schemes
  - Click Open


Now you can select a color scheme and view it on your iTerm2 terminal.

- Customize iTerm2 Fonts
Navigate to [this github webpage](https://github.com/powerline/fonts) and clone it. Then navigate to the folder (via command line). Once inside the fonts folder type
```bash
./install.sh
```

To change your font, go to the top left corner, select Preferences, then Profiles, then Text in the submenu. There is a drop down menu where you can select your desired font.

- Customize iTerm2 Theme
Type this into the command line
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

This downloads many different themes. You can preview [screenshots of them here](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes). To use a theme, navigate to your home directory and open the .zshrc file with a text editor. The default will be "robbyrussell". Change this to whichever theme you prefer. You can also type "random" to have random themes load each time you open the terminal.

You may get some text about insecure files when you open your prompt. Pasting and running the code provided by the prompt cleared it up for me.

<br>

## Pyenv

Install [pyenv](https://github.com/pyenv/pyenv#homebrew-on-macos)

In terminal, write
- ``` bash
brew install pyenv
```
- ```bash
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.zshrc
```
- ```bash
exec "$SHELL"
```
- ```bash
pyenv install 3.8.0
```
or whichever version you prefer rather than 3.8.0.

<br>

## Pipenv
Install [pipenv](https://pypi.org/project/pipenv/)

```bash
brew install pipenv
```


<br>

## Postgresql
Install [Postgresql](https://postgresapp.com/downloads.html) by downloading the second download option on that site. The first one only comes with one version while the second can handle several versions.

Once it's done downloading initialize a server and click on it. This should bring up your terminal. At the top of the terminal it will list the path at which psql is found. (/Applications/Postgres.app/Contents/Versions/12/bin)

Open .zshrc and append this to your PATH variable. Postgresql is good to go.

<br>

## Setting up Atom with Jekyll Serve
Download [atom](https://atom.io/), install platformio terminal in the settings, and then type in the following
- ```bash
xcode-select --install
```
- ```bash
brew install rbenv
```
- ```bash
rbenv init
```
- paste
```bash
eval "$(rbenv init -)"
```
into .zshrc (before exports)
- ```bash
rbenv install 2.7.1
```      (or latest)
- ```
bash rbenv global 2.7.1
```
- ```bash
gem install --user-install bundler jekyll
```
- ```bash
echo 'export PATH="$HOME/.gem/ruby/2.7.0/bin:$PATH"' >> ~/.bash_profile
```
- ```bash
gem install minima
```
- ```bash
gem install jekyll-feed
```

If you have problems with the port (i.e., "Address already in use - bind(2) for 127.0.0.1:4000") try

```bash
ps aux | grep jekyll
```

The first set of numbers returned is the port number. Then write

```bash
kill -9 (port_number)
```

Then restart jekyll serve.

<br>

## Project Workflow

- Make a directory where you would like to store your project and cd into it
- ```bash
pipenv install ipykernel
```
- ```bash
pipenv shell
```
- ```bash
python -m ipykernel install --user --name=name_of_virtual_environment
```
- ```bash
jupyter notebook
```

Then you can start your project. Use

```python
import sys
!{sys.executable} -m pip install package_name_here
```

to install packages.

When you have completed the project, exit out of Jupyter and write

 ```bash
 pipenv lock
 ```
 and
```bash
pipenv lock -r > requirements.txt
```

 You can then begin removing the environment and the kernel. To view the list of kernels:


```bash
jupyter kernelspec list
```

To remove a kernel:

```bash
jupyter kernelspec uninstall name_of_virtual_environment
```

and to remove the environment, make sure you've exited the environment (by writing ``` exit ```) and write:

```bash
pipenv --rm
```

Later, to install a requirements.txt file you can use:

```bash
pipenv install -r requirements.txt
```

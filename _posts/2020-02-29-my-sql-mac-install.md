---
layout: post
title: "MySQL Installation (Mac)"
Author: Tim Christy
---
There is a [great video here](https://youtu.be/9sbUsbDWTE8) that goes over the installation on Mac if preferred.

You can download the server [(macOS 10.15 (x86, 64-bit), DMG Archive) by clicking here](https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.19-macos10.15-x86_64.dmg) or by going to [www.mysql.com](https://www.mysql.com), clicking on "Downloads", scrolling to the bottom and clicking on "MySQL Community (GPL) Downloads", then clicking "MySQL Community Server", choosing your installation, and then clicking "No thanks, just start my download".

Follow the set-up instructions. It is important that you remember the password you create during the set-up. This password allows you to access the server. If you did not enter a password, that's ok, I'll explain how to deal with that after downloading the workbench.

Download the workbench [(macOS (x86, 64-bit), DMG Archive) by clicking here](https://dev.mysql.com/get/Downloads/MySQLGUITools/mysql-workbench-community-8.0.19-macos-x86_64.dmg) or by going to [www.mysql.com](https://www.mysql.com), clicking on "Downloads", scrolling to the bottom and clicking on "MySQL Community (GPL) Downloads", then clicking "MySQL Workbench", choosing your installation, and then clicking "No thanks, just start my download".

Install the workbench and drag it over to your applications folder.

Once that is installed, to set up a server with a password, navigate to your System Preferences. At the bottom you should see a MySQL icon. Click on that and click on "Initialize Database". Enter a password and then click "Ok". Next click "Start MySQL Server" and you should be good to go.

Open the MySQL Workbench, click on the root user, enter your password, and you are all set to start coding.

If you prefer to work with MySQL from the terminal, open your .zshrc file and paste in the following   

``export PATH=/usr/local/mysql/bin:$PATH``

Then save and open a new terminal. To start the server from the terminal write   

``mysql -u root -p``

It will then prompt you for your password. Enter it and your all set to code in the terminal.

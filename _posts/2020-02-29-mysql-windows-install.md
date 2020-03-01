---
layout: post
title: "MySQL Installation (Windows)"
Author: Tim Christy
---
by Tim Christy   


There are newer versions of MySQL available here [https://dev.mysql.com/downloads/](https://dev.mysql.com/downloads/), but they did not work for my computer. For this reason, I'm using an older version that is stable and installed without errors.    

The version I used is 5.6.13 and is available for download here: [mysql-installer-community-5.6.13.1.msi](https://drive.google.com/file/d/1ZqeVimWS77Xpy5LN6Oi73I6nu8h0KZNI/view?usp=sharing)  

After downloading that and starting the install you will see this  

![](../../../../../assets/imgs/blogs/2020-02-29/win1.png)  

Click ``Install MySQL Products``, agree to the terms, and skip the updates. After this, you will see the following  

![](../../../../../assets/imgs/blogs/2020-02-29/win2.png)  

You can choose which install you prefer. I would recommend either Developer or Full install.


Continue through the set-up wizard until you arrive at this page   

![](../../../../../assets/imgs/blogs/2020-02-29/win3.png)  

*Here it is important that you remember the password you input otherwise you will be unable to access the server.* Input your password and remember it. On the following page you can name your server instance. I will leave mine with the default name of MySQL56. Continue with the installation until you get to the end screen shown below  

![](../../../../../assets/imgs/blogs/2020-02-29/win4.png)   

Click "Finish" and the workbench should start. This is an interface that allows you to interact with the server.  

![](../../../../../assets/imgs/blogs/2020-02-29/win5.png)  

Double click on the "Local Instance" box and input your password from before and that's it. You should be able to see the following

![](../../../../../assets/imgs/blogs/2020-02-29/win6.png)   

and that's it. Installation is complete and this is what you will use to do all your database tasks with MySQL.

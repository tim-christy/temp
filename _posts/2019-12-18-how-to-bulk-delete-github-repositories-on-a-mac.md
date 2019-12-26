---
layout: post
title: "How to Bulk Delete Github Repositories on a Mac"
categories: Github
author: Tim Christy
---
If there are any, I'd recommend cloning the repos you’d like to keep onto your local computer before doing this.  
<br>
$$\textbf{1.}$$ Go to your github homepage and create a Personal Access Token   
&nbsp; &nbsp; &nbsp; &nbsp;  1a. On the home page, click on the arrow in the upper right corner   
&nbsp; &nbsp; &nbsp; &nbsp;    1b. Click on “Settings”    
&nbsp; &nbsp; &nbsp; &nbsp;    1c. At the bottom left column, click on “Developer Settings”    
&nbsp; &nbsp; &nbsp; &nbsp;    1d. Click “Personal Access Tokens”    
<br><br>
$$\textbf{2.}$$ Generate a new token and copy it to your clipboard  
<br><br><br>
$$\textbf{3.}$$ Open terminal and open .zshrc in a text editor and write

```bash
export DELETE_REPO_TOKEN=(paste your repo token here)
```

    save and close .zshrc.   
<br><br><br>

$$\textbf{4.}$$ brew install gnu-sed   

```bash
brew install gnu-sed
```  
<br><br><br>
$$\textbf{5.}$$ Open a text editor again and paste in the following code [1](#sources) & [2](#sources). Make sure you know the file path of where you save it.  

<script src="https://gist.github.com/tim-christy/25f838122d415fb02eb5043a1f5441ac.js"></script>   
<br><br><br>

$$\textbf{6.}$$  Run the following in the terminal  

```bash
bash path/to/script/delete_all_my_github_repositories.
```


This deleted around 30 repos each time it ran. I ended up running a for loop in a Jupyter Notebook to delete everything.  

<img src="../../../../assets/imgs/blogs/2019-12-18/delete_repos_loop.png">  

After you're done, don't forget to delete your Personal Access Token so that it is no longer active on GitHub.   

And that's it, all your repos should be deleted.
<br><br><br><br>
# Sources
[1] [https://gist.github.com/andybeak/602611212950559df9c102b0d1ae20c7](https://gist.github.com/andybeak/602611212950559df9c102b0d1ae20c7)   
[2] [https://github.com/pyrsmk/molt/issues/8](https://github.com/pyrsmk/molt/issues/8)

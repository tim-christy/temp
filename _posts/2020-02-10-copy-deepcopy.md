---
layout: post
title: "Copy and Deepcopy in Python"
Author: Tim Christy
---

### Assignment Operator

In Python, when you use the equal sign, it might not behave like you'd expect it to. For example, suppose you want to make a copy of a list and you do the following

{%highlight python%}
list1 = ['a', 'b', 'c']
list2 = list1
{%endhighlight%}

You might think you've made a copy of ``list1`` called ``list2``, but you have not. Instead you've made a reference to the same memory location. You can use the ``id()`` function to see the id of the objects. Here you'll see that they are the same.  

{%highlight python%}
print(id(list1))
print(id(list2))
id(list1)==id(list2)
{%endhighlight%}

4581973440  
4581973440  


True


This means that if I proceed to work on list2, I will simultaneously be working on list1

{%highlight python%}
list2.append(1)
list2.append(2)
list2.append(3)
{%endhighlight%}

As expected list2 now has the added elements 1, 2, and 3 added, but perhaps less expectedly, so does list1  

![](../../../assets/imgs/blogs/2020-02-10/list_copies.png)

### Copy
This is why copy functions exist. There are a few ways in which you can copy a list that does not share the same id as the original.

You can do so with the copy method, by adding .copy() to the end of the list variable to be copied as shown below

![](../../../assets/imgs/blogs/2020-02-10/copies.png)


Below are some other ways to make legitmate copies as well


![](../../../assets/imgs/blogs/2020-02-10/legit_list.png)


### What is deepcopy?

Every copy method shown above essentially does the same thing; including deepcopy for this type of object. But a problem arises when you start getting into matrices. Take the following for example  

![](../../../assets/imgs/blogs/2020-02-10/A.png)  

If I use copy on this it works out for the rows  

![](../../../assets/imgs/blogs/2020-02-10/row_copy.png)  

It did not alter matrix A like expected. However, when I want to alter an element...   

![](../../../assets/imgs/blogs/2020-02-10/element_copy.png)  


The original gets altered too. That is because the other forms of copying are shallow copies that do not get into the elements of our matrix. Really it is a list of lists, and so the shallow copies only copy the first objects in the outer list (which are lists). This is why changing a whole list worked out with the shallow copy. If you want to copy every element in the matrix and leave the original intact as you manipulate elements of the copy, use the deepcopy function.   



![](../../../assets/imgs/blogs/2020-02-10/deepcopy.png) 

---
layout: post
title: "Basic Web Scraping with Beautiful Soup"
Author: Tim Christy
---
by Tim Christy  
<br>

### Introduction  
What is web-scraping? It's taking data from web pages and storing them elsewhere. Via webscraping, you can select data from web pages and store that data into a csv, database, etc.  

There is a bit of legal ambiguity around the scraping of websites to be aware of. It seems to me that so long as the data you are scraping is meant for anybody who visits the site, it is likely ok. If you use it after you get past a paywall, that's probably not legal. Here are a list of articles regarding the legality of it for those who are interested.  

[US court says scraping a site without permission isn’t illegal](https://thenextweb.com/security/2019/09/10/us-court-says-scraping-a-site-without-permission-isnt-illegal/)  

[Is Web Scraping Legal? 6 Misunderstandings About Web Scraping](https://www.import.io/post/6-misunderstandings-about-web-scraping/)  

[Is Web Scraping Legal? Top 3 Legal Issues in Web Scraping](http://scrapingauthority.com/2016/08/22/web-scraping-legal)

[Is web crawling legal?
](https://towardsdatascience.com/is-web-crawling-legal-a758c8fcacde)

We're going to be scraping data from wikipedia, which allows for web scraping. The site we will be scraping in particular is [List of countries and dependencies by population](https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_by_population).


<br>


### The Packages

We will be using urllib and BeautifulSoup to do out scraping. urllib is part of the Python standard library and should come with Python. If you do not already have BeautifulSoup, you can pip install it via  

```python  

pip install beautifulsoup4

```  

pandas is also imported to help with the storing of the data later.   

```python  
from urllib.request import urlopen
from bs4 import BeautifulSoup
import pandas as pd  
```  

Once these are imported, we can access the web page using the urllib library. The following lines of code do the following:  

1) Store the url in string format into a variable URL   

2) Opens the web page at the given url    

3) Reads in all the html data and stores this data into a variable called html      

4) Closes the connection to the website  

```python  
URL = 'https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_by_population' # 1)  

uClient = urlopen(URL) # 2)  

html = uClient.read() # 3)  

uClient.close() # 4)  
```

If we observe the html variable from above, we see a mess of html data that was taken from the webpage. Below is a preview of the first of many many more lines.

![](../../../assets/imgs/blogs/2020-02-09/html_mess.png)

We can begin to clean this up with BS4. First we create a BeautifulSoup object, which allows us to use BeautifulSoup's functions to parse through the html data. To make the object we pass our html variable created above and the type of parser we would like to use. We will be using 'html.parser' although there are more options than that. You can read about them [here](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#installing-a-parser). Once the soup object is created, your can use the prettify() method to observe a more structured output of the html data.  

```python  
soup = BeautifulSoup(html, 'html.parser') # Create soup object  
print(soup.prettify())  
```   


![](../../../assets/imgs/blogs/2020-02-09/prettify_html.png)

<br>

### Navigating the HTML Data

BeautifulSoup has methods that make finding data in the html easier. The way this works is by referencing the tags in the html (tags are what's enclosed in the angel brackets; for example \< a \> is an anchor tag). You can search through the html by using the find_all method and passing the tag name you are interested in in brackets. One way to identify the tags of interest in a web page is by going to the web page, right clicking, and selecting "Inspect" as shown below (Google Chrome is being used here; may be different on other web browsers).  

<br>

![](../../../assets/imgs/blogs/2020-02-09/inspects.png)  

<br>

The html data will appear in the upper right corner as shown above. As you hover over the html, the corresonding parts on the web page will be highlighted. You can use this feature to see where the data you are interested in is located. For example, below we want to start at the table. Moving along through the html data shows us where we should start to gather this data.    

<br>

![](../../../assets/imgs/blogs/2020-02-09/highlight.png)  

<br>

### Grabbing the relevant data section

It looks like the 'td' tags contain the information we are interested in. We can use the find_all method on our soup object to grab this section by passing 'td' as an argument. This will then allow us to begin parsing through the section we are interested in for the data.  

```python
data = soup.find_all('td') # Grab the table data section  
```  
<br>

### Parsing to grab the data of interest

There are probably better ways to do this, but this is how I do it. The data object that has been created can be treated like a list in that it can be iterated through. Typically, I find a way to extract and store the data I am interested in for one row, and then iterate the process with a for loop for the rest of the data. As you can see below, the first item in the object is the rank, the second has the country name, the next has the population data, then the date, followed by the source. The row then repeats in a similar manner when we reach the seventh item in the object (seventh because of zero-indexing).   

![](../../../assets/imgs/blogs/2020-02-09/data_parsing.png)  

<br>

All we have to do is pick out the data of interest and store it for each iteration. You can pick out the data by using the contents attribute. This attribute selects the contents out from the html tags and stores the elements in a list. If the result isn't what you want, you can continue to parse it down by reusing a combination of indexing and contents. Below we parse out the info we would like for the first row.  

![](../../../assets/imgs/blogs/2020-02-09/contents_ex.png)   

We just want the country name here and the contents attribute returned way more than we wanted. To get around this we can index the spot in the list that contains the data we want and then use the contents attribute again.  

![](../../../assets/imgs/blogs/2020-02-09/country_content.png)   

The above is how we will grab country names in our loop. Let's look at how to grab the rest.  

![](../../../assets/imgs/blogs/2020-02-09/pop_dat_contents.png)   

<br>

### Iterating the process

Now that we have the genral layout for where our data lies in each row, we can iterate through this process by adjusting the numbers for each row. You may think that because the length of the data object is 1458 and there are 6 items per row, that there is 1458/6 = 243 rows. I did. This turned out to be incorrect because the data object holds data past the rows. I only found this out by attempting to implement the loop for that many rows only to recieve "list index out of range errors". I found the correct number of rows by manually searching the end of the data object to see where the last country occurs. It happens at index 1441 and so there are actually 1446/6 = 241 rows.  

Second thing: the indexing appeared to shift a bit with the contents between two different formats. Ergo, a try-except was implemented to catch both formats. You can see the two different formats based on the way the each of the countries data is appended in the two clauses.  

```python  
countries = []
pop = []
date = []

num_of_rows = 241 # There are 6 items per row.

for row_num in range(0, num_of_rows):


    try:
        countries.append(data[1 + row_num*6].contents[2].contents[0])
        pop.append(data[2+row_num*6].contents[0])
        date.append(data[4+row_num*6].contents[0].contents[0])

    except:
        countries.append(data[1+row_num*6].contents[0].contents[2].contents[0])
        pop.append(data[2+row_num*6].contents[0])
        date.append(data[4+row_num*6].contents[0].contents[0])
```  

As a quick check, I know that there are 241 countries on the web page. I can use the ```python len()``` function to make sure I have them all.  

![](../../../assets/imgs/blogs/2020-02-09/len.png)       

<br>

### Now to prepare the data for storage

From here you can just store this data into a dataframe and export to a csv as follows  

```python  
temporary_dictionary = {'Country': countries, 'Population':pop, 'Date':date}   

populations_df = pd.DataFrame(temporary_dictionary)    

populations_df
```
![](../../../assets/imgs/blogs/2020-02-09/pop_df_not_clean.png)   

```python  

populations_df.to_csv('populations.csv')  

```

<br>

### But Note a Little Cleaning is Very Helpful Before Storing

The data has been successfully scraped although it does still need to be cleaned. The population column for instance is a string data type, which needs to be converted to an integer in order to use many plotting features with it. That can quickly be done via the code below and then exporting. The Date column is also a string and may need to be converted depending on your analysis.   

```python  
populations_df['Pop Fixed'] = populations_df['Population'].str.replace(',', '').astype(int)  
populations_df['DateTime Date'] = pd.to_datetime(populations_df['Date'])  
populations_df.head()  
```  

![](../../../assets/imgs/blogs/2020-02-09/pop_df_head.png)  

<br>

### Dropping the old columns
Dropping the unnecessary columns, and renaming the new ones, we can export the relevant data to csv.  

```python  
populations_df.drop(columns=['Population', 'Date'], inplace=True)  
populations_df.columns = ['Country', 'Population', 'Date']  
populations_df.head(5)  
```  

![](../../../assets/imgs/blogs/2020-02-09/clean_df_head.png)  

<br>

### This is a nicer dataset to export  


```python  
populations_df.to_csv('cleaned_populations_data.csv')
```  
<br>

### Final Thoughts

Using the methods shown above can take you pretty far in gathering the data you want from a web page. Again I typically do it for one row and then loop through the rest. There will inevitably be minor problems as we saw above and you will have to adjust for them; like how the pattern in which I was extracting each row changed through some of the iterations. Through trial and error you can fix the loop and grab what you need.

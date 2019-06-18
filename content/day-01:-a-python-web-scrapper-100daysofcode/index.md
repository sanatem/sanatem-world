---
title: "Day 01: A Python Web scrapper #100DaysOfCode"
description: "Nowadays we hear a lot this word: \"scrapper\", but.. everyone does actually know what is it? For the ones who don’t know, a scrapper is a tool which is built for scan a website and retrieve some data…"
date: "2017-07-12T03:34:16.816Z"
categories: 
  - Python
  - Python3
  - Web Development
  - Scraping
  - Tutorial

published: true
canonical_link: https://medium.com/@sanatem/day-01-a-python-web-scrapper-100daysofcode-43bafc69366
redirect_from:
  - /day-01-a-python-web-scrapper-100daysofcode-43bafc69366
---

Hello everyone, I'm Santiago and this is the first episode of #100DaysOfCode!

_All the code for this project can be found on my_  [**_Github_**](https://github.com/sanatem/100DaysOfCode/tree/master/day01_simple-python-scrapper)**_._**

### Challenge: Build a web scrapper

Nowadays we hear a lot this word: "scrapper", but.. everyone does actually know what is it? For the ones who don’t know, a scrapper is a tool which is built for scan a website and retrieve some data.

In this first mini-project I am going to extract some data from the HackersNews website ([https://news.ycombinator.com/](https://news.ycombinator.com/)).

The final result I expect is a list with some useful dictionaries:

```
[{'news title':' link '},..]
```

In other day-project I will use this hashes for some frontend purpose. Stay tuned!

Ok ! Let’s do it !

### Solution

For this solution I used mainly 2 wide-known libraries (Installation details in repository):

-   **Requests:** A Web Client for doing some HTTP requests.
-   **Beautiful Soup:** A popular library for pulling data out HTML.

**Step 1:** We use the requests library to get the HTML document.

```
response = requests.get(“https://news.ycombinator.com/")
```

**Step 2:** Create a Beautiful Soup object

```
soup = BeautifulSoup(html)
```

**Step 3:** Retrieve the table of news, with the find method of the BeautifulSoup object. The **_find()_** method return the exact HTMLelement of the website.

```
table = soup.find(‘table’)
```

**Step 4:** Iterate over the rows of the table, get each link and title with the **_findAll_**  method which retrieves a ResultSet. We can also filter the attributes of the HTML element, like **_findAll(‘tr’,attrs={‘class’:’athing’})_**.

```
#Links array
links = []
#We iterate over the rows
for row in table.findAll(‘tr’,attrs={‘class’:’athing’}):
 for cell in row.findAll(‘td’,attrs={‘class’:’title’}):
 link = cell.find(‘a’,attrs={‘class’:’storylink’})
 if link:
 links.append({link.text.encode(‘utf-8’) : link.get(‘href’).encode(‘utf-8’)})
```

The result:

```
[
{‘How a VC-funded company is undermining the open-source community’: ‘https://theoutline.com/post/1953/how-a-vc-funded-company-is-undermining-the-open-source-community'},
{‘Host your own contacts and calendars and share them across devices’: ‘https://partofthething.com/thoughts/host-your-own-contacts-and-calendars-and-share-them-across-devices/'},
...
]
```

---

So far, I built this simple mini-project in my first day, so cheer up ! You can do it as well, if you have some ideas to add to this project or even better: build a new one based on this one, don't hesitaste and fork it on Github!

_Remember, the code for all projects is available_ [**_here_**](https://github.com/sanatem/100DaysOfCode)_._

![Happy coding everyone!](./asset-1.gif)

Stay tuned, for Day 02 project!

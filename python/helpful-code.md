---
description: Helpful Python Code Snippets for Technical SEOs.
---

# Helpful Code

## CTR Curves

```python
def add_ctr(x):
    
    vals = {"1":0.2759,
            "2":0.14415,
            "3":0.09255,
            "4":0.06265,
            "5":0.0639,
            "6":0.03285,
            "7":0.02305,
            "8":0.0173,
            "9":0.0135,
            "10":0.0108,
            "11":0.00925,
            "12":0.00925,
            "13":0.0099,
            "14":0.0095,
            "15":0.0096,
            "16":0.0097,
            "17":0.01025,
            "18":0.01125,
            "19":0.01185,
            "20":0.0129}
    return vals[str(x)]
```

## Random User-Agent Strings

Helpful for crawling pages that don't like default Python Requests library User-Agents.

```python
import random

def getUA():

    uastrings = ["Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/38.0.2125.111 Safari/537.36",\
                "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/28.0.1500.72 Safari/537.36",\
                "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10) AppleWebKit/600.1.25 (KHTML, like Gecko) Version/8.0 Safari/600.1.25",\
                "Mozilla/5.0 (Windows NT 6.1; WOW64; rv:33.0) Gecko/20100101 Firefox/33.0",\
                "Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/38.0.2125.111 Safari/537.36",\
                "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/38.0.2125.111 Safari/537.36",\
                "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_5) AppleWebKit/600.1.17 (KHTML, like Gecko) Version/7.1 Safari/537.85.10",\
                "Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; rv:11.0) like Gecko",\
                "Mozilla/5.0 (Windows NT 6.3; WOW64; rv:33.0) Gecko/20100101 Firefox/33.0",\
                "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/38.0.2125.104 Safari/537.36"\
                ]

    return random.choice(uastrings)
```

## Pull Title and Description from URL

```python
from bs4 import BeautifulSoup
import requests

# Use beautifulsoup to fetch page titles.
def fetch_meta(url):
    #Set UA as Googlebot as the server will only serve to GB
    headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.117 Safari/537.36'}  
    result = {'title':'', 'description':'', 'error':''}

    try:
        #Send a GET request to grab the file
        response = requests.get(url, headers=headers, timeout=3)

        #Parse the response
        soup = BeautifulSoup(response.text)

        #Extract the title
        result['title'] = soup.title.string
        description_tag = soup.find('meta', attrs={'name':'description'})
        if description_tag is not None:
            result['description'] = description_tag.get('content')

    except Exception as e:
        result['error'] = str(e)
    
    return result

    
```
Example: 
out = fetch_meta('https://i.codeseo.dev')
out

    [1] {'title': 'Development Resources for Technical SEOs - iCodeSEO',
     'description': 'i.codeseo.dev is a repository of code and reference library for Technical SEOs who are interested in development and data science.',
     'error': ''}
```
```


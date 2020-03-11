---
description: Helpful Python Code Snippets for Technical SEOs.
---

# Helpful Code

## CTR Curves

Useful for gathering simple Share-of-Traffic information from ranking position.  Date can be found at: [https://www.advancedwebranking.com/ctrstudy/](https://www.advancedwebranking.com/ctrstudy/).  Most major tool providers have individualized CTR curves for keywords or keyword sets.

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

Simple example of using the requests and BeautifulSoup libraries to pull `<title>` and `<meta name="description" content="..." />` from live URLs.

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

## Import Multiple Google SERPs on a Large Scale

**Setup:**

1. [Create a custom search engine](https://cse.google.com/cse/). At first, you might be asked to enter a site to search. Enter any domain, then go to the control panel and remove it. Make sure you enable "Search the entire web" and image search. You will also need to get your search engine ID, which you can find on the control panel page.
2. [Enable the custom search API](https://console.cloud.google.com/apis/library/customsearch.googleapis.com). The service will allow you to retrieve and display search results from your custom search engine programmatically. You will need to create a project for this first.
3. [Create credentials for this project](https://console.developers.google.com/apis/api/customsearch.googleapis.com/credentials) so you can get your key.
4. [Enable billing for your project](https://console.cloud.google.com/billing/projects) if you want to run more than 100 queries per day. The first 100 queries are free; then for each additional 1,000 queries, you pay USD $5.

```python
$ pip install advertools

import advertools as adv
cx = 'YOUR_GOOGLE_CUSTOM_SEARCH_ENGINE_ID'
key = 'YOUR_GOOGLE_DEVELOPER_KEY'

serp = adv.serp_goog(cx=cx, key=key,
                     q=['first query', 'second query', 'third query'],
                     gl=['us', 'ca', 'uk'])

# many other parameters and combinations are available, check the documentation for details
```

## Crawl a Website by Specifying a Sitemap URL

This spider will crawl pages specified in an XML sitemap\(s\), and extract standard SEO elements \(title, h1, h2, page size, etc.\). The output of this crawl will be saved to a CSV file. 

How to run: 

1. Modify the `sitemap_urls` attribute by adding one or more sitemap URLs. A sitemap index page is fine, and will go through all sub sitemaps. Or you can specify normal sitemaps.
2. \(optional\): Modify any elements that you want to scrape \(publishing date, author name, etc.\) through CSS or Xpath selectors.
3. Save the file with any name e.g. `my_spider.py`
4. From your terminal, run the following line: 

   `scrapy runspider path/to/my_spider.py -o path/to/output/file.csv`

where `path/to/output/file.csv`is where you want the scrape result to be saved.

```python
from scrapy.spiders import SitemapSpider

user_agent = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36',


class SEOSitemapSpider(SitemapSpider):
    name = 'seo_sitemap_spider'
    sitemap_urls = [
        'https://www.example.com/sitemap-index.xml',  # either will work, regular sitemaps or sitemap index files
        'https://www.example.com/sitemap_1.xml',
        'https://www.example.com/sitemap_2.xml',
    ]
    custom_settings = {
        'USER_AGENT': user_agent,
        'DOWNLOAD_DELAY': 0,  # you might need to make this a 3 or 4 (seconds)
                              # to be nice to the site's servers and
                              # to prevent getting banned,
        'ROBOTSTXT_OBEY': True,  # SEOs are polite people, right? :)
        'HTTPERROR_ALLOW_ALL': True
    }

    def parse(self, response):
        yield dict(
            url=response.url,
            title='@@'.join(response.css('title::text').getall()),
            meta_desc=response.xpath("//meta[@name='description']/@content").get(),
            h1='@@'.join(response.css('h1::text').getall()),
            h2='@@'.join(response.css('h2::text').getall()),
            h3='@@'.join(response.css('h3::text').getall()),
            body_text='\n'.join(response.css('p::text').getall()),
            size=len(response.body),
            load_time=response.meta['download_latency'],
            status=response.status,
            links_href='@@'.join([link.attrib.get('href') or '' for link in response.css('a')]),
            links_text='@@'.join([link.attrib.get('title') or '' for link in response.css('a')]),
            img_src='@@'.join([im.attrib.get('src') or '' for im in response.css('img')]),
            img_alt='@@'.join([im.attrib.get('alt') or '' for im in response.css('img')]),
            page_depth=response.meta['depth'],
        )
```

Items that contain multiple elements, like multiple H2 tags in one page will be listed as one string separated by two @ signs e.g. `first h2 tag@@second tag@@third tag` You simply have to split by "@@" to get a list of elements per page. 


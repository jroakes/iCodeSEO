---
description: >-
  This post tries to cover many SEO items that can be handled via plain vanilla
  Google Chrome without any tools
---

# Google Chrome SEO Without A Plugin

There are numerous add-ons for Chrome that handle many SEO data gathering tasks, but those are not covered here. For those that are unsure about the security of those add-ons, or whether they are mining Litecoin in the background and eating up your CPU cycles, this post is for you. But more over, it is just a reason to play around with Google searches, Chrome Developer Tools, and the Console.

## Google Searches <a id="googlesearches"></a>

In this section we cover a few common Google search operators used in SEO. Please let me know what I missed.

### Canonical content check <a id="canonicalcontentcheck"></a>

info:{url}

```text
info:https://www.codeseo.io
```

### On-page internal link candidates <a id="onpageinternallinkcandidates"></a>

site:{domain} {keyword}

```text
site:codeseo.io "googlebot"
```

  
 Bonus Points: Also the way to see if the correct page is ranking for a particular query.

### Pages that haven't moved to https <a id="pagesthathaventmovedtohttps"></a>

site:{domain} -inurl:https

```text
site:amazon.com -inurl:https
```

### If your page is cached by Google <a id="ifyourpageiscachedbygoogle"></a>

cache:{url}

```text
cache:https://codeseo.io
```

### Useful parameters in Google searches <a id="usefulparametersingooglesearches"></a>

* **nearby={city}**: Filters search results to nearby city.
* **filter=0**: Remove personalization from Google results.
* **num=100**: Display 100 Google results.

Most of the above provided by [Victor Pan](https://twitter.com/victorpan). Thanks for the idea for this post Victor. Please follow him on Twitter.

In this section we cover using the Console in Developer Tools to get data from Google and your pages in Chrome.

### Scrape Google links <a id="scrapegooglelinks"></a>

```text
$$('h3 a').join('\n')
```

### Scrape Google Images <a id="scrapegoogleimages"></a>

```text

var imgs=$$('a'); var out = [];
for (i in imgs){
  if(imgs[i].href.indexOf("/imgres?imgurl=http")>0){
		out.push(decodeURIComponent(imgs[i].href).split(/=|%|&/)[1].split("?imgref")[0]);
	}
}
out.join('\n')
```

  
 Hat tip to Peter Nikolow. Read more at his blog [here](http://peter.nikolow.me/kak-da-smaknem-kartinki-ot-google-images/) \(Bulgarian\).

### Count links on a page <a id="countlinksonapage"></a>

```text
$$('a').length
```

### See the page title <a id="seethepagetitle"></a>

```text
document.title
```

  
 Bonus Points:

```text
document.title.length
```

### See the page description <a id="seethepagedescription"></a>

```text
document.all.description.content
```

  
 Bonus Points:

```text
document.all.description.content.length
```

### See the robots meta <a id="seetherobotsmeta"></a>

```text
document.all.robots.content
```

### See the canonical <a id="seethecanonical"></a>

```text
$('link[rel="canonical"]')[0]
```

### Easter eggs in Google Search <a id="eastereggsingooglesearch"></a>

```text
document.all['easter-egg']
```

### Edit a page live <a id="editapagelive"></a>

```text
document.designMode = "on"
```

### Get Important N-Grams from Google search results <a id="getimportantngramsfromgooglesearchresults"></a>

```text

var stopwords = [
  'about', 'after', 'all', 'also', 'am', 'an', 'and', 'another', 'any', 'are', 'as', 'at', 'be',
  'because', 'been', 'before', 'being', 'between', 'both', 'but', 'by', 'came', 'can',
  'come', 'could', 'did', 'do', 'each', 'for', 'from', 'get', 'got', 'has', 'had',
  'he', 'have', 'her', 'here', 'him', 'himself', 'his', 'how', 'if', 'in', 'into',
  'is', 'it', 'like', 'make', 'many', 'me', 'might', 'more', 'most', 'much', 'must',
  'my', 'never', 'now', 'of', 'on', 'only', 'or', 'other', 'our', 'out', 'over',
  'said', 'same', 'see', 'should', 'since', 'some', 'still', 'such', 'take', 'than',
  'that', 'the', 'their', 'them', 'then', 'there', 'these', 'they', 'this', 'those',
  'through', 'to', 'too', 'under', 'up', 'very', 'was', 'way', 'we', 'well', 'were',
  'what', 'where', 'which', 'while', 'who', 'with', 'would', 'you', 'your', 'a', 'i', 's']

function nGrams(sentence, limit) {
	
	ns = [1,2,3,4]; var grams = {};
	var words = sentence.replace(/(?:https?|ftp):\/\/[\n\S]+/g, '').toLowerCase().split(/\W+/).filter(function (value) {return stopwords.indexOf(value.toLowerCase()) === -1})
	for (n of ns){
		var total = words.length - n;
		for(var i = 0; i <= total; i++) {
		var seq = '';
		for (var j = i; j < i + n; j++) { seq += words[j] + ' ';}
		if (seq.trim().length < 3) {continue;}else{seq = seq.trim()}
		grams[seq] = seq in grams ? grams[seq] +  1 : 1;
		}
	}
	var sort =  Object.keys(grams).sort(function(a,b){return grams[b]-grams[a]});
	for (s of sort){ if (grams[s] < limit){break;} console.log(s, ':', grams[s]);}
}
	
var gtext = document.all.search.innerText
var ng = nGrams(gtext, 3)
```

### Get Google Analytics info <a id="getgoogleanalyticsinfo"></a>

```text

    for (const [key, value] of Object.entries(ga.getAll()[0].b.data.values) ) {
	if (typeof value === 'string'){
		console.log('%s: %s', key.replace(':',''), value);
	}
}
```

  
 Bonus Points: Check the hit count for your profiles

```text
gaData
```

### See what Google is storing to the google object on search result pages <a id="seewhatgoogleisstoringtothegoogleobjectonsearchresultpages"></a>

```text

for (k of Object.keys(google)){
    if (typeof google[k] !== 'function') {console.log(k,google[k])}
}
```

### Get load timings from PerformanceTiming <a id="getloadtimingsfromperformancetiming"></a>

```text

for (t in window.performance.timing){
	var tAll = window.performance.timing; var t0 = tAll['navigationStart'];
	if (tAll[t] !== "undefined" && (tAll[t]- t0) > 10){
		console.log(t,':', (tAll[t]- t0)/1000, 'secs')
	}
}
```

This section covers some of the best Developer Tools tabs.

### Security <a id="security"></a>

In developer tools. Look for the Security tab to ensure your page and loaded resources are secure.  
 

### Audits <a id="audits"></a>

Use the built-in Lighthouse audits to test your webpage for:

* Speed
* PWA implementation
* Accessibility
* Best Practices
* SEO

You have to get the Chrome [canary build](https://www.google.com/chrome/browser/canary.html) for the SEO audit portion to be available through Developer Tools. Otherwise, use the Chrome plugin for Lighthouse.  
 

### Network <a id="network"></a>

I most often find myself using the network view for a couple things. First, it is great for verifying redirect chaining as long as you have "Preserve log" checked.  
 

It is also great for looking at time-to-first-byte \(TTFB\), the time it took a server to respond to you. Also content download timings for image assets, scripts etc. There is also a nice filmstrip view in the latest canary version which quickly shows rendering progression to time.

### Responsive <a id="responsive"></a>

In responsive view in Developer Tools, it is easy to add additional devices for Googlebot using the user-agent strings found [here](https://support.google.com/webmasters/answer/1061943?hl=en), and window sizes found [here](https://codeseo.io/console-log-hacking-for-googlebot/). This gives you the ability to browse as Googlebot and can uncover strange issues where a particular website either serves bots from different servers or handles those sessions differently. Not a good thing generally.  
 

### Sensors <a id="sensors"></a>

In addition to the above, you can use the More Tools &gt; Sensors portion of Developer Tools to set the latitude and longitude to appear from in Google searches. There are many services that give you the lat/lon information but I generally rely on Google \([Google Maps Api](https://maps.googleapis.com/maps/api/geocode/json?address=boston+ma)\). This option has been glitchy for me in the past. Was brought up by [Victor Pan](https://twitter.com/victorpan), confirmed working by [Dan Hinckley](https://twitter.com/dhinckley)  
 

### Shortcuts: Full Size Screenshots <a id="shortcutsfullsizescreenshots"></a>

This is a great tip from [Anthony Nelson](https://twitter.com/anthonydnelson).

> One of my fave Chrome tips: on Console tab, hit Command+Shift+P to bring up shortcuts. Then type in "screenshot" and select "Capture Full Size Screenshot" - super easy way to get full sized png of a long page.

[Russ Jones is not weird, he just owns a Tesla](https://moz.com/about/team/rjonesx)

## More Amazing Chrome SEO Tips <a id="moreamazingchromeseotips"></a>

* Aleyda Solis has a wonderful writeup on Seach Engine Land: [Chrome’s DevTools for SEO: 10 ways to use these browser features for your SEO audits](https://searchengineland.com/chromes-devtools-seo-10-ways-use-seo-audits-266433)
* Maria Cieślak goes more indepth with Chrome Developer Tools:  [Overview of Chrome Developer Tools’ Most Useful Options for SEO](https://www.elephate.com/blog/chrome-developer-tools-overview/)

That's all I have. If you have anything to add, please comment below or hit me up on [Twitter](https://twitter.com/jroakes).


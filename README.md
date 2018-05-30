# shs-



from urllib.request import urlopen
from xml.dom import minidom
import collections

# extract the headlines from the feed
def extractString(doc):
   str = ""
   for node in doc.getElementsByTagName('channel'):
      for title in node.getElementsByTagName('title'):
         str = str + title.firstChild.data + "\n"
   return str

# extract the feed from the url
def getRSSString(url):
    results = []
    rssString = ""
    results.append(minidom.parse(urlopen(url)))
    for webDoc in results:
        rssString = rssString + extractString(webDoc)
    return rssString



# START HERE ...

# Read the RSS feed from the URL provided
feed = getRSSString("http://www.rte.ie/news/rss/news-headlines.xml")

# Display the results
feed=feed.replace("the","da bleedin")
words=feed.split()
print(collections.Counter(words).most_common(5))

print(feed)
# Display the number of lines
print("There are %d lines in this feed" %feed.count("\n"))


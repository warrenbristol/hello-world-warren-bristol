# hello-world-warren-bristol
This is my first time creating a repository for Open Source GIS 
My name is warren and here is some sample code on subjectivity-sentiment analysis I am running. Ultimately I want to get it into a loop that then connects to an ArcGIS Online Webmap. Maybe I can do so through Jupyter Notebook?:

from textblob import TextBlob
import requests
from bs4 import BeautifulSoup
import csv

class Analysis:
    def __init__(self, term):
        self.term= term
        self.subjectivity = 0
        self.sentiment = 0
        self.url = 'https://google.com/search?q={0}&source=lnms&tbm=nws'.format(self.term)

    def run (self):
        response= requests.get(self.url)
        print(response.text)
        soup= BeautifulSoup(response.text, 'html.parser')
        headline_results= soup.find_all('div', class_='kCrYT')
        for h in headline_results:
            blob= TextBlob(h.get_text())
            self.sentiment += blob.sentiment.polarity / len(headline_results)
            self.subjectivity += blob.sentiment.subjectivity / len(headline_results)


a= Analysis("Baja California")
a.run()
print(a.term, 'Subjectivity', a.subjectivity, 'Sentiment', a.sentiment)


# web-scrapping
import requests
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
import pandas as pd
import csv

news_boxes = []
filtered_sentence = []
source = requests.get('https://www.indiatoday.in/coronavirus-covid-19-outbreak')
soup = BeautifulSoup(source.text,'lxml')
news_box = soup.find_all('div', {'class' : 'catagory-listing'})
for news in news_box:
   print(news.text,"\n")
   bodyword = news.text.split(" ")
   keepword = [word for word in bodyword if word not in stopwords.words('english')]
   news_box = " ".join(keepword)
   news_boxes.append(news_box)
   print(news_boxes, "\n")
pd.set_option('max_colwidth', -1)
df = pd.DataFrame({'news': news_boxes})
print(df)
df.to_csv('news.csv', index=True, encoding='utf-8')

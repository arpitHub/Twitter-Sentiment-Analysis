

```python
# General:
import tweepy           # To consume Twitter's API
import pandas as pd     # To handle data
import numpy as np      # For number computing
```


```python
# For plotting and visualization:
from IPython.display import display
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline
```


```python
CONSUMER_KEY = ""
CONSUMER_SECRET = ""
ACCESS_TOKEN = ""
ACCESS_SECRET = ""
```

$/sqrt(2+x)$

_italic_


```python
# We create an extractor object:
extractor = twitter_setup()

# We create a tweet list as follows:
tweets = extractor.user_timeline(screen_name="lisarobinkelly", count=300)
print("Number of tweets extracted: {}.\n".format(len(tweets)))

# We print the most recent 5 tweets:
print("5 recent tweets:\n")
for tweet in tweets[:5]:
    print(tweet.text)
    print()
```

    Number of tweets extracted: 200.
    
    5 recent tweets:
    
    Lisa is being laid to rest today.  This is a clip she uploaded herself to youtube awhile back and was very proud... http://t.co/SmqLCjYCge
    
    From Lisa's Aunt Kate: 
    
    "Dear Friends of Lisa,
    Lisa's funeral is on Thursday, September 5th in Charlotte, N.C.... http://t.co/5GLjSR1WCB
    
    Hi everyone, this post right now is obviously not from Lisa, but rather I'm good friend who has collaborated with... http://t.co/aL2rm9z4wG
    
    go "like" my friends restaurant page please... https://t.co/lKhn8Fb3Du http://t.co/eerFItRM7q
    
    Tonight, dinner at Mr Souvla.... I need me some Greek.... !! xoxox
    



```python
# We create a pandas dataframe as follows:
data = pd.DataFrame(data=[tweet.text for tweet in tweets], columns=['Tweets'])
#data = data.drop(data.index[[0,1,2]]) #removing last 3 tweets posted by her friend
#data = data.reset_index()

# We display the first 10 elements of the dataframe:
display(data.tail(10))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Tweets</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>190</th>
      <td>@LisaRobin357</td>
    </tr>
    <tr>
      <th>191</th>
      <td>C'mon boston RED SOX NATION!!!</td>
    </tr>
    <tr>
      <th>192</th>
      <td>@BurkhartHyde.</td>
    </tr>
    <tr>
      <th>193</th>
      <td>@DENISE_RICHARDS</td>
    </tr>
    <tr>
      <th>194</th>
      <td>@EMILIOTHEWAY E. Peace and love. Xo</td>
    </tr>
    <tr>
      <th>195</th>
      <td>To walk away from love hurts.......,this time ...</td>
    </tr>
    <tr>
      <th>196</th>
      <td>MISS CALIE!!!!</td>
    </tr>
    <tr>
      <th>197</th>
      <td>Movin today. Everyday in everyway life is gett...</td>
    </tr>
    <tr>
      <th>198</th>
      <td>@EMILIOTHEWAY facebook me!!!</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Listening to music and just chillin.</td>
    </tr>
  </tbody>
</table>
</div>



```python
# Internal methods of a single tweet object:
print(dir(tweets[1]))
```

    ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_api', '_json', 'author', 'contributors', 'coordinates', 'created_at', 'destroy', 'entities', 'favorite', 'favorite_count', 'favorited', 'geo', 'id', 'id_str', 'in_reply_to_screen_name', 'in_reply_to_status_id', 'in_reply_to_status_id_str', 'in_reply_to_user_id', 'in_reply_to_user_id_str', 'is_quote_status', 'lang', 'parse', 'parse_list', 'place', 'possibly_sensitive', 'retweet', 'retweet_count', 'retweeted', 'retweets', 'source', 'source_url', 'text', 'truncated', 'user']



```python
# We print info from the first tweet:
print(tweets[1].id)
print(tweets[1].created_at)
print(tweets[1].source)
print(tweets[1].favorite_count)
print(tweets[1].retweet_count)
print(tweets[1].geo)
print(tweets[1].coordinates)
print(tweets[1].entities)
```

    373278417724391424
    2013-08-30 02:58:04
    Facebook
    1
    4
    None
    None
    {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'http://t.co/5GLjSR1WCB', 'expanded_url': 'http://fb.me/2lJeB4gd6', 'display_url': 'fb.me/2lJeB4gd6', 'indices': [115, 137]}]}



```python
# We add relevant data:
data['len']  = np.array([len(tweet.text) for tweet in tweets])
data['ID']   = np.array([tweet.id for tweet in tweets])
data['Date'] = np.array([tweet.created_at for tweet in tweets])
data['Source'] = np.array([tweet.source for tweet in tweets])
data['Likes']  = np.array([tweet.favorite_count for tweet in tweets])
data['RTs']    = np.array([tweet.retweet_count for tweet in tweets])
```


```python
# Display of first 10 elements from dataframe:
display(data.head(10))
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Tweets</th>
      <th>len</th>
      <th>ID</th>
      <th>Date</th>
      <th>Source</th>
      <th>Likes</th>
      <th>RTs</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lisa is being laid to rest today.  This is a c...</td>
      <td>138</td>
      <td>375630003205337088</td>
      <td>2013-09-05 14:42:26</td>
      <td>Facebook</td>
      <td>16</td>
      <td>9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>From Lisa's Aunt Kate: \n\n"Dear Friends of Li...</td>
      <td>137</td>
      <td>373278417724391424</td>
      <td>2013-08-30 02:58:04</td>
      <td>Facebook</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Hi everyone, this post right now is obviously ...</td>
      <td>139</td>
      <td>368127944746483714</td>
      <td>2013-08-15 21:51:56</td>
      <td>Facebook</td>
      <td>19</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>go "like" my friends restaurant page please......</td>
      <td>93</td>
      <td>350035042921218048</td>
      <td>2013-06-26 23:37:12</td>
      <td>Facebook</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Tonight, dinner at Mr Souvla.... I need me som...</td>
      <td>66</td>
      <td>350033449148616704</td>
      <td>2013-06-26 23:30:52</td>
      <td>Facebook</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Bikram Yoga anyone???</td>
      <td>21</td>
      <td>349908742705389569</td>
      <td>2013-06-26 15:15:19</td>
      <td>Facebook</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Spent the day walking the beach in sunny Calif...</td>
      <td>105</td>
      <td>349735692399677440</td>
      <td>2013-06-26 03:47:41</td>
      <td>Facebook</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>I am having a great day............,free at la...</td>
      <td>110</td>
      <td>348955877665021953</td>
      <td>2013-06-24 00:08:59</td>
      <td>Facebook</td>
      <td>11</td>
      <td>6</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Morning! — feeling happy</td>
      <td>24</td>
      <td>348081811282358274</td>
      <td>2013-06-21 14:15:45</td>
      <td>Facebook</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Root for the underdog.  We have a heart and so...</td>
      <td>70</td>
      <td>346830769974562816</td>
      <td>2013-06-18 03:24:34</td>
      <td>Facebook</td>
      <td>2</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



```python
# We extract the mean of lenghts:
mean = np.mean(data['len'])

print("The lenght's average in tweets: {}".format(mean))
```


```python
# We extract the tweet with more FAVs and more RTs:

fav_max = np.max(data['Likes'])
rt_max  = np.max(data['RTs'])

fav = data[data.Likes == fav_max].index[0]
rt  = data[data.RTs == rt_max].index[0]

# Max FAVs:
print("The tweet with more likes is: \n{}".format(data['Tweets'][fav]))
print("Number of likes: {}".format(fav_max))
print("{} characters.\n".format(data['len'][fav]))

# Max RTs:
print("The tweet with more retweets is: \n{}".format(data['Tweets'][rt]))
print("Number of retweets: {}".format(rt_max))
print("{} characters.\n".format(data['len'][rt]))
```


```python
# We create time series for data:

tlen = pd.Series(data=data['len'].values, index=data['Date'])
tfav = pd.Series(data=data['Likes'].values, index=data['Date'])
tret = pd.Series(data=data['RTs'].values, index=data['Date'])
```


```python
# Lenghts along time:
tlen.plot(figsize=(16,4), color='r');
```


```python
# Likes vs retweets visualization:
tfav.plot(figsize=(16,4), label="Likes", legend=True)
tret.plot(figsize=(16,4), label="Retweets", legend=True);
```


```python
# We obtain all possible sources:
sources = []
for source in data['Source']:
    if source not in sources:
        sources.append(source)

# We print sources list:
print("Creation of content sources:")
for source in sources:
    print("* {}".format(source))
```


```python
# We create a numpy vector mapped to labels:
percent = np.zeros(len(sources))

for source in data['Source']:
    for index in range(len(sources)):
        if source == sources[index]:
            percent[index] += 1
            pass

percent /= 100

# Pie chart:
pie_chart = pd.Series(percent, index=sources, name='Sources')
pie_chart.plot.pie(fontsize=11, autopct='%.2f', figsize=(6, 6));
```


```python
from textblob import TextBlob
import re

def clean_tweet(tweet):
    '''
    Utility function to clean the text in a tweet by removing 
    links and special characters using regex.
    '''
    return ' '.join(re.sub("(@[A-Za-z0-9]+)|([^0-9A-Za-z \t])|(\w+:\/\/\S+)", " ", tweet).split())

def analize_sentiment(tweet):
    '''
    Utility function to classify the polarity of a tweet
    using textblob.
    '''
    analysis = TextBlob(clean_tweet(tweet))
    if analysis.sentiment.polarity > 0:
        return 1
    elif analysis.sentiment.polarity == 0:
        return 0
    else:
        return -1
```


```python
# We create a column with the result of the analysis:
data['SA'] = np.array([ analize_sentiment(tweet) for tweet in data['Tweets'] ])

# We display the updated dataframe with the new column:
display(data.head(10))
```


```python
# We construct lists with classified tweets:

pos_tweets = [ tweet for index, tweet in enumerate(data['Tweets']) if data['SA'][index] > 0]
neu_tweets = [ tweet for index, tweet in enumerate(data['Tweets']) if data['SA'][index] == 0]
neg_tweets = [ tweet for index, tweet in enumerate(data['Tweets']) if data['SA'][index] < 0]
```


```python
# We print percentages:

print("Percentage of positive tweets: {}%".format(len(pos_tweets)*100/len(data['Tweets'])))
print("Percentage of neutral tweets: {}%".format(len(neu_tweets)*100/len(data['Tweets'])))
print("Percentage de negative tweets: {}%".format(len(neg_tweets)*100/len(data['Tweets'])))
```

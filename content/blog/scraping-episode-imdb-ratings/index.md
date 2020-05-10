---
title: "Step-by-step: Scraping Epsiode IMDb Ratings"
slug: scraping-episode-imdb-ratings-tutorial
summary: "There are many tutorials out there that teach you how to scrape movies. This one shows you how to do that for the episodes of a TV series. We use Community as the example."
authors: []
tags: [community, tutorial, python, jupyter notebook, web scraping]
categories: [tutorial, python, web scraping]
date: '2020-05-09'
reading_time: true

external_link: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: true

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
links:
 - name: repository
   url: https://github.com/isabellabenabaye/community-project
   icon_pack: fab
   icon: github

 - name: dataset
   url: https://www.kaggle.com/imbenab/community-episodes-imdb-ratings
   icon_pack: fab
   icon: kaggle

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
toc: true  # Show table of contents? true/false
---
There are tons of tutorials out there that teach you how to scrape movie ratings from IMDb, but I haven't seen any about scraping TV series episode ratings. So for anyone wanting to do that, I've created this tutorial specifically for it. It's catered mostly to beginners to web scraping since the steps are broken down. If you want the code without the breakdown you can find it [here]().

There is a wonderful DataQuest [tutorial](https://www.dataquest.io/blog/web-scraping-beautifulsoup/) by Alex Olteanu that explains in-depth how to scrape over 2000 movies from IMDb, and it was my reference as I learned how to scrape these episodes.    

Since their tutorial already does a great job at explaining the basics of [identifying the URL structure](https://www.dataquest.io/blog/web-scraping-beautifulsoup/#identifyingtheurlstructure) and understanding the HTML structure of a single page, I've linked those parts and recommend you read them if you aren't already familiar because I won't be explaining them here.

In *this* tutorial I will *not* be redundant in explaining what they already did[^1]; instead, I'll be doing many similar steps, but they will be specifically for taking episode ratings (same for any TV series) instead of movie ratings.

[^1]: In the tutorial, they have extra sections where they control the crawl-rate & monitor the loop as it's still going, but we won't do that here because series' have much less episodes (they scraped 2000+ movies) so that's not necessary.      


<br>    
<br>     
    
# Breaking it down
First, you'll need to navigate to the series of your choice's season 1 page that lists all of that season's episodes. The series I will be using is Community. It should look like this:

{{< figure src="01_season_page.png" title="" lightbox="true" >}}

Get the url of that page. It should be structured like this:     

ht<span>tp://ww</span>w.imdb.com/title/<span style="background-color: #ffd850">tt1439629</span>/episodes?season=1       

Highlighted is the part that is the show's ID and will be different for you if you're not using Community.    

First, we will request from the server the content of the web page by using `get()`, and store the server’s response in the variable `response` and look at the first few lines. We can see that inside `response` is the html code of the webpage.


```python
from requests import get
url = 'https://www.imdb.com/title/tt1439629/episodes?season=1'
response = get(url)
print(response.text[:250])
```

    
     
    
    
    
    
    
    
    
    
    
    
    <!DOCTYPE html>
    <html
        xmlns:og="http://ogp.me/ns#"
        xmlns:fb="http://www.facebook.com/2008/fbml">
        <head>
             
            <meta charset="utf-8">
            <meta http-equiv="X-UA-Compatible" content="IE=edge">
    
        <meta name="apple-itunes-app" content="app-id=342792525, app-argument=imdb:///title/tt1439629?src=mdot">
    
      
<br>     

## Use BeautifulSoup to parse the HTML content
Next, we'll parse `response.text` by creating a BeautifulSoup object, and assign this object to `html_soup`. The `html.parser` argument indicates that we want to do the parsing using Python’s built-in HTML parser.


```python
from bs4 import BeautifulSoup

html_soup = BeautifulSoup(response.text, 'html.parser')
type(html_soup)
```




    bs4.BeautifulSoup



<span style="background-color: #ffd850">This part onwards is where the code will differ from the movie example.</span>

**The variables we will be getting are:**
- Episode title
- Episode number
- Airdate
- IMDb rating 
- Total votes
- Episode description

Let's look at the container we're interested in. As you can see below, all of the info we need is in `<div class="info" ...> </div>`:
{{< figure src="02_html.png" title="" lightbox="true" >}}

In <span style="background-color: #ffd850">yellow</span> are the tags/parts of the code that we will be calling to get to the data we are trying to extract, which are in <span style="background-color: #99CC99">green</span>.

We will grab all of the instances of `<div class="info" ...> </div>` from the page; there is one for each episode.


```python
episode_containers = html_soup.find_all('div', class_='info')
```

`find_all()` returned a `ResultSet` object --`episode_containers`-- which is a list containing all of the 25 `<div class="info" ...> </div>`s.
<br>
<br>                 

## Extracting each variable that we need

Read [this part](https://www.dataquest.io/blog/web-scraping-beautifulsoup/#thenameofthemovie) of the DataQuest article to understand how calling the tags works.

Here we'll see how we can extract the data from the `episode_containters` for each episode.

`episode_containters[0]` calls the first instance of `<div class="info" ...> </div>`, i.e. the first episode. After the first couple of variables, you will understand the structure of calling the contents of the html containers.
<br> 

### Episode title
For the title we will need to call `title` attribute from the `<a>` tag.


```python
episode_containers[0].a['title']
```




    'Pilot'
<br> 

### Episode number
The episode number in the `<meta>` tag, under the `content` attribute.


```python
episode_containers[0].meta['content']
```




    '1'
<br> 

### Airdate
Airdate is in the `<div>` tag with the class `airdate`, and we can get its contents the `text` attribute, afterwhich we `strip()` it to remove whitespace.


```python
episode_containers[0].find('div', class_='airdate').text.strip()
```




    '17 Sep. 2009'
<br> 

### IMDb rating
The rating is is in the `<div>` tag with the class `ipl-rating-star__rating`, which also use the `text` attribute to get the contents of.


```python
episode_containers[0].find('div', class_='ipl-rating-star__rating').text
```




    ['7.8', '(3,178)']
<br> 

### Total votes
It is the same thing for the total votes, except it's under a different class.


```python
episode_containers[0].find('span', class_='ipl-rating-star__total-votes').text
```
<br> 

### Episode description
For the description, we do the same thing we did for the airdate and just change the class.


```python
episode_containers[0].find('div', class_='item_description').text.strip()

```




    'An ex-lawyer is forced to return to community college to get a degree. However, he tries to use the skills he learned as a lawyer to get the answers to all his tests and pick up on a sexy woman in his Spanish class.'

<br> 

# Final code-- Putting it all together

Now that we know how to get each variable, we need to iterate for each episode and each season. This will require two `for` loops. The output will be a list that we will make into a pandas DataFrame. The comments in the code explain each step.


```python
# Initializing the series that the loop will populate
community_episodes = []

# For every season in the series
for sn in range(1,7):
    # Request from the server the content of the web page by using get(), and store the server’s response in the variable response
    response = get('https://www.imdb.com/title/tt1439629/episodes?season=' + str(sn))

    # Parse the content of the request with BeautifulSoup
    page_html = BeautifulSoup(response.text, 'html.parser')

    # Select all the episode containers from the season's page
    episode_containers = page_html.find_all('div', class_ = 'info')

    # For each episode in each season
    for episodes in episode_containers:
            # Get the info of each episode on the page
            season = sn
            episode_number = episodes.meta['content']
            title = episodes.a['title']
            airdate = episodes.find('div', class_='airdate').text.strip()
            rating = episodes.find('span', class_='ipl-rating-star__rating').text
            total_votes = episodes.find('span', class_='ipl-rating-star__total-votes').text
            desc = episodes.find('div', class_='item_description').text.strip()
            # Compiling the episode info
            episode_data = [season, episode_number, title, airdate, rating, total_votes, desc]

            # Append the episode info to the complete dataset
            community_episodes.append(episode_data)
```
<br> 

## Making the dataframe


```python
import pandas as pd 
community_episodes = pd.DataFrame(community_episodes, columns = ['season', 'episode_number', 'title', 'airdate', 'rating', 'total_votes', 'desc'])

community_episodes.head()
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
      <th>season</th>
      <th>episode_number</th>
      <th>title</th>
      <th>airdate</th>
      <th>rating</th>
      <th>total_votes</th>
      <th>desc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Pilot</td>
      <td>17 Sep. 2009</td>
      <td>7.8</td>
      <td>(3,187)</td>
      <td>An ex-lawyer is forced to return to community ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>Spanish 101</td>
      <td>24 Sep. 2009</td>
      <td>7.9</td>
      <td>(2,760)</td>
      <td>Jeff takes steps to ensure that Brita will be ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>Introduction to Film</td>
      <td>1 Oct. 2009</td>
      <td>8.3</td>
      <td>(2,696)</td>
      <td>Brita comes between Abed and his father when s...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>4</td>
      <td>Social Psychology</td>
      <td>8 Oct. 2009</td>
      <td>8.2</td>
      <td>(2,473)</td>
      <td>Jeff and Shirley bond by making fun of Britta'...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>5</td>
      <td>Advanced Criminal Law</td>
      <td>15 Oct. 2009</td>
      <td>7.9</td>
      <td>(2,375)</td>
      <td>Señor Chang is on the hunt for a cheater and t...</td>
    </tr>
  </tbody>
</table>
</div>

Looks good! Now we just need to clean up the data a bit.

<br> 

# Data Cleaning

## Converting the total votes count to numeric
First, we create a function that uses `replace()` to remove the ',' , '(', and ')' strings from `total_votes` so that we can make it numeric.


```python
def remove_str(votes):
    for r in ((',',''), ('(',''),(')','')):
        votes = votes.replace(*r)
        
    return votes
```

Now we apply the function, taking out the strings, then change the type to int using `astype()`


```python
community_episodes['total_votes'] = community_episodes.total_votes.apply(remove_str).astype(int)

community_episodes.head()
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
      <th>season</th>
      <th>episode_number</th>
      <th>title</th>
      <th>airdate</th>
      <th>rating</th>
      <th>total_votes</th>
      <th>desc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Pilot</td>
      <td>17 Sep. 2009</td>
      <td>7.8</td>
      <td>3187</td>
      <td>An ex-lawyer is forced to return to community ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>Spanish 101</td>
      <td>24 Sep. 2009</td>
      <td>7.9</td>
      <td>2760</td>
      <td>Jeff takes steps to ensure that Brita will be ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>Introduction to Film</td>
      <td>1 Oct. 2009</td>
      <td>8.3</td>
      <td>2696</td>
      <td>Brita comes between Abed and his father when s...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>4</td>
      <td>Social Psychology</td>
      <td>8 Oct. 2009</td>
      <td>8.2</td>
      <td>2473</td>
      <td>Jeff and Shirley bond by making fun of Britta'...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>5</td>
      <td>Advanced Criminal Law</td>
      <td>15 Oct. 2009</td>
      <td>7.9</td>
      <td>2375</td>
      <td>Señor Chang is on the hunt for a cheater and t...</td>
    </tr>
  </tbody>
</table>
</div>
<br> 

## Making rating numeric instead of a string


```python
community_episodes['rating'] = community_episodes.rating.astype(float)
```
<br> 

## Converting the airdate from string to datetime


```python
community_episodes['airdate'] = pd.to_datetime(community_episodes.airdate)

community_episodes.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 110 entries, 0 to 109
    Data columns (total 7 columns):
     #   Column          Non-Null Count  Dtype         
    ---  ------          --------------  -----         
     0   season          110 non-null    int64         
     1   episode_number  110 non-null    object        
     2   title           110 non-null    object        
     3   airdate         110 non-null    datetime64[ns]
     4   rating          110 non-null    float64       
     5   total_votes     110 non-null    int32         
     6   desc            110 non-null    object        
    dtypes: datetime64[ns](1), float64(1), int32(1), int64(1), object(3)
    memory usage: 5.7+ KB
    


```python
community_episodes.head()
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
      <th>season</th>
      <th>episode_number</th>
      <th>title</th>
      <th>airdate</th>
      <th>rating</th>
      <th>total_votes</th>
      <th>desc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Pilot</td>
      <td>2009-09-17</td>
      <td>7.8</td>
      <td>3187</td>
      <td>An ex-lawyer is forced to return to community ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>Spanish 101</td>
      <td>2009-09-24</td>
      <td>7.9</td>
      <td>2760</td>
      <td>Jeff takes steps to ensure that Brita will be ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>Introduction to Film</td>
      <td>2009-10-01</td>
      <td>8.3</td>
      <td>2696</td>
      <td>Brita comes between Abed and his father when s...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>4</td>
      <td>Social Psychology</td>
      <td>2009-10-08</td>
      <td>8.2</td>
      <td>2473</td>
      <td>Jeff and Shirley bond by making fun of Britta'...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>5</td>
      <td>Advanced Criminal Law</td>
      <td>2009-10-15</td>
      <td>7.9</td>
      <td>2375</td>
      <td>Señor Chang is on the hunt for a cheater and t...</td>
    </tr>
  </tbody>
</table>
</div>



Great! Now the data is tidy and ready for analysis/visualization.

Let's make sure we save it:


```python
community_episodes.to_csv('Community_Episodes_IMDb_Ratings.csv',index=False)
```

And that's it, I hope this was helpful! Feel free to comment or [DM me](https://twitter.com/_isabellamb) for any edits or questions.

The links for my github repository for this project and the final Community ratings dataset can be found in the links at the top of this page.

{{< figure src="community_header.jpg" title="" lightbox="true" >}}
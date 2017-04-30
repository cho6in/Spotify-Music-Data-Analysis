
## Project Introduction

In this project, we conducted data mining for 200000 tracks over the past 20 years, in order to analyze the trend of music industry development, and produce a predictive model for track popularity.


## Project Goals:

**Analyze the trend of music development over past 20 years.** 

  For example:
   
 ⋅⋅*Music has generally been louder than before?*
   
 ⋅⋅*What novel types of music have evolved popular in the past five years?*


**Establish models to predict track popularity by machine learning algorithms.**




## Data Extraction and Transformation

1. Spotify has provided amazing API resources:

   [Spotify API link](https://developer.spotify.com/web-api/track-endpoints/)

2. We randomly extracted data for 10000 tracks per year for the past 20 years.
```python
url = 'https://api.spotify.com/v1/search?q=year:'+ keywords +'&type=' + search_type +'&offset='+ off +'&limit=' + lim
requests.get(url).json()
```

3. Then acquire audio feature data by track_id; Access_token is required for this.

```python
url = 'https://api.spotify.com/v1/audio-features?ids=' + track_ids
requests.get(url, headers={"Authorization": access_token})
```


4. Vectorization of text (e.g. genres or name) by bag-of-words model

```python
vectorizer = CountVectorizer(analyzer='word',max_features=100)
WordVec = vectorizer.fit_transform(dicname[name]).toarray().tolist()
```

Then use pandas dataframe

Cleaned data like:


No location information
The information was pulled out from Spotify API and include: 
1. General numeric features (e.g. release time, popularity, artist popularity), 
2. Numeric physical properties (e.g. loudness, duration) 
3. Non-numeric ones (e.g. genres, album name, artist name)

One critical target variable is `track popularity`, which we used as indicator of popularity. It's provided by Spotify API, and calcuated by algorithms based on total number of plays the track has had and how recent those plays are.



### General pipeline and techniques:
```   
1. API extract and data snippet
2. Data clean and transform
3. Data visualization
4. Machine learning and modeling
```

### Result
### General trend of music over past 20 years

1. First, regardless of popularity, time series barplot for 16 different numeric features.
   Only loudness slightly change
   
   <p align="center">
   <img src="Figure/modified-boxplot-matrix.png" width="120%"/>
   </p>



### Popularity Analysis
### Association between track popularity and different numeric features.

1. What types of music do we listen these days?
   
   Barplot for number of different genres of tracks which are either popular or unpopular
   
   We define "popular songs" as those with track popularity score ranking at top 20 
 
   <p align="center">
   <img src="Figure/barplot-genres.png" width="80%"/>
   </p>
 
 


2. Barplot for number of different genres of tracks for the past four years. 

   
   <p align="center">
   <img src="Figure/stream-pop.png" width="80%"/>
   </p>

   <p align="center">
   <img src="Figure/stream-total.png" width="80%"/>
   </p>

3. Time-series analysis of popularity for different genres of music.

   <p align="center">
   <img src="Figure/year-type-popularity.png" width="80%"/>
   </p>



4. Which features are associated with track popularity? 
   Scatterplot between track popularity and features.
 
   <p align="center">
   <img src="Figure/modified-scatterplot-matrix.png" width="100%"/>
   </p>


5. Album popularity and artist popularity are two strong features linearly associated.
 
   <p align="center">
   <img src="Figure/album-artist-track.png" width="50%"/>
   </p>



### Modeling: Random Forest Regression
```
Before ML, correlation map for different features
```
   <p align="center">
   <img src="Figure/corr-map.png" width="80%"/>
   </p>

### Modeling: Random Forest Regression
```
1. xgbclassifier tune parameters
2. Which features are most predictive?
----MAKE wordle!
```

We define "popular songs" as those with track popularity score ranking at top 20 
 
   <p align="center">
   <img src="Figure/wordle.png" width="80%"/>
   </p>
 

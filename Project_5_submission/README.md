# Project 2:  Leveraging News and Media for Situational Awareness
> **BOS DSI-8:** Callie Bouzane, Sara Almeida, Marielle Marcus 
---

## Problem Statement 

The aim of this project is to provide the public with timely and relevant news updates during a major natural disaster.  Currently, there isn’t a central location for the affected community to receive and view updates.  In addition, updates come in from a variety of sources and contain various details, at times adding another layer of noise.  

This project will leverage the News API to gather articles from roughly 30,000 different sources to create a content-based recommender that can pull articles of particular interest to an individual.  Our hope is that this will not only be a centralized resource, but that it will also  reduce noise and tailor updates to the community’s needs. 

---

## The Process 

---

**Data Collection**

To train the content-based recommender, we used the News API, which is an API that returns JSON metadata for live headlines and articles from roughly 30,000 sources.  The data dictionary below outlines in detail the data returned.  We ultimately collected roughly 3,400 articles and filtered our collection so the API would only return articles containing he following terms:  heat wave, blizzard, tropical storm, earthquake, fires, hurricane, polar vortex, and tornado. 


**Data Dictionary**

| Feature | Description |
| --- | --- |
| Content | The content of the article | 
| Description | A summary of the article |
| Published At | Date the article was published | 
| Title | The title of the article |
| Source | The source of the article | 
| Author| The author of the news articles | 
| URL | The url to the article | 

**Limitations**

1. you can only access the first 100 articled per query
2. you can only pull from articles within the last month
3. there is a limited number of request per 24 hours  
4. source column was inaccurate - we corrected for this by extracting data from the url column, using Regular Expression (RegEx) 

**Model Summary**

We performed Natural Language Processing (NLP) data on the 3,400 articles using RegEx and TFIDF vectorizer so that it could be in a format that would allow for better feature extraction in our model.  We specifically vectorized the content, description, and title columns and chose TFIDF as the vectorizer since it would identify the distinguishing features of articles relative to others. 

We then used the TFIDF matrix to create our content-based recommender.  This recommender evaluated the relationship between articles using cosine similarity.  (The range of the cosine similar score is -1 to +1.)  A score closer to 1 represents a smaller ‘distance’ between the vectors for each individual article - i.e., the closer the score between two articles was to 1, the more likely they were to contain similar content.  

After entering an article title into the content based recommender, the model returns up to 10 ‘similar’ articles (defined here as the top 10 articles with cosine similarity scores of at least 0.40). 

---

## Conclusions 

While we were happy with our recommender and the data collected, there were challenges in using the free, public version of the API.  If we were to scale this up, we would want to upgrade to the paid version so that we could have a more up to date and higher volume of data.  This would allow this model to collect article in real-time, which is critical during a natural disaster.   


**Next Steps**

1. Add more news sources 
2. Create an app with the updated news, real-time
3. Introduce an interface where users can search in a Google-esque search engine to generate relevant articles


---

## Sources 


https://newsapi.org/

[https://www.datacamp.com/community/tutorials/recommender-systems-python?utm_source=adwords_ppc&utm_campaignid=1565261270&utm_adgroupid=67750485268&utm_device=c&utm_keyword=&utm_matchtype=b&utm_network=g&utm_adpostion=1t1&utm_creative=332661264371&utm_targetid=aud-522010995285:dsa-473406569915&utm_loc_interest_ms=&utm_loc_physical_ms=1018127&gclid=Cj0KCQjwyerpBRD9ARIsAH-ITn_LfMdHbYHake9SSueRPugpfzvuslA8sGTEwpScrvWdQ3hFQYFF1iEaAun-EALw_wcB\]

[https://www.datacamp.com/community/tutorials/wordcloud-python]

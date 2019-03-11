# EnviroNews

This project aims to model topics in environment news covered by various sources over several years. My goal here is to explore topics using unsupervised learning techniques and to assess their performance in detecting subtopics. These techniques include (1) matrix decomposition/factorization: e.g., NMF (Non-negative Matrix Factorization), LDA (Latent Dirichlet Allocation), PCA (Pricinpal Component Analysis) and (2) clustering algorithms (e.g., KMeans).

One critical assumption I made in this project was that each article can only be described by one topic, so one-hot encoding was used to categorize the articles. In reality, an article may touch upon many topics, and this nuance can certainly be captured by the model. However, this project focuses less on the subtlety of the topics but instead on the amount of coverage different news sources gave to these topics. As a result, this simplication made comparison between sources much easier.

## Data Sources & Storage

I obtained full-text articles from NYTimes and Fox News to compare their coverage with each other. NYTimes was seleted specifically for its extensively developed [API](https://developer.nytimes.com/docs/articlesearch-product/1/overview) and Fox News due to it being a good comparison point to NYTimes. Additionally, I used [NewsAPI](https://newsapi.org/) to get articles from a plethora of sources up to 1 month old ([free plan](https://newsapi.org/pricing)). Results of this project are displayed as an [interactive Tableau dashboard](https://public.tableau.com/profile/khoa.lam#!/vizhome/NYT_2/README) in 3 tabs: (1) evolution of environmental topics in NYTimes over 16 years, (2) comparison between NYTimes vs. Fox News, and (3) topics distribution in articles obtained by NewsAPI.

The full-text articles are stored in MongoDB on an AWS-EC2 instance. MongoDB is a NoSQL database and uses JSON-like documents and syntax. As there is no definite data structure between NewsAPI output, Fox News website, and NYTimes API output, in addition to the long-form nature of full-text articles, MongoDB was selected to work with unstructured data and the articles are stored on an AWS-EC2 instance due to large file size. The [CSVs in this GitHub](./urls-data/) only consists of the urls for the articles:

1. NYTimes: 13654 articles (08/2002-07/2018)
2. Fox News: 3132 articles (09/2012-08/2018)
3. NYTimes/Fox News subset (same time frame): 6876 articles (09/2012-08/2018)
4. NewsAPI (various sources): 20628 articles (09/2017-08/2018)

## Notes

This project consists of three parts:

1. Getting URLs for environment-related articles (codes available [here](./code/url-codes))
2. Downloading full-text articles from URLs using [newspaper API](https://newspaper.readthedocs.io/en/latest/) and storing them on MongoDB on an AWS-EC2 instance
3. Using NLP techniques to model topics
4. Integrating modeling data into Tableau for visualization and comparison

Python packages required: pandas, numpy, seaborn, matplotlib, sklearn, pymongo
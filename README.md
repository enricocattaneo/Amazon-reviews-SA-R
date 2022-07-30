# Sentiment Analysis of Amazon Reviews 
## For the book: “Fiesta: The Sun Also  Rises (Arrow Classic)" by Ernest Hemingway.


## Table of Contents

- [Project Overview](#projectoverview)
- [Data Description](#datadescription)
- [Technical Overview](#technicaloverview)
- [Results](#results)

***

<a id='projectoverview'></a>
## Project Overview

Our initial purpose is to scrape relevant information about Amazon products, including product details, reviews, and ratings. 
We construct two scraping functions that take as input an URL and will return a tibble with the product information. The first function scrapes the product's general info (product details, number of customer ratings, and the fastest delivery date). In contrast, the second one scrapes the reviews' titles, texts, and related stars. 
The product details are displayed on a single page, so our function needs to input only the product's ID. Instead, since the reviews are organized on multiple pages, the function will need not only the product ID but also the number and "position" of the pages from which we want to scrape. The reviews are divided into "Reviews from the UK" and "Other countries." 
For this analysis, we chose a book called "Fiesta: The Sun Also Rises (Arrow Classic)" by Ernest Hemingway.
This analysis's main objective is to understand the meaning behind reviews' comments better and compare it to star ratings. In order to do so, we will conduct a dictionary-based sentiment analysis using three different lexicons (BING, AFINN, NRC).


<a id='datadescription'></a>
## Data Description

The scraped review data contains 300 observations, including the title, text, and related star ratings (from 1 to 5) of each book's review. 
By conducting a preliminary EDA, we observe the number of reviews divided by star rating.![rev_by_star](https://user-images.githubusercontent.com/80990030/181917797-d29e8ed0-fb3e-42a3-9e23-7ac7c4e7a73a.png) We also consider the difference in the reviews' length between positive (>= 4 stars) and negative reviews (<4 stars).![nchar](https://user-images.githubusercontent.com/80990030/181917809-f5d72698-f582-4cb0-9f13-81ad236d5cda.png)

<a id='technicaloverview'></a>
## Technical Overview

The project has been divided into various steps which include:
#### Data Cleaning and Pre-Processing 
* Language Detection: select only the English-written reviews, so we do not have to translate the non-English ones (end up with 242 observations out of the starting 300). 
* Data tokenization: extracting the words in the reviews' text. 
* Cleaning the tokenized data:  eliminate custom stop-words (common words irrelevant to our analysis), digits, and punctuation. This step permits a more accessible and precise analysis. 
* Word normalization: we use Stemming which is the process of reducing the word to its root and eliminating the suffix (Lemmatization could be an alternative approach). 


It is essential to keep in mind that all the choices made in this pre-processing and cleaning phase impact the final output of the analysis.

#### Dictionary-Based Sentiment Analysis 

In this analysis we use two different approaches: 
* Tidytext approach.
* Udpipe approach.

With the Tidytext approach, we consider each word independently and separately from others. Instead, when using the Udpipe approach, we can also account for polarity negators and amplifiers positionally close to a term (the performance usually increases).

For both approaches we also consider three different lexicons: 
* BING (gives words a positive or negative sentiment).
* AFINN (rates words with a value from -5 to +5).
* NRC (labels  words  with  six  possible  sentiments  or  emotions). 

The procedure for each of these lexicons is similar, but the results depend on the lexicon itself. With every specific lexicon, we can give a sentiment or value to (almost) each word. Then we compute the value of each review as an aggregation of the contained words' values/sentiment. We compare the sentiment distributions considering each lexicon and analyze every word's contribution to the sentiment using bar charts and word clouds. 

<a id='results'></a>
## Results

The reviews are primarily positive, which we knew from the start. However, it is crucial to notice how different choices and approaches can bring different results. Moreover, such an analysis can be conducted from multiple and different perspectives. 
The main result of our analysis was to highlight the similarities and differences that arise from the analysis choices, not only when considering the approach or lexicon but also in the pre-processing and cleaning phase.


The analysis and resulting visualizations are in the R Notebook and HTML file. At the same time, `Report.pdf` contains comments and observations on the analysis and its results.

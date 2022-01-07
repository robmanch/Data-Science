# Objective
The goal is to extract stock symbols present in the news of www.prnewswire.com,  then, the Yahoo Finance service will be queried to find the Close Prices and Volume of the last 10 days. Moreover, The code will continue scanning on the background for new symbols at the specified time interval.

## Introduction
A python module was created in order to perform the specific tasks of the assignment, including:
- Periodically scanning and parsing news from https://www.prnewswire.com/news-releases/news-releases-list/
- Searching the content of the news to find a stock symbol TSX.
- Keeping track on a file of the number of occurrences of each symbol.
- Using Matplotlib to create visualizations of the volume and closing price of every stock symbol.

Additionally, our solution employs a scheduler which search for new content and symbols in the background at the specified intervals.

## Coding Strategies

- Overall structure: A separate module was created for the tasks for parsing the news, retrieving stock symbols and showing the graphs. A scheduler keeps fetching more news and symbols at specific intervals.

![image](https://user-images.githubusercontent.com/62516990/148603422-6433b626-4d91-4bd3-b490-e8015b7448fa.png)

- <b>Scheduler</b>: Schedule library is used to scan the website periodically.

![image](https://user-images.githubusercontent.com/62516990/148603565-8685fa02-cf0c-4336-95f5-77e48d6936a3.png)

- <b>News parsing</b>: The library Beautiful Soup was employed for the job of fetching and traversing the web site:
1. First, we navigate to the specific HTML container with the list of news by CSS class selector
2. Then we extract the title and summary/paragraph of the each new in the current page
3. We add the results to a dictionary for future use.

![image](https://user-images.githubusercontent.com/62516990/148603689-20ed96a6-5c79-473a-966c-9c74deb65218.png)

- <b>Saving the parsed news</b>: Dictionary with headlines and paragraphs is converted to data frame with pandas library.

![image](https://user-images.githubusercontent.com/62516990/148603787-1f78774b-ad1a-4a3e-99c0-7dad15f7145e.png)

- <b>Symbol retrieval</b>: stock symbols were extracted from the articles’ paragraphs by extracting the text inside the tokens (TSX:**)

![image](https://user-images.githubusercontent.com/62516990/148603862-306e32e3-8b3e-4dfd-aeb1-78c857c6fb85.png)

- Saving the symbols with their occurrence frequencies

![image](https://user-images.githubusercontent.com/62516990/148603903-9020eb63-24be-448b-9906-cdb9902d5174.png)

- <b>Extracting stock market data and plotting results</b>:
1. The package yfinance was used to query the Yahoo API and get each symbol stock history
2. We took only the last 10 days.
3. Finally, we plot the Volume and Closing Price information using matplotlib.

![image](https://user-images.githubusercontent.com/62516990/148603986-036e2fd9-4476-400a-a5ad-94d86b65f253.png)

## Plots for Close Price and Volume

<b>Agnico Eagle Mines Limited (AEM)</b>
Canadian Mining company

![image](https://user-images.githubusercontent.com/62516990/148604088-0548ba78-43ec-4eb3-8747-e6f505083c79.png)

## Conclusions
- Our module is able to scan and parse news from the newswire website, extracting headline and paragraph
- Stock symbols were searched into the parsed news
- Symbol frequency was calculated
- Plotted symbols found by Yahoo Finance.
- Plotted the Volume data and Close data

<b> Computational efficiencies</b>:
- A set instead of a list was used to save memory and discard duplicated news between different scans. 
- A scheduler and a sleep call were used rather than an infinite loop to save CPU time.
- To get most of the symbols from the website, on the first run, pages from 2 to 8 are retrieved by the scanner. Later, first two pages are retrieved. 



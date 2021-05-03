# WebscraperRepo

* __Please open webscraper_eb.ipynb in JupyterLab before attempting to navigate it using the internal links, they will not work in GitHub__
* Repository housing a Jupyter Notebook which leverages the PRAW Python package in order to scrape [Reddit](https://www.reddit.com/) data

# How to use:

* Load webscraper_eb.ipynb __as well as the 3 pngs__ into a JupyterLab environment. From there, follow the instructions contained within the cells of webscraper_eb.ipynb
# Reddit - Why?

* "Reddit is a social news platform that allows users to discuss and vote on content that other users have submitted. there are small communities called subReddits that bring people and their interests together."
* In this particular Jupyter Notebook I am scraping title data from the subReddit [r/CryptoMoonShots](https://www.reddit.com/r/CryptoMoonShots/) in order to try and determine the most frequently mentioned cryptocurrency in the first 350 "hot" posts

# How are hot posts determined?
* "hot" posts on a subReddit are determined by taking the log10 of the score and weighing it against 12 hour periods. i.e. to keep the same place, a post must increase its score by x10 every 12 hours.

# Why this subReddit?
* [r/CryptoMoonShots](https://www.reddit.com/r/CryptoMoonShots/) works well because the _majority_ of users include the ticker symbol for the cryptocurrency they have made their post about preceded by a "$", giving us something to actually look for. Sure, it's easy enough finding the most frequently occurring words within the first X number of hot posts, but finding the most frequently occurring _cryptocurrencies_ mentioned is more difficult. This is why I did not choose a larger cryptocurrency subReddit with a broader range of post topics e.g. [r/CryptoCurrency](https://www.reddit.com/r/CryptoCurrency/)

# How the code works:
* After X hot posts are iterated through in the desired subReddit and the post's titles are loaded into a list, the post titles are split into their individual words
* Next, the number of times each word is mentioned is calculated, this information is then stored in a key-value pair dictionary:       
  key = word from title       
  value = number of occurrences of word     

* As previously mentioned, to check what words in these post titles are cryptocurrencies the first element of the String is checked - if it is not "$", it is removed from the dictionary (This is not failsafe, [more on this later](#flies-in-the-ointment))
* The top 10 remaining dictionary posts are then graphed as a bar chart:       
  x = name of cryptocurrency       
  y = number of occurrences of the word within X "hot" post titles

# Flies in the ointment:
* One shortcoming of the code currently is that by keeping words from hot posts that start with "$", sometimes certain Strings are kept which are not cryptocurrencies - e.g. several post titles might have the String "$1M" in it, therefore this could end up being graphed.
* On the flip side of this coin, not all contributers to this subReddit precede the ticker symbol of the cryptocurrency they are talking about with "$" in post titles, this is solely a general rule of thumb. Therefore, there is a chance that many "hot" posts reference one cryptocurrency e.g. "IFP", but if this isn't written as "$IFP" in the posts it will not be in the count.

# Possible remedies to the above problems:
* Instead of removing words from the dictionary which do not begin with "$", keep all words, and their count
* [CoinGecko](https://www.coingecko.com/en) - the world's largest independent cryptocurrency data aggregator - has an open API:       
  ```Python
  pip install pycoingecko
  from pycoingecko import CoinGeckoAPI
  cg = CoinGeckoAPI()
  ```
*  Search for each word in the dictionary on CoinGecko. If it exists as a token, don't remove it from the dictionary       
   If it doesn't exist as a token, remove it.        
*  Hypothetically this would prevent the removal of words which are cryptocurrencies but are not preceded with $ like currently, and it would also correctly remove words which shouldn't be there but slip through the cracks, e.g. "$1M"
   

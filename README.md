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

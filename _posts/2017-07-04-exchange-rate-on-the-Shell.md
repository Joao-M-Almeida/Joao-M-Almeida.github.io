---
layout: post
title: Exchange Rate on the Shell
tldr: I've made a small python script to fetch some useful information about currency exchange rates and display it when opening a shell.
---


## __TL;DR__

I've made a small python script to fetch some useful information about currency exchange rates and display it when opening a shell.

Check it out [here](https://gist.github.com/Joao-M-Almeida/5dcb9be460f9f4ef8c3cf76f48842dbe).

---------

## The idea

Due to being paid in Swiss Francs, but spending mostly Euros, I have been paying close attention on the CHF-EUR exchange rate.
Since finishing my master thesis I was also looking for ways to practice my Python, as I'm working with Java at work.
I thought a simple script to fetch exchange rate information and to display it on the shell would be a fun and small project.

## The code
All the code is available on my Github, it's very simple and could definitely be made more generic and reusable.
For now it serves its purpose.

### The Data
For this I was interested in the closing exchange rate for the last year or so and the most update rate I could get.
Most API's I found relied on [the ECB](http://www.ecb.europa.eu/stats/policy_and_exchange_rates/euro_reference_exchange_rates/html/index.en.html) for their historical data, so I opted for one of them, [Fixer](http://fixer.io/), which was pretty simple to use.
For the most update currency data, I'm using [exchangerate-api](https://www.exchangerate-api.com/) which allows me to do 1000 requests per month which is more than enough for me.

### A Cache
Because I would be doing a request per data of data I decided it would be better to have a cache to avoid having to wait too long when starting my shell.
I went for the simplest solution I thought of, just using [Pickle](https://docs.python.org/3/library/pickle.html) to store a dictionary with the rate for each day.

### Code structure
The code is structured in the following way:

1. Load or create the cache if it doesn't exist;
2. Fetch all the exchange rates from the past year, if they don't exist in the cache;
3. Save the cache;
4. Transform the cache into a pandas DataFrame;
5. Calculate statistics on the data, in this case: _average_, _median_, _maximum_ and _minimum_;
6. Print it on the screen;
<!-- ### Code improvements -->



## Future
I have some more ideas on some extra analyzes that could be done on top of this data and some other types of data that would be interesting to look at.
For instance looking into moving averages and trying to recommend when should I exchange money from CHF to EUR or incorporating news data about the EU or Swiss economy.

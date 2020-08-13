---
layout: post
title:      "Final Project - Stock Market App"
date:       2020-08-13 22:02:49 +0000
permalink:  final_project_-_stock_market_app
---


My final project with Flatiron Academy is almost done!  I'm happy to say that I've learned a ton and really enjoyed the learning experience at Flatiron.

My fifth and final project is based on Ruby on Rails and JavaScript including  the JavaScript Frameworks React and Redux.  I have to say that working with these frameworks was tricky, but has been a fun challenge.

My project is a stock market app that gets company and stock data from an API provided by https://finnhub.io.  I'm able to display candlestick stock charts based on this data with an excellent library from https://amcharts.com.  If you need heat maps, charts, or other dynamic graphics, I definitely liked using AmCharts.

My app is based on the following problem and solution:

* Problem: Most stock apps use standard time periods (day, week, month, year) to view stock price trends.  This can make it difficult to spot and track price movement over short term periods.

* Solution: Allow the user to view candlestick charts over custom time periods, create and maintain watchlists, and view stock price data over a user specified three day period.

Features include:
* Easily create an account with name, email address, and password.
* Passwords are encrypted using bcrypt.
* Enter stock ticker or enter company name and select from list.
* View company data and candlestick stock chart for user specified time period.
* Create and save multiple "watchlists" to quickly view stock data.
* Daily View (list of multiple stocks on one page): 1. Select watchlist; 2. Specify custom three day period; 3. Get a table with closing stock price and movement for each day; 4. See every stock in your specified watchlist.

This project was very challenging and I had no shortage of difficulties to overcome.  Following is a list of some of my challenges and how I solved them:

Handling Deeply Nested Models / Data:

My `Company` model has many `charts` that in turn have many `chart_lines`.  I was using the `active_model_serializers` GEM in Rails, but this will only render data one level deep (`Company -> charts`).  After some research I found a solution that returned data from all three levels:

1. Create a file called `active_model_serializer.rb` in the initializers folder.
2. Add the code `ActiveModelSerializers.config.default_includes = '**'`.

This code tells the serializer to include all nested levels in the return data.  Note that this solution isn't always a good idea as it can cause infinite looping errors, but it did work great for me.

Challenge with Dates:

The Finnhub API requires dates to be in Unix Timestamp format while the HTML date picker provides dates in a string format.  JavaScript has a great function to get the UTC timestamp from a string: `Date.parse()`.  What I didn't realize at first is this is the number of **milliseconds** from Jan 1st, 1970 while Unix is the number of **seconds**.  Once I realized this, all I had to do is divide the UTC timestamp by 1,000.  However, I got some really interesting data and errors before I figured this out.  One of many tricky challenges we deal with in development!

Handling Charts:

The charts from AmCharts worked great, but I did have one challenge.  My blank chart would render before the data was received (due to the asynchronous fetch functionality).  However, once the data was received, the React Framework didn't recognize the new chart as a state update so it would not re-render the chart with the data.  This is where the `React Lifecycle Hooks` came in really handy.

What I did is render the initial blank chart using the `componentDidMount()` event.  Then I used the `componentDidUpdate()` event to compare the previous chart props to the new chart props with data.  If different, I invoked the function to build a new chart.  AmCharts has great documentation, but they assume the data is already present when the chart is first created.

Handling Multiple Asynchronous Fetches:

The Daily View in my app requires that I fetch data for multiple companies from the Finnhub API.  This was one of my biggest challenges due to the asynchronous nature of these fetches.  I used an example solution from online to create an `async function` called by a `reduce function` that enabled me to collect data from multiple API calls before passing this data to Rails.  The way this worked is as follows:

1. Start with an object that includes the stock symbols I need:
`companies`

2. Loop through the list of company objects to get an array of stock symbols:
`.map(company => company.ticker)`

3. Call `.reduce` on the array with a callback to an async function also passing a `Promise` to the callback:
`.reduce(chainedFetchData, Promise.resolve({}))`

The chainedFetchData function:
```
async function chainedFetchData(p, ticker) {
            
const companyObj = await p
const companyData = await fetchData(ticker)
const chartData = await fetchChart(ticker)
return {...companyObj, [ticker]: {companyData: companyData, chartData: chartData}
 }
```

4. Once the `.reduce` function has looped through the array of stock symbols and the callback function has returned an object that includes all of the data, only then do I invoke the function to pass the object to Rails.
`.then(dailyData => databaseFetch(dailyData))`

I learned a lot researching and overcoming these challenges.  I'm excited to be finishing up with Flatiron Academy in the coming weeks and start applying my knowledge and learning in a web development career!

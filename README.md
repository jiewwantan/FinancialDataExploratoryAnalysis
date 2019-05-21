# FinancialDataExploratoryAnalysis

### by Jiew Wan Tan
### 19th June 2016

Financial Data exploratory analysis using R: Distribution, time-series analysis, bivariate exploration of various features, correlation matrix, risk sentiments and behavior for different asset class.

This project explores the behavior and inter-relationships among different financial assets and indices. All data are time series data.

Financial and economic data are abundant and up-to-date. Correlations, causation and any form of relationships among indices, asset classes and instruments have always exist. As much as the complexity of the relationships are fascinating for data analysis, they are constantly in flux too as market condition change. It makes them challenging as well as irresistable to study. Financial time series are available from as short as 1 minute period. For uniformity, this exercise adopt daily time series and they are compiled into a csv file: dollar.csv, from 4th Jan 1995 to the second week of June 2016, a 20 years period. Since not all markets the assets trade in are open everyday (some markets open while the other are closed), we will see missing values among the datasets. In this case, they are omitted.

We are looking at dollar index, S&P500 index, gold, brent oil, treasury bonds at different maturities, LIBOR at different maturites, effective Fed fund rate, interest rate spreads and volatility index. Please note that treasury bond and T-bill are used interchangeably throughout this report, they actually mean the same instrument type.

Ther purpose in this exploration is the understand relationships. If the exploration found useful relationships, it can be used to generate actionable trading signal for algorithmic trading. For this reason, we are particularly interested in dollar Index and the Standard & Poor 500 index (S&P500) as there are easily a few popular instruments derived from these indices.

The function to calculate and display correlation coefficient on the plots: 

1. Data loading, all data are cleaned and saved in a file: dollar.csv. 
2. Convert date field to date format readable by R. 
3. Setting the range of date to explore. 
4. Summary of data. 

## Distribution & Time Series Characteristics for Dollar Index
The dollar index has been ranging between 80 to 140 over the past twenty year. Now hovering around 121, it is on the higher end of the range. From the historgram, it has a weak binomial distribution. So it is commonly seen to be ranging around 100 and 120. Its uptrend pathway is generally steeper than downtrend. The last 8 years has seen 2 uptrends that lasted 2-3 years, whereas the the uptrend before that took about 7 years. The 3 uptrends happened during the late nineties, the late 2000s and the early to mid 2010s. 
In all following historgrams, means are marked with red lines, 25% and 75% quantiles are marked with yellow lines. 

[image1]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/dollar_index.png"Distribution & Time Series Characteristics for Dollar Index"
![Distribution & Time Series Characteristics for Dollar Index][image1]

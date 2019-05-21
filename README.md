# Financial Data Exploratory Analysis

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

[image1]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/dollar_index.png "Distribution & Time Series Characteristics for Dollar Index"
![Distribution & Time Series Characteristics for Dollar Index][image1]

## Distribution & Time Series Characteristics for S&P500

The S&P500 index has a normal distribution. We can observe that at some point of time, the dollar index correlates with the S&P500. In most other time, it propably relates more to other factors. The attraction of capital to the US capital market, part of it contributed by the stock markets (which the S&P500 tracks) should also contributes to USD demand and hence its uptrend. Though, this correlation could be hard to catch and both the dollar and stock markets are huge market with global participants’ interactions. There are just too many causations in their movements. The major causes are trade and capital flow, central banker’s manupulations. Naturally, when most participants are driving on the same cause at the same period, a trend is set for years. 

[image2]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/S%26P500_index.png "Distribution & Time Series Characteristics for S&P500"
![Distribution & Time Series Characteristics for S&P500][image2]

## Distribution & Time Series Characteristics for effective Fed fund rate

The EFFR has an unnatural, somewhat skewed distribution. We notice a large number of distribution concentrates in the 0.xx region. This is an unnatural cause of Federal reserve massive quantitative easing program that suppress interest rate at 0.25-0.5 since the subprime financial crisis in 2008. However, it is expected to move gradually.

[image3]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/EFFR.png "Distribution & Time Series Characteristics for effective Fed fund rate"
![Distribution & Time Series Characteristics for effective Fed fund rate][image3]

## Distribution & Time Series Characteristics for Gold

Gold is considered a commodity as well as a safe haven asset. It has enjoyed a long period of uptrend when interest rates have been set to exceptionally low. Sometime in early 2013, market has expectation for Fed to raise interest rate, as such the begin of gold downtrend. In the recent months, despite the backdrop of Fed’s rate rise, negative interest rates are seen in major economies such as Europe and Japan while emerging markets growth weakens. Gold has seen revival due to its safe asset status. So we can assume that gold has a negative correlation with interest rates and a positive correlation with risk sentiment. 

[image4]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/gold.png "Distribution & Time Series Characteristics for Gold"
![Distribution & Time Series Characteristics for Gold][image4]

## Distribution & Time Series Characteristics for Brent Crude oil

Oil is a commodity asset. What contributes to its price are more on political, economical and environmental factors. Its histogram is somewhat skewed. the past ten years has been extremely volatile for oil.

[image5]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/BrentCrudeoil.png "Distribution & Time Series Characteristics for Brent Crude oil"
![Distribution & Time Series Characteristics for Brent Crude oil][image5]

## Distribution Characteristics for VIX, High yield bond spread and TED Spread

VIX is an Index, TED spread is the difference between interbank loan interest rate and short term T-bill rate, High yield spread is the rates difference between risky and low risk bonds. All can be used as gauge for risk sentiment. The skewed histograms shows that most of the time , market sentiment is calm with occassional risk aversion sentiment. 

[image6]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/VIX_TED.png "Distribution Characteristics for VIX, High yield bond spread and TED Spread"
![Distribution Characteristics for VIX, High yield bond spread and TED Spread][image6]

## Distribution Characteristics for LIBORs

From both LIBORs and Treasury bonds’ histograms, we observed that the longer maturity bonds are less skewed and more normal. The shorter term bonds’ histograms look more similar to effective Fed fund rate’s histogram (see above). We can attribute this to the power of Federal Reserve’s market manupulation on short term interest rate, with its ultimate goal to encourage bank lending to stimulate economy. The longer term bonds are less affected by it and more by market force. 

[image7]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/dist_libor.png "Distribution Characteristics for LIBORs"
![Distribution Characteristics for LIBORs][image7]

## Distribution Characteristics for Treasure Bonds

[image8]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/dist_TreasureBonds.png "Distribution Characteristics for Treasure Bonds"
![Distribution Characteristics for Treasure Bonds][image8]

## Bivariate exploration of various features: Scatter plot

We are experimenting S&P 500 and Dollar index’s relationship with other features, to see if we can find any interesting correlation. As for treasury bond and LIBOR, we select a few commonly use maturities from each set.

All scatter plots will be fitted with linear regression or loess lines with confidence internals. When a linear association is observed, a linear regression line is plotted. If the scatter plot shows a non-linear and more complicated relationship, a loess line will be plotted instead. Correlation coefficients will also be included in all plots. The complex relationships observed in most plots reflects that the plots deserve further investigation in a different study.

[image9]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/BivariateScatter%20plot.png "Bivariate exploration of various features: Scatter plot"
![Bivariate exploration of various features: Scatter plot][image9]

## Bivariate exploration of interest rate spreads: Scatter plot

[image10]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/BivariateExplorationInterestRateSpreadsScatter%20plot.png "Bivariate exploration of interest rate spreads: Scatter plot"
![Bivariate exploration of interest rate spreads: Scatter plot][image10]

## Bivariate exploration of gold: Scatter plot

Gold and oil, in contrast have strong negative correlation with most other assets, espciallly interest rate. Gold is viewed a safe haven in the market, during the time of market stress, together with treasury bonds, gold price will be bid up by investor rushing for safety. When bond price is up, causing its yield to drop (a fixed interest rate bond’s yield will be less attractive when it price goes up), as such gold price is highy correlated with bond price and has strong negative correlation with bond yield. Before we proceed further to investigate risk and interest rate-related assets , let’s look at gold price behavior with 3 assets: 

[image11]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/BivariateExplorationGoldScatter.png "Bivariate exploration of gold: Scatter plot"
![Bivariate exploration of gold: Scatter plot][image11]

## Correlation Matrix: An Overview

Since we have many features, a correlation matrix will be handy. We notice that the two features: S&P 500 and dollar index we are studying here do not have obvious correlationship with most other assets. Particularly dollar, that imply its complexity with other assets in the markets.

[image12]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/CorrelationMatrix.png "Correlation Matrix: An Overview"
![Correlation Matrix: An Overview][image12]

## VIX in Dollar Index and S&P500 distribution: Histogram

Volatity index (VIX) is known to be the fear index. When market is fearful, the VIX reflects that. VIX is currently moving between mid to late teens, not particularly fearful. It is when it has gone above 30. From the histograms below, we can tell most of the time the markets are not fearful. Though, as we see from S&P0500’s histogram, markets are fearful when they are at the lower end: < 1000 and between 105 to 113 for dollar index. 

[image13]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/VIXDollarIndexS%26P500Histogram.png "VIX in Dollar Index and S&P500 distribution: Histogram"
![VIX in Dollar Index and S&P500 distribution: Histogram][image13]

## VIX in Dollar Index and S&P500 distribution: Scatter plot

The scatterplots show Dollar index & S&P500 relationships with VIX. There are weak positive (dollar) and weak negative correlations (S&P500). 

[image14]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/VIXDollarIndexS%26P500Scatterplot.png "VIX in Dollar Index and S&P500 distribution: Scatter plot"
![VIX in Dollar Index and S&P500 distribution: Scatter plot][image14]

## Dollar Index & S&P500 behavior in risk sentiment

TED spread is the difference between the interest rates on interbank loans and on short-term U.S. government debt (“T-bills”). It can be used as a gauge of risk sentiments. (See note) From the scatterplots, we notice that when VIX is high, TED spread tends to be high too.

Note: TED is an acronym formed from T-Bill and ED (Eurodollar, LIBOR), the ticker symbol for the Eurodollar futures contract. TED spread is the difference between the three-month LIBOR and the three-month T-bill interest rate. The TED spread is an indicator of perceived credit risk in the general economy,since T-bills are considered risk-free while LIBOR reflects the credit risk of lending to commercial banks. An increase in the TED spread is a sign that lenders believe the risk of default on interbank loans (also known as counterparty risk) is increasing. Interbank lenders, therefore, demand a higher rate of interest, or accept lower returns on safe investments such as T-bills. When the risk of bank defaults is considered to be decreasing, the TED spread decreases. 

[image15]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/DollarIndexS%26P500behaviorRiskSentiment.png "Dollar Index & S&P500 behavior in risk sentiment"
![Dollar Index & S&P500 behavior in risk sentiment][image15]

## Correlations of risk sentiment indicators

We know that risk sentiments plays a significant part in market behavior, the analysis thus far has shown how it is reflected in different asset class. We progress further by adding a variable into the bivariate plots, making multi-variate analysis. First, by reaffirming it with three risk indicator behave with each other. See notes about high yield bond spread: https://research.stlouisfed.org/fred2/series/BAMLH0A0HYM2 for further info about high yield bond spread.

We notice from all three scatter plots that VIX, TED Spread & high yield bond spread are very much correlated. Their indiviual line charts also show that they spiked up around the same period, or better say they response to market sentiment similarly. 

[image16]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/CorrelationsRiskSentimentIndicators.png "Correlations of risk sentiment indicators"
![Correlations of risk sentiment indicators][image16]

## More on other asset classes behavior with VIX

We notice that dollar has negative correlationships with gold and oil. That makes sense as both are denominated by dollar. When dollar goes up, they have to go down. However, there seems to be more between Dollar and gold. 
Dollar and effective Fed fund rate (EFFR) has mild correlation as EFFR is somewhat manipulated by Federal Reserves (the United States’ central bank). 
S&P500 is inversely correlated to High yield bond spread, this explains the stock market is down when risk sentiment is high, VIX color in the plot reaffirms that too. 
The dollar index has a non linear association with high yield spread, which probably worth looking further into an equation that explains their relationship. VIX’s behavior in them is mixed. 
The dollar index and S&P 500 looks to have a very complicated relationship. It will take some quantative analysis work to derive a method to explain it.

[image17]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/MoreonotherAssetClassesBehaviorwithVIX.png "More on other asset classes behavior with VIX"
![More on other asset classes behavior with VIX][image17]

## Characteristics of fixed income assets (bonds) of different maturities

The plots reveals that interest rate, their spread among short and long term maturities plays a part in risk sentiment. They have also shown coherent and consistent behavior from the plots above. Given market is very much affected by risk sentiment, we should see if these can help predict movement of S&P500 and the dollar.

Having looked at how risk sentiment plays out in different asset classes, we now look into how it is reflected in treasuries and LIBORs of varied maturities or better how bonds and LIBORs reflect that. Treasury bonds are viewed as a safe asset (risk free assets) in the market. When risk sentiment is high or imminent, the bonds market is likely the earliest to reflect that as investors rush for safe havens. When demand bids up bond price, naturally, their yields drop. LIBORs are interbank rates: borrowing between banks. When interbank borrowing market is stressed, the banks wil bid up LIBOR rates. We can observe form the boxplot that longer maturity bonds tend to have higher yields, and that shorter maturity bonds tend to be more volatile. The one month treasury bond even has a bunch of outliers.

[image18]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/CharacteristicsFixedIncomeAssetsBondsofDifferentMaturities.png "Characteristics of fixed income assets (bonds) of different maturities"
![Characteristics of fixed income assets (bonds) of different maturities][image18]

## Behavior of LIBOR and Treasury of the same maturity

Following the findings on risk, rates and spread, we sum it up by looking at TED Spread in action: how LIBOR and Treasury bond of the same matuirties relate to each other and together their response to risk sentiment.

We observe that LIBORs and treasury bonds are very correlated at all 4 shared maturities, when their rates go to the upper end, market tends to be in above average stress, moderately high risk sentiment. It is the extreme stressful market condition that distort their correlationship, LIBOR rates went high while treasury bonds stick to their lowest range, particularly the shorter maturity bonds. This very much explains the characteristic difference between LIBOR and treasury markets mentioned above.

This is an important finding so far in this exploration. When trader see a tendency of bond rates of the same maturity diversify from each other and both rates are not at their high end, the trader should take note. Though this finding has to be complimented by another perspective: time. Because it is enough to know the correlation and distribution. We should know who is leading and who is lagging to have an actionable signal in trading.

[image19]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/BehaviorLIBORandTreasurySameMaturity.png "Behavior of LIBOR and Treasury of the same maturity"
![Behavior of LIBOR and Treasury of the same maturity][image19]

## Treasury bonds from 1995- Present

An overview of how treasury bonds trend over the years. 

[image20]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/TreasuryBondsFrom1995-Present.png "Treasury bonds from 1995- Present"
![Treasury bonds from 1995- Present][image20]

## LIBORS from 1995-Present

An overview of how LIBORs trend over the years. 

[image21]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/LIBORSFrom1995-Present.png "LIBORS from 1995-Present"
![LIBORS from 1995-Present][image21]

## LIBOR-T- bill spreads from 1995-Present

An overview of how LIBORs and treasury bills spreads (LIROR rate - treasury bill rate) trend over the years. The 3 month spread is actual TED spread. This plot is the time series plot for Final Plot 1: Behavior of LIBOR and Treasury of the same maturity. 

[image22]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/LIBOR-T-billSpreadsFrom1995-Present.png "LIBOR-T- bill spreads from 1995-Present"
![LIBOR-T- bill spreads from 1995-Present][image22]

## Behavior of Treasury bonds vs VIX
The 1995-present time series capture the two major financial crisis: the internet bubble in the late nineties - early 2000s and the 2008 subprime financial crisis. We can see that T-bills started to behave unusually(the spreads between short and long term yield became very narrow) much earlier than before the market became panic (when VIX spikes up).

[image23]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/BehaviorofTreasuryBondsVsVIX.png "Behavior of Treasury bonds vs VIX"
![Behavior of Treasury bonds vs VIX][image23]

## Intermarket behavior of S&P500 VS VIX

From the last two major financial crisis, VIX shot up to one of the highest when the stock market fell to almost the lowest. Most of the time, market rebounded before the panic is over. For other smaller market downtrends, or corrections, VIX also spiked up when market has dropped to its lowest point and was about to rebound. As such VIX as a fear index in risk sentiment is a lagging indicator.

What about VIX’s two other sentimental friends, TED Spread and High yield bond spread?

[image24]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/IntermarketBehaviorS%26P500VsVIX.png "Intermarket behavior of S&P500 VS VIX"
![Intermarket behavior of S&P500 VS VIX][image24]

## Intermarket behavior of TED spread and High yield bond spread vs S&P500
It seems TED and the other LIBOR-T-bill spreads and High yield bond spread did not react at the same time. High yield bond spread is almost as slow as VIX. Furthermore, high yield bond spread is quite volatile most of the time and as such not very useful as an indicator. The reason being is, it would be hard to tell which actions are for real and which is not, without the benefit of hindsight.

LIBOR-T-bill and TED spreads are the calmer beasts and have the wisdom to signal earlier. However, almost half of the stock market actions are in motion when TED spread reacted in a big way. Though, we do see a bit of TED spread jitters prior to that.

Now we shall revisit T-bills. From the plots above, if treasury bonds reacted much earlier than VIX, what about comparing it to the stock market? 

[image25]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/IntermarketBehaviorofTEDSpreadHighYieldBondSpreadVsS%26P500.png "Intermarket behavior of TED spread and High yield bond spread vs S&P500"
![Intermarket behavior of TED spread and High yield bond spread vs S&P500][image25]

## Intermarket behavior of Treasury bonds vs S&P500

From here it is obvious that the contraction of treasury bond spread precedes S&P500 down trends. When the spread was in widest range, market trends up for years.

In both 2000-2001 and 2008 crisis, short term yield (the orange-pinkish lines) actually exceed long term yield (the blueish lines) before the crashes. It seems market expect inflation and economic growth in the longer terms to be gloomier than now! Or worse, a crash or crisis is imminent!

So yield spread (short term Vs long term maturity spread) works conversely with bond spread (high yield/riskier vs low yield/low risk). When yield spread is high, market is optimistic of the future, when yield spread is low, market is more pessimistic and risk-averse. While high yield bond or TED spread work the other way. The exploration so far has clarified types of yield and spread and how they behave under risk-on/risk-off situation. The first two final plots conclude that. 
With this observation in mind, we can conclude that interest rate and their spread serve as a reliable indicator to signal of trouble. Looking forward, we can see that treasury bond spread is showing sign of contraction now, is a market downtrend imminent and is this the time to short the S&P500? 

[image26]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/IntermarketBehaviorOfTreasuryBondsVsS%26P500.png "Intermarket behavior of Treasury bonds vs S&P500"
![Intermarket behavior of Treasury bonds vs S&P500][image26]

## Intermarket behavior of Treasury bonds VS Dollar Index

Finally, since treasury bills are such a reliable indicator, we shall look at how it fare with dollar index. Unlike the earlier plots, this plot shows little relationship between bonds and dollar. As such the limitation of the technique we have used so far. It is meant to open room for further investigation beyond this project. More advanced techniques (to be discussed in Reflection) to be explored for the Dollar Index relationship with other assets.

Hypothetically, we can assume that the dollar plays many roles as an international reserve and trading currency in the global market, there are much more interactions in the works than the US stock market. Understandably, it would be challenging to find a trading clue from just a few visualizations. 

Nonetheless we should still explore dollar correlation with treasury bonds. The result shows that they generally have weak positive correlations: 

[image27]: https://github.com/jiewwantan/FinancialDataExploratoryAnalysis/blob/master/IntermarketBehaviorOfTreasuryBondsVsDollarIndex.png "Intermarket behavior of Treasury bonds VS Dollar Index"
![Intermarket behavior of Treasury bonds VS Dollar Index][image27]

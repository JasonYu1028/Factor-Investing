# Description

## Objective: 
In-depth backtesting of a quantitative trading strategy over a 35-year period, which utilizes ***Fama-MacBeth cross-sectional regressions*** and the ***Random Forest Model*** to train, validate, and test the trading model of 11 factors of four categories.

## Details:
### In-sample Training
1. The whole backtesting period is 35 years with 300 months (15 years) of in-sample training starting from Jan 1983 to Dec 2019 and 120 months (10 years) of out-of-sample testing starting from Jan 2020 to Dec 2019.

2. The universe of stocks is NYSE/Nasdaq stocks, only common stocks (not preferred, ETFs, etc.).

3. Each stock must have a price that exceeds *$5* per share and a market capitalization of equity of at least *$100 million* at the beginning of every forecast year (January of each year), to avoid trading illiquid stocks.

4. Uniformize/standardize and filter values of each of the chosen factors using **z-scores**, relative to the industry average and standard deviation of each month.

5. Use Fama-MacBeth regressions to estimate the factor premia on each factor during each estimation window, then compute the **average factor premia** across all 
windows and the **t-statistic** of this average (i.e., the Fama-MacBeth average and the Fama-MacBeth t-statistic). These represent the average profitability and the consistency of profitability of each factor, respectively. 

6. Drop factors from the final model if they end up with a backtest t-statistic that is low (e.g., *below 1*) or the wrong sign (e.g., negative for the E/P ratio, which should positively predict returns). However, may choose to keep a signal with a low t-statistic or even a wrong sign if there seems to be a strong economic story or a compelling research article that indicates it should work well when tried over many years. A rough “rule-of-thumb” is to keep at least 5-10 factors.

### Out-of-sample Testing
1. Use Fama-MacBeth linear regression (predicted *return = alpha + beta's * factor's*) to score stocks/predict returns then rank the portfolios in 10 quintiles and construct hedge portfolios by longing the top 10% and shorting the bottom 10% portfolios at each month

2. Use the Random Forest model to score stocks/predict returns then rank the portfolios in 10 quintiles and construct hedge portfolios by longing the top 10% and shorting the bottom 10% portfolios each month

3. Take the average of both Fama-MacBeth linear regression and Random Forest model to score stocks/predict returns then rank the portfolios in 10 quintiles and construct hedge portfolios by longing the top 10% and shorting the bottom 10% portfolios at each month

4. Analyze the performance of the three constructed hedge portfolios using the ***CAPM model*** and the ***Fama-French Four Factor model***

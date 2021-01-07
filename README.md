# Volatility Study
## Summary: 
• Conducted a volatility study to develop pairs trading strategy by writing web crawlers that automated extracting 30 equity and ETF spot and options prices data from CBOE and Yahoo Finance <br/>
• Utilized NumPy, Pandas, and SciPy packages to calculate implied volatility, realized volatility, and risk premiums to measure how the market prices risk <br/>
• Gathered and plotted daily VIX futures data with Selenium, Seaborn and Matplotlib to study volatility term structure <br/>
• Examined volatility clustering and built forecasting tools for market risk using correlations of daily absolute returns and volatility at different time lags <br/>

## Procedures:

### Prep: Data collection:

Write Python web crawler to automatically collect daily CBOE VIX futures data from the following sites:<br/>
http://www.cboe.com/trading-tools/strategy-planning-tools/term-structure-data#3 <br/>
Save data in CBOE VIX.csv file<br/>
http://www.cboe.com/products/futures/vx-cboe-volatility-index-vix-futures <br/>
Save data in CBOE VIX futures.csv file<br/>
Schedule the task to run daily using Task Scheduler <br/>

### Part 1: Vol smile analysis

1. Create list of about 30 stocks ranging from high to low beta. Include the major ETFs such as SPY, DIA, QQQ, GLD in the list
2. Automatically pull spot and option prices (bid price) middle of the trading day using Selenium package
3. Calculate using Newton method and plot implied vol (ImpVol) of options in each stock for strike prices ranging [stock price-20% - stock price+20%] using NumPy, Pandas, Matplotlib. Should see the “smile” for each stock. <br/>
Use the code for Put options for strikes < spot price, and code for Call options for strikes > spot price, then join the two.<br/>
4. Calculate smile numbers: <br/>
o Incremental Slope (ISp): change in ImpVol between consecutive strike prices <br/>
o Calculate average up-slope: Average [ISp(strike price>stock price)]<br/>
o Calculate average down-slope: Average [ISp(strike price<stock price)]<br/>
o Calculate Convexity: Average [Delta ISp] (from lowest strike to highest strike)<br/>
5. Output the data, calculations, and charts into Excel
6. Plot each of the smile numbers above for the whole set of stock in order of increasing beta
7. Repeat steps 2 – 5 with closing option prices
8. Run this vol smile analysis daily

### Part 2: Realized vs Implied Vol

Using SPY, IWM, DIA, TLT, QQQ and GLD
1. Calculate ImpVol for options expiring 1-month to 1-year, At-the-Money strikes.
2. Calculate ImpVol for options expiring 1-month to 1-year, 10% Out-of-the-Money strikes.
3. Calculate Realised Vol for options over 4 periods: Recovering from Great Recession (2011 to 2018), Trade War period (2018 to 2020), COVID crash (02-2020 to 03-2020), Recovery due to Fed intervention (03-2020 to 07-2020)
4. Calculate and plot risk premiums by subtracting most recent monthly realized vol from implied vol for options expiring in Dec 2020 of each ticker

### Part 3: Vol Term Structure
1. Using the data in “CBOE VIX futures” spreadsheet, plot “Settlement” prices vs “Expiration Date” for each block of data between “^VIX” rows.
2. Using the data in your “CBOE VIX” spreadsheet, plot “VIX” vs “Expiration Date” for each “Trade Date”, 1 plot per week.

### Part 4: Vol Clustering
Define:<br/>
CorN=corr(rt,rt+d): correlation of return (rt) at day t and return (rt+d) d days later<br/>
CorA=corr(|rt|,|rt+d|): correlation of absolute return (|rt|)at day t and absolute return (|rt+d|) d days later<br/>

Calculate: CorN and CorA values of SPY, IWM, DIA, TLT, and GLD for d=(2, 3, 5, 10, 15, 20, 25, 30) [Use 5 years of history]<br/>
Plot CorN and CorA vs days d<br/>
Build a future vol indicator: use the autocorrelations observed in the absolute return data to see if there is a correlation between observed vol over the previous d days and vol over the next d days<br/>

Utilizing same ETF list, close prices, and d days:<br/>
Define:<br/>
Sdf(d1)=standard deviation(|r1|,|r2|,…,|rd|)<br/>
Sdf(d2)=standard deviation(|r(d+1)|,|r(d+2)|,…,|r(2d)|)<br/>
Calculate: CorF=Correlation(Sdf(d1),Sdf(d2)), linear <br/>
Plot: CorF vs d for each ETF <br/>

Run for:<br/>
Major equity ETFs such as SPY, DIA, QQQ, IWM<br/>
Commodities ETFs such as GLD, SLV, USO, BNO, USL<br/>
Bond ETFs of different maturities such as TLT, IEI, SHY

*Note: Data and dates in this project was last updated August 14, 2020. Update dates and URLs for accurate numbers and calculations

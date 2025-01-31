## Rate-and-HousePrice-TrendX
Extracting insights from mortgage rates and house prices
### Project Overview

This project analyzes historical trends in average house prices and mortgage interest rates using time series decomposition techniques. By breaking down these variables into trend, seasonal, and residual components, it seeks to understand the underlying patterns of housing prices and lending rates. It will give homebuyers insights into the best times to buy or sell properties, providing a reliable guide for their decisions. Similarly, it will assist investors in making data-driven decisions on property investments, offering a reassuring tool for their strategies. The datasets are collected from the Federal Reserve Economic Data (FRED).

### Data Source

Federal Reserve Economic Data (FRED) contains the two datasets used for this analysis: the 30-year fixed-rate mortgage average in the United States and the Average sales price for new houses sold in the United States.

### Tools
-Python

### Data Cleaning and Preparation
The inital data preparation phase, I performed the following tasks:
 1. Data loading and inspection.
 2. Data cleaning and formatting.

### Exploratory Data Analysis
EDA involved exploring mortgage rates and the sale price for houses sold to answer the key questions, such as:
 - How have average house prices and mortgage rates changed over time?
 - Are there noticeable long-term trends in housing prices and interest rates?
 - Are there any unusual spikes or drops in home prices or mortgage rates?
 - What external factors might explain anomalies?
![image](https://github.com/user-attachments/assets/a55af022-58b6-4e84-a5ad-bb63e1cef4b2)


### Data Analysis
``` Python
price_decomposition = seasonal_decompose(df['Price'], model='additive', period=12)
rate_decomposition = seasonal_decompose(df['Rate'], model='additive', period=12)
price_decomposition.plot()
plt.show()
rate_decomposition.plot()
plt.show()
```

```python
seasonal_component = price_decomposition.seasonal
seasonal_df = pd.DataFrame({
    'Seasonal': seasonal_component,
    'Month': seasonal_component.index.month,  # Extract month
    'Year': seasonal_component.index.year     # Extract year
})
monthly_seasonal_avg = seasonal_df.groupby('Month')['Seasonal'].mean()
plt.figure(figsize=(10, 6))
monthly_seasonal_avg.plot(kind='bar', color='skyblue')
plt.title('Average Seasonal Effect on House Prices by Month')
plt.xlabel('Month')
plt.ylabel('Seasonal Component')
plt.xticks(ticks=range(12), labels=['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 
                                    'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'], rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()
```

![image](https://github.com/user-attachments/assets/ea283ec6-56e0-4ffd-9f0e-0d5b94d371d3)
![image](https://github.com/user-attachments/assets/36e86415-8caf-4630-86ff-09190ffe081e)
![image](https://github.com/user-attachments/assets/5c7859e4-cd5a-42e4-9b7a-3ae19a316f1a)


### Results/ Finding
From the plot of time series decomposition, I draw the following insights that will equip homebuyers and investors with valuable information:
 1. A clear upward trend indicates that house prices have increased significantly. They have been rising steadily, with a noticeable acceleration in recent decades, particularly after 2010.
 2. The seasonal variations in house prices seem periodic and consistent, suggesting regular seasonal factors influencing house prices.
     - House prices are significantly higher in April than the trend-adjusted baseline, likely due to increased market activity (e.g., spring buying season).
     - December also shows elevated seasonal effects, potentially driven by end-of-year buying incentives or reduced inventory.
     - House prices dropped in January due to a slower market after the holidays and winter weather affecting buyer activity.
     - House prices are low in May, June, and September reflecting reduced buyer interest or changes in inventory availability. 
     - February, October, and November show moderate positive seasonal effects, suggesting a ramp-up in activity during these months.
     - The low prices in March and July may represent transitions between peak and low seasons.
 3. The price residuals show increasing variance over time, implying that recent years might have seen more significant market uncertainty or external influences. This may be associated with the 2007-2009 Great Recession and the 2020 COVID pandemic.
 4. High Rates in the 1980s. The Mortgage rates were historically high, likely due to central bank inflation control measures.
 5. There has been a clear downward trend in rates, promoting housing affordability over the decades.
 6. The recent increase in mortgage rates indicates a potential reversal of the declining trend. The upward trend is due to global monetary policy responses to post-pandemic inflation.
 7. The residuals appear relatively stable, with occasional deviations, which could reflect major economic events.

### Recommendations
 - Homebuyers should act early. If they are planning to buy, delaying could mean paying a higher price in the future. Lock in a purchase sooner rather than later.
 - Homebuyers to choose fixed-rate Mortgages; this is because of uncertainty in interest rates.
 - Consider purchasing a house in January, May, and September, when prices are low and competition is reduced.
 - For investors, buy and hold. Given the long-term upward trend in house prices, real estate remains a strong asset for long-term appreciation.
 - Investors should sell their homes in April and December to maximize profits on property sales.
 - Investors should pay attention to interest rates and inflation that could impact real estate values.
 -  If rates drop in the future, consider refinancing to reduce borrowing costs.

   ### Limitations

   I removed all data with dates earlier than 1/1/1975 to match the dates for the two datasets. I have collective outliers for the 1981 interest rate. They are not really outliers, but their group represents the highest interest rate in the dataset and has unusual behavior



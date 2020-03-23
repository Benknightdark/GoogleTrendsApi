# 透過Google Trends 可以查詢關鍵字在各個時間點上的查詢次數變化，並讓我們可以更容易了解現今的趨勢。而如果可以透過Google Trends API呼叫其相關應用，則可以跟系統整合或進行各種資料分析。

# 但是Google Trends並沒有官方的API，所以今天會使用第三方Google Trends套件 - [PyTrends]([https://github.com/GeneralMills/pytrends](https://github.com/GeneralMills/pytrends)來Demo Google Trends的使用方式。



## 使用方式

- 下載PyTrends和引用相關套件
  
  ```python
  !pip install pytrends
  import pandas
  import numpy as np 
  ```

- ### Build PayLoad
  
  ```python
  pytrend = TrendReq(hl='zh-TW', tz=360)
  keywords = ['Azure','GCP','AWS']
  pytrend.build_payload(
      kw_list=keywords,
      cat=0,
      timeframe='today 3-m',
      geo='TW',
      gprop='')
    ```

- ### Interest Over Time
  
  ```python
  pytrend.interest_over_time().plot()
  ```
  
  

- ### Historical Hourly Interest
  
  ```python
  data=pytrends.get_historical_interest(keywords, year_start=2020,
  month_start=1, day_start=1, 
  hour_start=0, year_end=2020, 
  month_end=2, day_end=1, 
  hour_end=0, cat=0, geo='TW', gprop='', sleep=0)
  data.plot()
  
  ```

- ### Interest by Region
  
  ```python
  pytrends.interest_by_region(resolution='COUNTRY', inc_low_vol=True, inc_geo_code=False)
  ```
  
  

- ### Related Queries

  ```python
  pytrends.related_queries()['Azure']['top']
  pytrends.related_queries()['GCP']['top']
  pytrends.related_queries()['AWS']['top']
  ```
- ### Trending Searches
  ```python
  pytrends.trending_searches(pn='taiwan')
  ```

- ### Top Charts
  ```python
  top_charts_df = pytrend.top_charts(2019, hl='zh-TW', tz=300, geo='TW')
  ```

- ### Suggestions
  ```python
  pytrends.suggestions('azure')
  ```


# 資料來源
- [PyTrends](https://github.com/GeneralMills/pytrends)
- [Google Trends](https://trends.google.com/trends/)
- [Source Code](https://github.com/Benknightdark/GoogleTrendsApi)
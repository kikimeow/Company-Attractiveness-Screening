# Evaluate attractiveness of company for investment based on KPIs
 
400 days of KPI data of 64 companies are used for classifying companies into two groups- "Good Company" & "Bad Company." The KPIs include: <br>
* Mobile Downloads- Number of downloads of the company's mobile app on a given day
* Mobile MAUs - Number of people who used the company's app at least once in a given month
* Web visits - Number of visits to teh company's website on a given day
* Web rank- Number of visits to the company's website on a given day (lower is better)
* Web MUVs - Number of unique visitors to the company's web site in a given month
* Monthly sales - The comapny's revenue in a given month
* FB likes - Number of likes on the company's Facebook page on a given day. <Br>
  
### Feature Engineering
312 features are created to measure the investment opportunity of a company. For the KPIs in the dataset, the higher the number, the better the company is. The only exception is Web rank, where a lower number is better. The KPIs are summarized using rolling averages. A good company should exhibit three traits- Market dominance, Growth, and Consistency. 

**Market Dominance** <br>
To assess market dominance, rank based measurements are calculated. Companies are compared against each other for each of the KPIs.

**Growth** <br> 
To assess growth, we calculate how much the KPI has grown relative to historical average, and how much the KPI has grown relative to the current value. The growth of the ranks of the various KPI metrics are also calculated.

Example:  <br> 
growth calc relative to historical value = (Web visits 5-day moving average-Web visits 90-day moving average) / Web visits 90-day moving average
A company with 1000 visits now and 10 visits before, had a 9x growth. (1000-100)/10 = 9 

growth calc relative to current value = (Web visits 5-day moving average-Web visits 90-day moving average) / Web visits 5-day moving average
A company with 1000 visits now and 10 visits before, has a size of growth of 0.9 of its current value. (1000-100)/1000 = 0.9 

**Consistency** <br> 
To assess consistency, the changes of the KPI measurements between recent values and historical values should be small. We want to identify companies that are leaders and maintain its leadership. The direction of the changes in KPI also indicate if the performance of the companies have improved or worsened. For an existing market leader, the company should have small changes in KPI measurements. For an up-and-coming growth company, the company should see a positive improvement in KPI measurments.

Example: 
Web rank difference = Web rank difference(rolling 5 day average) - Web rank difference(rolling 90 day average) should be small.

**Why is rolling averages used** <br> 
The advantage of rolling averages is that it smooths out some noise, and it is also easier to see the changes in a timeseries. It is often useful to compare a short-term moving average against a longer-term moving average. In this analysis, the most recent observation of the moving averages are used for modeling.

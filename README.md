<img src='Images/README Header.jpg' width=100%>

# Finding Stock Market Inefficiencies

# Overview

HIT Investments is looking to leverage advanced analytics to identify inefficient companies where their low stock price is attractive when compared to their historic performance. HIT investments has 2 key evaluation metrics that are used to identify these companies:
1. **Value Metrics** which provide insight into a companies price relative to their recent historic performance
2. **Growth & Volatility Metrics** which provide insight into a companies recent stock performance to measure whether a company's value is growing and how volatile the price has been

This analysis will provide answers to the following important business questions:
1. **Where are there significant data quality issues which skew the results?**
2. **Which companies show high value, growth and low volatility?**
3. **How can machine learning classification be used to predict which companies to buy and which metrics are most important in making that prediction?**

The insights of the analysis will be summarized in a Tableau dashboard that HIT Investments can utilize to keep track of their current holdings, explore data quality issues and determine which companies could be a good investment.

# Business Problem

HIT Investments strives to maximize after-tax returns for their clients by actively identifying and capitalizing on proven inefficiencies in the stock market using quantitative analysis. 

A market is said to be "efficient" if the price of a stock reflects all available and relevant information. This theory holds true for larger companies that are thoroughly tracked by investment firms. However, HIT Investments believes the market has inefficiencies, specifically in the Micro-Cap and Small-Cap segments, which can be exploited to outpeform the stock market and deliver maximum return on investment. 

The 3 business questions that are important to answer with this analysis are:
1. **Where are there significant data quality issues?**

The Financial Modeling Prep API is constantly improving their data quality but there are significant issues that have been observed by HIT Investments that need to be identified. I will utilize an anomaly detection machine learning model along with a Tableau dashboard to highlight these data quality issues so that companies can be evaluated based on accurate data only.

2. **Which companies show high value, growth and low volatility?**

There are over 20,000 potential companies to invest in across multiple global markets. Manually evaluating each company for investment is unreasonable because of how quickly a company's stock price changes relative to how quickly someone could evaluate a company's performance. By using the Value and Growth Metrics, companies which show promise for investment can be quickly identified. 

3. **How can machine learning classification be used to predict which companies to buy and which metrics are most important in making that prediction?**

Machine learning is a way in which companies can be quickly evaluated based on historic performance on the Value Metrics, Growth Metrics as well as other important features of a company. Another benefit of machine learning is that some models will provide insights into which company features are most important to focus on when predicting which companies to invest in.

# Data

This analysis will gather company specific performance metrics from the Financial Modeling Prep [FMP API](https://financialmodelingprep.com/developer/docs). I utilized a [Data Collection notebook](https://github.com/bentson1187/Stock-Market-Inefficiency-Analysis/blob/dde064775aef01477dd5dcd21c0d8ca363cb2213/Data%20Collection.ipynb) to produce the API calls and the .csv's necessary to import into this analysis as well as the [Tableau dashboard](https://public.tableau.com/app/profile/brian8863/viz/CapstoneDashboard_16252496264850/HoldingsDashboard?publish=yes). That Data Collection notebook can be found in the same github repo. 

# Methods

There a 2 main focuses of this analysis:
1. **Finding data quality issues**
2. **Find which companies show promise for investment using machine learning classification**

In order to find potential data quality issues, I will utilize an anomaly detection algorithm called Isolation Forest which will show the most extreme outliers in the data with respect to a company's Value Metrics and Growth Metrics. This will help validate whether or not the values that feed these metrics are accurate.

To find which companies show promise for investment, companies will be analyzed on their historical performance for Value Metrics and Growth Metrics. Each company will be labeled based on domain expertise rules-of-thumb into one of the following buckets:
1. Buy
2. Risky Buy
3. Affordable
4. Hold
5. Sell

<img src='Images/3d Scatter Plot.png' width=100%>

A machine learning classification model will then be trained on these new labels to ultimately predict which companies should be evaluated further for investing and which company features played a significant role in those predictions. 

Lastly, all relevant company information and model predictions will be summarized in an interactive Tableau dashboard which allows HIT Investment employees to quickly research the companies for which the model predicts are good investments and have accurate underlying data quality.

# Results

There were 2 main results of this analysis that I'd like to discuss:
1. **Using anomaly detection for identifying potentially incorrect data**
2. **Utilizing classification algorithms to predict my action labels.**

**Anomaly Detection**

The anomaly detection algorithm identified 4-5% of the stocks which are outliers for the main features in this analysis. The insights from this are best seen in the Tableau dashboard where I utilize the `anomaly` feature to quickly mark stocks which may have a potential issue in the data quality. However, below is a single example where the anomaly detection algorithm identified that a Revenue per Share of 26,456 looks abnormal when compared to other metrics for the same stock. As you can see below, there seems to be values which are extremely high in comparison to past values. These anomalies are making stock IIVIP look much better than it actually is. In fact, IIVIP is ranked #1 for the Value Rank meaning it is the cheapest stock compared to its performance. However, because of the anomaly detection algorithm we know that this ranking was false due to anomalies in the data quality.

<img src='Images/Anomaly Detection Screenshot for README.png' width=100%>
<br>
<br>

**Classification Modeling of `action` Feature**

The initial labeling of the `action` feature was done as a hard-coded segregation and then used as the target of the classification model. The initial models were providing great overall accuracy of 92%. However, the XGBoosted model performed improved overall accuracy to 94% but significantly increased the recall score of the "Buy" action which is the most important label. The model also gave insight into which features were most important to making its predictions. By far, the `ev_to_operating_cashflow` feature was the most important.

<img src='Images/Model Results Graphs.png' width=100%>


# Conclusions

In conclusion, this analysis provides HIT Investments 3 main capabilities that improve the analysis of which stocks to evaluate for potential purchase:
1. The ability to segregate stocks into distinct action buckets using machine learning which drastically speeds up the analysis since a user can focus on only the stocks with the action of "Buy". 
2. Provides a quick way to identify stocks where the data quality has skewed the results and further vetting needs to be done before making an investment. 3. Gives insight into which stock performance features are good at helping bucket stocks into distinct action buckets

The 3 capabilities above are brought together intelligently in an interactive Tableau dashboard that will make investigating and analyzing stocks much quicker.

<img src='Images/Grouped Dashboard Screenshot.png' width=100%>

For the future, it is recommended to create a live data pipeline that can be updated daily to have the most up to date information feeding the Tableau dashboard at any given moment.

## **For More Information**

Please review our full analysis in the [Jupyter Notebook](https://github.com/bentson1187/Stock-Market-Inefficiency-Analysis/blob/9f0b97058ed28d6b5c27332730886f05fb60e1d0/Analysis%20Notebook.ipynb),  [Presentation](https://github.com/bentson1187/Stock-Market-Inefficiency-Analysis/blob/8e66da0f9ff55c1929d04ee97af80b6d65c8ae0a/Stakeholder%20Presentation.pdf) and the [Tableau Dashboard](https://public.tableau.com/app/profile/brian8863/viz/CapstoneDashboard_16252496264850/ResearchDashboard?publish=yes). 

For any additional questions, please contact **Brian Bentson, bentson.brian@gmail.com**

## Repository Structure

Describe the structure of your repository and its contents, for example:

```
├── README.md                           <- The top-level README for reviewers of this project
├── Analysis Notebook.ipynb       <- Narrative documentation of the analysis in Jupyter notebook
├── Stakeholder Presentation.ppt        <- Project presentation
├── Data        <- Data used for analysis
└── Images                              <- Both sourced externally and generated from code
```

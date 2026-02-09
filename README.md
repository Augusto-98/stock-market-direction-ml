_**Stock Market Direction Prediction with Machine Learning**_

_**Quick Summary**_

	- Built an end-to-end machine learning pipeline to predict next-day stock market direction using financial time-series data  
	- Engineered lag-based and rolling statistical features from daily returns  
	- Evaluated multiple models (Logistic Regression, Random Forest, Gradient Boosting, XGBoost) using time-aware validation to avoid data leakage
	- Best-performing models achieved approximately 51–52% accuracy, reflecting weak but detectable predictive signals  
	- Results emphasize realistic expectations when applying ML to financial markets



_**Project Objective**_

Predict whether the stock market (SPY ETF) will move up or down the following day using historical financial data.

Rather than forecasting raw prices, the problem is framed as a binary classification task, which is more robust and realistic for short-term financial modeling.


_**Notebook**_

- Main analysis: [notebooks/main_analysis.ipynb](notebooks/main_analysis.ipynb)


_**Dataset**_

Historical daily price data for the SPY ETF was collected using the Yahoo Finance API (yfinance package).

Features were derived from daily returns, not raw prices, to ensure stationarity and improve model performance.

![SPY close Price](./images/spy_close_price.png)



_**Data Science Pipeline**_

Data collection from Yahoo Finance

Data cleaning and preparation

Daily return computation

Target variable creation (next-day direction)

Feature engineering:

	-Lagged returns

	-Rolling means

	-Rolling volatility

Time-series aware train-test split (no shuffling)

Model training and evaluation

Model comparison and analysis



_**A correlation analysis was conducted to evaluate potential multicollinearity introduced by the engineered features.**_


The results indicate low correlation among return-based and lagged features, reflecting the weak short-term dependency typically observed in financial markets. As expected, moderate correlations were observed among rolling mean features (50/200-day windows) and among rolling volatility measures, which capture persistent market regimes.

Importantly, no extreme linear correlations were identified that would justify feature removal at this stage. The observed relationships suggest that the engineered features provide complementary information related to momentum, trend, and volatility dynamics, making them suitable for tree-based machine learning models.

![Feature correlation matrix](./images/Feature_correlation.png)



_**Models Tested**_

Logistic Regression (baseline + class balanced)

Random Forest (baseline + class balanced)

Gradient Boosting (HistGradientBoostingClassifier)

XGBoost (XGBClassifier)

Class imbalance was addressed using class weighting and sample weighting techniques.



_**Results Summary**_

Model				Accuracy	Recall (Down)	Recall (Up)	Macro F1
XGBoost				0.519267	0.534699	0.500000	0.516581
Gradient Boosting		0.518004	0.507395	0.531250	0.517005
Logistic regression		0.516740	0.519909	0.512784	0.514957
Random Forest (balanced)	0.512318	0.491468	0.538352	0.511771

Although XGBoost achieved the best accuracy, Gradient Boosting achieved the strongest and most stable performance with smaller recall difference and best macro F1-score among tested models.  

Despite modest performance, results reflect realistic financial market conditions and demonstrate proper time-series modeling practices.

![Accuracy comparison](./images/results_accuracy.png)
![Recall comparison](./images/results_recall.png)


_**Key Insights**_

-Financial time-series data contains weak but detectable predictive signals

-Naive models tend to collapse toward majority classes

-Class balancing is essential for realistic evaluation

-Results remain close to random, highlighting the intrinsic difficulty of predicting short-term market movements.



_**Technologies Used**_

Python

Pandas, NumPy

scikit-learn

XGBoost

yfinance

Matplotlib

Seaborn


_**Conclusion**_

This project demonstrates a complete Data Science workflow applied to real financial data — from data acquisition to model comparison and critical performance evaluation.

It highlights both the challenges of financial prediction and the importance of rigorous machine learning practices when working with noisy time-series data.


_**Disclaimer**_

This project is for educational purposes only and does not constitute financial advice.



_**Author**_

Augusto Fernandes

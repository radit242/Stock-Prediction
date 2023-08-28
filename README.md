**Stock Prediction** 

website - https://stock-prediction-ajay2rpastuvkpmtczu7ny.streamlit.app/




Stocks are financial instruments that represent ownership in a company. When individuals or institutions buy shares of a company's stock, they become shareholders and have a claim on the company's assets and earnings. Stocks are traded on stock exchanges, and their prices are influenced by various factors such as company performance, market conditions, and economic trends.

Stock predictions aim to forecast the future price movements of specific stocks. Analysts, traders, and investors use various techniques, including fundamental analysis (evaluating a company's financial health), technical analysis (examining historical price patterns), and sentiment analysis (assessing market sentiment) to make informed predictions. Accurate stock predictions can offer valuable insights for investors to make well-informed decisions about buying, selling, or holding stocks in their portfolios. However, it's important to note that stock prediction is inherently uncertain, and market risks should always be carefully considered.

We are using financial data from Yahoo finance. The data being used in this prediction model is from 2010-01-01 to Current date. 

![image](https://github.com/radit242/Stock-Prediction/assets/107355525/c6d0cb37-c05c-466b-bbf9-032d4eb1c985)

**MA100 and MA200**

In financial markets, "MA100" and "MA200" typically refer to moving averages. Moving averages are popular technical indicators used by traders and investors to smooth out price data and identify trends over a specific period.

MA100: This stands for the 100-day moving average. It is calculated by adding up the closing prices of the asset over the past 100 trading days and then dividing the sum by 100.

MA200: This stands for the 200-day moving average. It is calculated in a similar way to MA100, but using the past 200 trading days instead.

When the MA100 crosses above the MA200, it is called a "golden cross," signaling a potentially strong bullish trend. On the other hand, if the MA100 crosses below the MA200, it is referred to as a "death cross," indicating a potentially strong bearish trend.

If the MA100 is greater than the MA200, it suggests that the recent price action is stronger, and the asset is potentially in a bullish trend.

If the MA100 is lower than the MA200, it indicates weaker recent price performance and a potential bearish trend

![image](https://github.com/radit242/Stock-Prediction/assets/107355525/b9b8483e-e627-4519-8d09-daae7b6837fc)

A training and test data set is being formed with training set being 70% of the data and test data size is about 30% of the data.
Only Close price is considered for the prediction.

Data that is being used to train the model is scaled with min value 0 and max value is 1. This is essential for algorithms that are sensitive to the scale of features, as it prevents some features from dominating others due to their larger magnitude.

The model uses previous 100 days closing value to predict todays stock price. Two arrays are used x_train and y_train. x_train stores stock price for the last 100 days and y_train stores the price of todays price. x_train will be passed down to the deep learning model sequential with LSTM neural network which uses relu actvation function to predict todays stock price depending on the stock price of the last 100 days. y_train is also passed to the model for validation purpose.

a new model named stock_prediction1.h5 is being trained for predicting data after 2019 as most of the stocks have showed drastic change after 2019

![image](https://github.com/radit242/Stock-Prediction/assets/107355525/6ddfee54-ba59-4a42-9ffb-d5153332396e)


**Prophet model**

Prophet is a time series forecasting model developed by Facebook's Core Data Science team. It is designed to provide accurate and intuitive predictions for time series data with strong seasonality and multiple changepoints. It is being trained using the same data_training set that has been used for traing sequential model

For accuracy purpose we are only predicting 4 months into the future. Since LSTM donot have the ability to extrapolate

 Prophet employs its make_future_dataframe() function, which creates a dataframe with dates extending into the future. The predict() function then utilizes this extended dataframe to forecast future values of the time series, including trend, seasonality, and uncertainty intervals.

 ![image](https://github.com/radit242/Stock-Prediction/assets/107355525/3d3052ed-b329-430c-887c-ea748ef911f8)

![image](https://github.com/radit242/Stock-Prediction/assets/107355525/b57872d0-6077-4125-9342-ab0042b03c00)


The future dataframe made using make_future_dataframe() is appended with data frame which will be used to predict future data using sequential model. Sequential model is being used to predict the entire dataset collected from yahoo data frame having data till this date. This set is done before appending the future data with dataframe. 

temp_df_Copy_close a dataframe is created to store all the actual close value before they are droped.
temp_df_copy has only the prediction value
Since we dont have stock value of future data so we are not being able to use any existing data to validate the data. we have two arrays x_future . x_future is appending last 300 days value from today's date to predict tomorrows stock data which is appended to temp_df_copy which has the predicting data pf previous days. 

![image](https://github.com/radit242/Stock-Prediction/assets/107355525/68e52b2e-9a3b-4198-9ed9-da5d77a1032c)


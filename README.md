# S&P 500 Index

## Examining S&P 500 Index Data from 1/1/2015 to 12/31/2019
The data is gathered from the yfinance library. A total of 1258 dates of open price, high price, low price, close price, volume of stocks, dividends, and stock splits. The dividends and stock splits columns only had values of 0, so these two columns were dropped.

![Candlestick_s&p_500](https://github.com/oimartin/SP_500_index_RNN/blob/main/images/canldestick_allyears.png?raw=true)

Plotting all of the data in a canldestick chart, there was a general trend of increasing open, high, low and close prices. The lowest price was a low price on January 20, 2016 at $1812.29 and the highest price was a high price on December 27, 2019 at $3,247.93. 

![boxplot_s&p_500](https://github.com/oimartin/SP_500_index_RNN/blob/main/images/boxplot_years_openHighlowClose.png?raw=true)
![hist_open_price_by_year](https://github.com/oimartin/SP_500_index_RNN/blob/main/images/compare_open_all.png?raw=true)

The boxplot comparison of open, high, low and close prices across the five years shows that the each year is distinct across the four prices. 2015 and 2016 years are relatively similar across the four prices. From 2017 to 2019 is where there is a stronger trend of increasing prices.The spread of prices for 2019 is quite wide compare to the other years and more centered. 

![histograme_volume_sp500](https://github.com/oimartin/SP_500_index_RNN/blob/main/images/combined_volume.png?raw=true)
![scatterplot_volume_sp500](https://github.com/oimartin/SP_500_index_RNN/blob/main/images/scatter_year_volume_all.png?raw=true)

The distribution of volume of stocks is slightly skewed to the right, with a majority of volume of stocks traded is around 3.5 billion stocks. The volume of stocks traded at the end of year in November or December experience a wider range of volume of stocks traded.

![open_close_high](https://github.com/oimartin/SP_500_index_RNN/blob/main/images/3d_view_open_high_close_all.png?raw=true)

For the years from 2015-2019, there seems to be a linear relationship among the three prices.

## Preprocessing Data
All input data, open, high, and low prices, and output data, close prices, were standardized using the MinMaxScaler with range 0 to 1. Using the function from https://machinelearningmastery.com/how-to-develop-lstm-models-for-time-series-forecasting/ to transform the data to be used in RNN as batch size, time steps, and input size. The train shape was (956, 50, 3) and the test shape was (202, 50, 3)The train data was taken from the first 80% the data, and the remaining 20% of the data was used for the test dataset. A validation data set was designateted to be 20% of the training data.

## Model Comparisons
All three RNN models were run with an EarlyStopping(monitor='loss') with 50 epochs. compiled with the adam optimizer and mse loss metric. The rnn1 model only has 3 SimpleRNN layers and was compiled with mse as the loss metric. rnn2 model has 4 LSTM layers and one SimpleRNN layer. rnn3 model has two LSTM layers with relu activation and one dense layer. rnn2 and rnn3 have been compiled with hinge as the loss metric. The MSE for train and test data sets for all  

![rmse](https://github.com/oimartin/SP_500_index_RNN/blob/main/images/rnn_models_RMSE.png?raw=true)
![mae](https://github.com/oimartin/SP_500_index_RNN/blob/main/images/rnn_models_MAE.png?raw=true)
![runtime](https://github.com/oimartin/SP_500_index_RNN/blob/main/images/rnn_models_runtime.png?raw=true)

## Management Research Question
Predicting the future close prices or any other stock prices is helpful in order to gauge whether to hold onto stocks or sell stocks. 

## Conclusion
None of the models had very promising MSE scores. I choose to evaluate the model on 50 time step which may have negatively impacted the models ability to predict day to day prices. I would also try to increase the number of epochs run in order to bring down the MSE loss function. 

model | train/test | MSE
-- | -- |  --
rnn1 | train | 425.93
rnn1 | test | 875.96
rnn2 | train | 2396.27
rnn2 | test | 6269,16
rnn3 | train | 727.83
rnn3 | tesst | 1857.27


# Big-Data-Course

## time series forecasting
For my project I have chosen to make a forecast based on time.
I use the data from the past to predict future data.

### The data
The dataset that I used is about the monthly beer production in Australia, I found this data on kaggle.
This dataset stretches from 1956 all the way to 1995 however I only selected the data from 1959 till 1973 since in that timeframe there was a clear trend in the sale numbers.
Then i transformed the dataframe to have Date as index and the monthly beer production just as values.

### Decompose the data
First i decompose the data to have a look at some important values.
Trend: Here we can see that there is a clear increasing trend in our data and this will be used as guideline to predict further data.
Seasonal: This shows us that there is a clear seasonal patern in our data. We can see that the sales rise after september and then after january they go back down.

### Observe the correlation
To observe the correlation i used autocorrelation.
Autocorrelation plots graphically summarize the relationship between an observation in a time series and an observation at a prior time.
Sharp peaks indicate a clear correlation where as shorter peaks indicate little correlation in a time series.
As we can see in the notebook there is a clear correlation in the data.

### Rolling statistics
Now I visualise the rolling mean and the rolling standard deviation.
As we can see the rolling mean increases as the monthly beer sales increase.
To have an accurate forecast the rolling mean has to be as close to constant as possible therefor we still have to transform the data to achieve this.

### Dickey fuller test
Before I transform the data I take a look at the dickey fuller test. The important value to look for is the p-value. This ideally is as close to 0 as possible. The result of the test however is 0.99 wich isn't ideal to perform the forecast prediction.

### Stationary data
To make the data stationary I use differencing. Once non seasonal "diff()" and once seasonal "diff(12)" because we have monthly data with a clear seasonal trend.
If we now run the dickey fuller test we see that the p-value has decreased to 0.000096 wich is very good and is a sign the data is stationary.

### Arima model
I use the pmdarima library to extract the best parameters for the arima model because otherwise this can get quite complex. I put seasonal=True and m=12 for this data.

### Train the data
When training the data i got the best results when i used 80% as train data and 20% as test data.

### Sarima model
This is the same as the arima model but with extra parameters to include seasonality. This can also be achieved with the regular arima model but is much more difficult that way.
I got the best results with the following parameters:
order=(2,1,3)
seasonal_order=(1,1,1,12)

### Validate the model
When we take a look at the diagnostics of the model we can see that the data is very close to being perfectly normalized this is a sign we have a very good model.

### Making a forecast and compare it to real data
Before making a future forecast I first compare the trained data to the test data to validate the results are accurate.
First I visualised the data and quickly we can see that the forecast is quite close to the real values.
When checking predicted values with real values we can see there is a slight margin between the 2.

### Test the accuracy 
If we test the accuracy we can see we have achieved just shy of 90% accuracy with the predicted forecast, something i am quite proud of given I used a real dataset from kaggle and not just some tutorial dataset.

### Forecast 
Finally I made a final forecast. I added an extra cell below to run the forecast against the real data and if we use the complete dataset we can see the forecast is pretty accurate.
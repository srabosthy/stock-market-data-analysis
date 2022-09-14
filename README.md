<h1 align="center">Stock Market Data Analysis</h1>

<h2 align="center">Time Series Analysis using Python</h2>

Analyzing and identifying patterns in a time series collection is known as time series analysis. A collection of data over a period of time is referred to as a time-series dataset. Time-series data includes information on stock prices, monthly sales, daily rainfall, and hourly website traffic. As a data scientist, you will use this information to solve business problems. This article is for you if you want to learn Time Series Analysis. I'll walk you through the Python time series analysis task in this article.

<h3 align="center">Time Series Analysis</h3>

Install Required Dependencies
```
!pip install yfinance
!pip install plotly==5.10.0
```

Import Required Libraries
```
import pandas as pd
import yfinance as yf
import datetime
from datetime import date, timedelta
import plotly.express as px
import plotly.graph_objects as go
```

Get Present Date
```
today = date.today()
print(today)
d1 = today.strftime("%Y-%m-%d")
end_date = d1
print(end_date)
d2 = date.today() - timedelta(days=360)
d2 = d2.strftime("%Y-%m-%d")
start_date = d2
print(start_date)
```

Download Stock Dataset From yfinance
```
data = yf.download('AAPL',
                   start = start_date,
                   end = end_date,
                   progress = False)
data.head()
```

Dataframe Index Selection
```
data["Date"] = data.index
data = data[["Date", "Open", "High", "Low", "Close", "Adj Close", "Volume"]]
data.reset_index(drop=True, inplace=True)
data.head()
```

Plot The Dataset
```
figure = px.line(data, x = data['Date'], y = "Close", title = "Time Series Analysis (Line PLot)")
figure.show()
```

Plot Candlestick Chart To Analyse Realtime Data From Stock Market
```
figure = go.Figure(data=[go.Candlestick(x = data.index, open = data["Open"], high = data["High"], low = data["Low"], close = data["Close"])])
figure.update_layout(title = "Time Series Analysis (Candlestick Chart)", xaxis_rangeslider_visible = False)
figure.show()
```

Plot Bar Chart
```
figure = px.bar(data, x = data.index, y = "Close", title = "Time Series Analysis (Bar Plot)")
figure.show()
```

Line Plot
```
figure = px.line(data, x = data.index, y = 'Close', range_x = ['2021-07-01' , '2021-12-31'], title = "Time Series Analysis (Custom Date Range)")
figure.show()
```

Plot Dynamic Candlestick
```
figure = go.Figure(data = [go.Candlestick(x = data.index, open = data["Open"], high = data["High"], low = data["Low"], close = data["Close"])])
figure.update_layout(title = "Time Series Analysis (Candlestick Chart with Buttons and Slider)")

figure.update_xaxes(
    rangeslider_visible = True,
    rangeselector = dict(
        buttons = list([
            dict(count = 1, label = "1m", step = "month", stepmode = "backward"),
            dict(count = 6, label = "6m", step = "month", stepmode = "backward"),
            dict(count = 1, label = "YTD", step = "year", stepmode = "todate"),
            dict(count = 1, label = "1y", step = "year", stepmode = "backward"),
            dict(step = "all")
            ])
    )
)
figure.show()
```

<h2 align="center">Summary</h2>

A collection of data over a period of time is referred to as a time-series dataset. Analyzing and identifying patterns in a time series collection is known as time series analysis. A time series data might have time intervals that are weekly, monthly, daily, or even hourly. I hope you enjoyed reading this documentation on Python-based time series analysis.

<h2 align="center">Referrence</h2>

- [Time Series Analysis doc](https://thecleverprogrammer.com/2022/01/17/time-series-analysis-using-python/)

- [Get Stock Data](https://thecleverprogrammer.com/2021/12/21/get-stock-price-data-using-python/)

- [What Is Open High Low Close in Stocks?](https://analyzingalpha.com/open-high-low-close-stocks)

# Imports & Open File


```python
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
import numpy as np
import seaborn as sns
```


```python
crypto_df = pd.read_csv("CryptocoinsHistoricalPrices.csv")
```


```python
crypto_df.columns
```




    Index(['Unnamed: 0', 'Date', 'Open', 'High', 'Low', 'Close', 'Volume',
           'Market.Cap', 'coin', 'Delta'],
          dtype='object')




```python
crypto_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Market.Cap</th>
      <th>coin</th>
      <th>Delta</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1/4/18</td>
      <td>15270.7</td>
      <td>15739.7</td>
      <td>14522.2</td>
      <td>15599.2</td>
      <td>21,783,200,000</td>
      <td>256,250,000,000</td>
      <td>BTC</td>
      <td>0.021512</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1/3/18</td>
      <td>14978.2</td>
      <td>15572.8</td>
      <td>14844.5</td>
      <td>15201.0</td>
      <td>16,871,900,000</td>
      <td>251,312,000,000</td>
      <td>BTC</td>
      <td>0.014875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1/2/18</td>
      <td>13625.0</td>
      <td>15444.6</td>
      <td>13163.6</td>
      <td>14982.1</td>
      <td>16,846,600,000</td>
      <td>228,579,000,000</td>
      <td>BTC</td>
      <td>0.099604</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1/1/18</td>
      <td>14112.2</td>
      <td>14112.2</td>
      <td>13154.7</td>
      <td>13657.2</td>
      <td>10,291,200,000</td>
      <td>236,725,000,000</td>
      <td>BTC</td>
      <td>-0.032242</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>12/31/17</td>
      <td>12897.7</td>
      <td>14377.4</td>
      <td>12755.6</td>
      <td>14156.4</td>
      <td>12,136,300,000</td>
      <td>216,326,000,000</td>
      <td>BTC</td>
      <td>0.097591</td>
    </tr>
  </tbody>
</table>
</div>




```python
#determine total number of altcoins
crypto_df["coin"].nunique()
```




    1356




```python
#filter out top 15 cryptocurrencies to analyze
top15 = crypto_df.loc[(crypto_df["coin"]=="BTC")|(crypto_df["coin"]=="ETH")|
                      (crypto_df["coin"]=="LTC")|(crypto_df["coin"]=="MIOTA")|
                      (crypto_df["coin"]=="XRP")|(crypto_df["coin"]=="DASH")|
                      (crypto_df["coin"]=="XEM")|(crypto_df["coin"]=="XMR")|
                      (crypto_df["coin"]=="BTG")|(crypto_df["coin"]=="ETC")|
                      (crypto_df["coin"]=="ADA")|(crypto_df["coin"]=="EOS")|
                      (crypto_df["coin"]=="XLM")|(crypto_df["coin"]=="NEO")|
                      (crypto_df["coin"]=="BCC")
                      ,:] 
top15.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Market.Cap</th>
      <th>coin</th>
      <th>Delta</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1/4/18</td>
      <td>15270.7</td>
      <td>15739.7</td>
      <td>14522.2</td>
      <td>15599.2</td>
      <td>21,783,200,000</td>
      <td>256,250,000,000</td>
      <td>BTC</td>
      <td>0.021512</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1/3/18</td>
      <td>14978.2</td>
      <td>15572.8</td>
      <td>14844.5</td>
      <td>15201.0</td>
      <td>16,871,900,000</td>
      <td>251,312,000,000</td>
      <td>BTC</td>
      <td>0.014875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1/2/18</td>
      <td>13625.0</td>
      <td>15444.6</td>
      <td>13163.6</td>
      <td>14982.1</td>
      <td>16,846,600,000</td>
      <td>228,579,000,000</td>
      <td>BTC</td>
      <td>0.099604</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1/1/18</td>
      <td>14112.2</td>
      <td>14112.2</td>
      <td>13154.7</td>
      <td>13657.2</td>
      <td>10,291,200,000</td>
      <td>236,725,000,000</td>
      <td>BTC</td>
      <td>-0.032242</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>12/31/17</td>
      <td>12897.7</td>
      <td>14377.4</td>
      <td>12755.6</td>
      <td>14156.4</td>
      <td>12,136,300,000</td>
      <td>216,326,000,000</td>
      <td>BTC</td>
      <td>0.097591</td>
    </tr>
  </tbody>
</table>
</div>



# 1) Correlation with Bitcoin


```python
#filter the top 15 dataframe
top15 = top15[["Date", "Close", "coin"]]
```


```python
#convert the date to datetime so we can use it in a plot 
#top15.set_index(pd.to_datetime(top15["Date"], format = "%m/%d/%y"), inplace = True) 
top15["Date"]=pd.to_datetime(top15["Date"]) #, format = "%m/%d/%y")
top15.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Close</th>
      <th>coin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-01-04</td>
      <td>15599.2</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-01-03</td>
      <td>15201.0</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-01-02</td>
      <td>14982.1</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-01-01</td>
      <td>13657.2</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-12-31</td>
      <td>14156.4</td>
      <td>BTC</td>
    </tr>
  </tbody>
</table>
</div>




```python
#plot an individual graph for historic closing price data for each of the 15 cryptocurrencies
for name, group in top15.groupby("coin"):
    group.plot(x= "Date", y= "Close", figsize=(15,4), grid = True)
    plt.ylabel("Close Price", fontsize = 15)
    plt.xlabel("Date", fontsize = 15)
    #plt.xlim(top15.iloc[-1,0], top15.iloc[0,0])
    plt.xlim('2017-01-01', top15.iloc[0,0])
    plt.title(name, fontsize = 15)
```


![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_0.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_1.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_2.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_3.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_4.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_5.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_6.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_7.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_8.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_9.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_10.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_11.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_12.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_13.png)



![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_10_14.png)



```python
top5 = crypto_df.loc[(crypto_df["coin"]=="BTC")|(crypto_df["coin"]=="ETH")|
                      (crypto_df["coin"]=="LTC")|(crypto_df["coin"]=="MIOTA")|
                      (crypto_df["coin"]=="XRP")
                      ,:]

top10 = crypto_df.loc[(crypto_df["coin"]=="DASH")|(crypto_df["coin"]=="XEM")|
                      (crypto_df["coin"]=="XMR")|(crypto_df["coin"]=="BTG")|
                      (crypto_df["coin"]=="ETC")
                      ,:]

final_top = crypto_df.loc[(crypto_df["coin"]=="ADA")|(crypto_df["coin"]=="EOS")|
                      (crypto_df["coin"]=="XLM")|(crypto_df["coin"]=="NEO")|
                      (crypto_df["coin"]=="BCC")
                      ,:]
```


```python
top5 = top5[["Date", "Close", "coin"]]
top10 = top10[["Date", "Close", "coin"]]
final_top = final_top[["Date", "Close", "coin"]]
```


```python
top5.set_index(pd.to_datetime(top5["Date"], format = "%m/%d/%y"), inplace = True) 
top5["Date"]=pd.to_datetime(top5["Date"], format = "%m/%d/%y") 
top5 = top5.reset_index(drop=True)
top10.set_index(pd.to_datetime(top10["Date"], format = "%m/%d/%y"), inplace = True) 
top10["Date"]=pd.to_datetime(top10["Date"], format = "%m/%d/%y") 
top10 = top10.reset_index(drop=True)
final_top.set_index(pd.to_datetime(final_top["Date"], format = "%m/%d/%y"), inplace = True) 
final_top["Date"]=pd.to_datetime(final_top["Date"], format = "%m/%d/%y") 
final_top = final_top.reset_index(drop=True)
```


```python
pd.pivot_table(top5, values= "Close", columns= "coin", index= "Date").plot(figsize=(15,10))
plt.ylabel("Close Price", fontsize = 20)
plt.xlabel("Date", fontsize = 20)
```




    <matplotlib.text.Text at 0x116daa048>




![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_14_1.png)



```python
pd.pivot_table(top10, values= "Close", columns= "coin", index= "Date").plot(figsize=(15,10))
plt.ylabel("Close Price", fontsize = 20)
plt.xlabel("Date", fontsize = 20)
```




    <matplotlib.text.Text at 0x116ef2470>




![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_15_1.png)



```python
pd.pivot_table(final_top, values= "Close", columns= "coin", index= "Date").plot(figsize=(15,10))
plt.ylabel("Close Price", fontsize = 20)
plt.xlabel("Date", fontsize = 20)
```




    <matplotlib.text.Text at 0x1138cfa58>




![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_16_1.png)



```python
#Plotting all top15 coins together. All coins are trending upwards. 
#All coins experience the majority of their growth in 2017.
pd.pivot_table(top15, values= "Close", columns= "coin", index= "Date").plot(figsize=(15,10))
plt.ylabel("Close Price", fontsize = 20)
plt.xlabel("Date", fontsize = 20)
```




    <matplotlib.text.Text at 0x119f0c080>




![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_17_1.png)



```python
top15cor = crypto_df.loc[(crypto_df["coin"]=="BTC")|(crypto_df["coin"]=="ETH")|
                      (crypto_df["coin"]=="LTC")|(crypto_df["coin"]=="MIOTA")|
                      (crypto_df["coin"]=="XRP")|(crypto_df["coin"]=="DASH")|
                      (crypto_df["coin"]=="XEM")|(crypto_df["coin"]=="XMR")|
                      (crypto_df["coin"]=="BTG")|(crypto_df["coin"]=="ETC")|
                      (crypto_df["coin"]=="ADA")|(crypto_df["coin"]=="EOS")|
                      (crypto_df["coin"]=="XLM")|(crypto_df["coin"]=="NEO")|
                      (crypto_df["coin"]=="BCC")
                      ,:] 
```


```python
top15cor = top15cor[["Date", "Delta", "coin"]]
top15cor['Date'] = pd.to_datetime(top15['Date'])
top15cor = top15cor[(top15cor['Date'] > '2016-12-31') & (top15cor['Date'] <= '2017-12-31')]  
top15cor.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Delta</th>
      <th>coin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>2017-12-31</td>
      <td>0.097591</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2017-12-30</td>
      <td>-0.117812</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2017-12-29</td>
      <td>-0.002695</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017-12-28</td>
      <td>-0.079273</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2017-12-27</td>
      <td>-0.020107</td>
      <td>BTC</td>
    </tr>
  </tbody>
</table>
</div>




```python
#st dev and average of daily return (delta)
top15cor.groupby("coin").agg({np.std, np.mean}) 
top15cor = top15cor.reset_index(drop=True)
top15cor.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Delta</th>
      <th>coin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-12-31</td>
      <td>0.097591</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-12-30</td>
      <td>-0.117812</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-12-29</td>
      <td>-0.002695</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017-12-28</td>
      <td>-0.079273</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-12-27</td>
      <td>-0.020107</td>
      <td>BTC</td>
    </tr>
  </tbody>
</table>
</div>




```python
top15p = pd.pivot_table(top15cor, values= "Delta", columns= "coin", index= "Date")
```


```python
#daily price correlation among coins
top15p = top15p.corr()
top15p = round(top15p, 2)
top15p
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>coin</th>
      <th>ADA</th>
      <th>BCC</th>
      <th>BTC</th>
      <th>BTG</th>
      <th>DASH</th>
      <th>EOS</th>
      <th>ETC</th>
      <th>ETH</th>
      <th>LTC</th>
      <th>MIOTA</th>
      <th>NEO</th>
      <th>XEM</th>
      <th>XLM</th>
      <th>XMR</th>
      <th>XRP</th>
    </tr>
    <tr>
      <th>coin</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ADA</th>
      <td>1.00</td>
      <td>0.07</td>
      <td>0.12</td>
      <td>-0.04</td>
      <td>0.09</td>
      <td>0.11</td>
      <td>0.49</td>
      <td>0.17</td>
      <td>0.13</td>
      <td>0.32</td>
      <td>0.24</td>
      <td>0.18</td>
      <td>0.39</td>
      <td>0.32</td>
      <td>0.40</td>
    </tr>
    <tr>
      <th>BCC</th>
      <td>0.07</td>
      <td>1.00</td>
      <td>0.44</td>
      <td>0.04</td>
      <td>0.13</td>
      <td>0.14</td>
      <td>0.11</td>
      <td>0.22</td>
      <td>0.15</td>
      <td>0.25</td>
      <td>0.06</td>
      <td>0.05</td>
      <td>0.10</td>
      <td>0.18</td>
      <td>0.02</td>
    </tr>
    <tr>
      <th>BTC</th>
      <td>0.12</td>
      <td>0.44</td>
      <td>1.00</td>
      <td>0.11</td>
      <td>0.31</td>
      <td>0.24</td>
      <td>0.35</td>
      <td>0.35</td>
      <td>0.37</td>
      <td>0.40</td>
      <td>0.22</td>
      <td>0.19</td>
      <td>0.22</td>
      <td>0.41</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>BTG</th>
      <td>-0.04</td>
      <td>0.04</td>
      <td>0.11</td>
      <td>1.00</td>
      <td>0.05</td>
      <td>0.01</td>
      <td>0.04</td>
      <td>0.04</td>
      <td>0.04</td>
      <td>0.09</td>
      <td>0.00</td>
      <td>0.06</td>
      <td>-0.04</td>
      <td>0.07</td>
      <td>-0.04</td>
    </tr>
    <tr>
      <th>DASH</th>
      <td>0.09</td>
      <td>0.13</td>
      <td>0.31</td>
      <td>0.05</td>
      <td>1.00</td>
      <td>0.20</td>
      <td>0.28</td>
      <td>0.37</td>
      <td>0.29</td>
      <td>0.32</td>
      <td>0.21</td>
      <td>0.23</td>
      <td>0.14</td>
      <td>0.49</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>EOS</th>
      <td>0.11</td>
      <td>0.14</td>
      <td>0.24</td>
      <td>0.01</td>
      <td>0.20</td>
      <td>1.00</td>
      <td>0.30</td>
      <td>0.38</td>
      <td>0.28</td>
      <td>0.24</td>
      <td>0.23</td>
      <td>0.21</td>
      <td>0.21</td>
      <td>0.25</td>
      <td>0.20</td>
    </tr>
    <tr>
      <th>ETC</th>
      <td>0.49</td>
      <td>0.11</td>
      <td>0.35</td>
      <td>0.04</td>
      <td>0.28</td>
      <td>0.30</td>
      <td>1.00</td>
      <td>0.58</td>
      <td>0.48</td>
      <td>0.48</td>
      <td>0.39</td>
      <td>0.31</td>
      <td>0.23</td>
      <td>0.37</td>
      <td>0.08</td>
    </tr>
    <tr>
      <th>ETH</th>
      <td>0.17</td>
      <td>0.22</td>
      <td>0.35</td>
      <td>0.04</td>
      <td>0.37</td>
      <td>0.38</td>
      <td>0.58</td>
      <td>1.00</td>
      <td>0.35</td>
      <td>0.47</td>
      <td>0.26</td>
      <td>0.26</td>
      <td>0.19</td>
      <td>0.46</td>
      <td>0.11</td>
    </tr>
    <tr>
      <th>LTC</th>
      <td>0.13</td>
      <td>0.15</td>
      <td>0.37</td>
      <td>0.04</td>
      <td>0.29</td>
      <td>0.28</td>
      <td>0.48</td>
      <td>0.35</td>
      <td>1.00</td>
      <td>0.35</td>
      <td>0.27</td>
      <td>0.31</td>
      <td>0.26</td>
      <td>0.36</td>
      <td>0.21</td>
    </tr>
    <tr>
      <th>MIOTA</th>
      <td>0.32</td>
      <td>0.25</td>
      <td>0.40</td>
      <td>0.09</td>
      <td>0.32</td>
      <td>0.24</td>
      <td>0.48</td>
      <td>0.47</td>
      <td>0.35</td>
      <td>1.00</td>
      <td>0.23</td>
      <td>0.39</td>
      <td>0.43</td>
      <td>0.48</td>
      <td>0.19</td>
    </tr>
    <tr>
      <th>NEO</th>
      <td>0.24</td>
      <td>0.06</td>
      <td>0.22</td>
      <td>0.00</td>
      <td>0.21</td>
      <td>0.23</td>
      <td>0.39</td>
      <td>0.26</td>
      <td>0.27</td>
      <td>0.23</td>
      <td>1.00</td>
      <td>0.16</td>
      <td>0.15</td>
      <td>0.15</td>
      <td>0.08</td>
    </tr>
    <tr>
      <th>XEM</th>
      <td>0.18</td>
      <td>0.05</td>
      <td>0.19</td>
      <td>0.06</td>
      <td>0.23</td>
      <td>0.21</td>
      <td>0.31</td>
      <td>0.26</td>
      <td>0.31</td>
      <td>0.39</td>
      <td>0.16</td>
      <td>1.00</td>
      <td>0.24</td>
      <td>0.27</td>
      <td>0.14</td>
    </tr>
    <tr>
      <th>XLM</th>
      <td>0.39</td>
      <td>0.10</td>
      <td>0.22</td>
      <td>-0.04</td>
      <td>0.14</td>
      <td>0.21</td>
      <td>0.23</td>
      <td>0.19</td>
      <td>0.26</td>
      <td>0.43</td>
      <td>0.15</td>
      <td>0.24</td>
      <td>1.00</td>
      <td>0.37</td>
      <td>0.48</td>
    </tr>
    <tr>
      <th>XMR</th>
      <td>0.32</td>
      <td>0.18</td>
      <td>0.41</td>
      <td>0.07</td>
      <td>0.49</td>
      <td>0.25</td>
      <td>0.37</td>
      <td>0.46</td>
      <td>0.36</td>
      <td>0.48</td>
      <td>0.15</td>
      <td>0.27</td>
      <td>0.37</td>
      <td>1.00</td>
      <td>0.16</td>
    </tr>
    <tr>
      <th>XRP</th>
      <td>0.40</td>
      <td>0.02</td>
      <td>0.10</td>
      <td>-0.04</td>
      <td>0.00</td>
      <td>0.20</td>
      <td>0.08</td>
      <td>0.11</td>
      <td>0.21</td>
      <td>0.19</td>
      <td>0.08</td>
      <td>0.14</td>
      <td>0.48</td>
      <td>0.16</td>
      <td>1.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
#heat map shows all coins have a positive correlation 
f,ax= plt.subplots(figsize=(15,15))
sns.set(font_scale = 1.1)
sns.heatmap(top15p, mask= np.zeros_like(top15p, dtype= np.bool),cmap= sns.diverging_palette(220,10,as_cmap= True),square = True, ax=ax) 
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1194c8dd8>




![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_23_1.png)


# 2) Year to Year Growth
  Historical Growth( Year Over Year with Closing Price of Average /Exponential Slope)


```python
# Saving all my sorted_extracted data to the csv file 
top15.to_csv('./top15.to_csv.csv')
```


```python
#Initialize the dataframe with fill in integers(0), so no value will be empty before plotting a chart
# Minor Data Cleanup
YOY_df = pd.DataFrame({"Top15 Coins": ['ADA','BCC','BTC','BTG','DASH',
                                       'EOS','ETC','ETH','LTC','MIOTA',
                                        'NEO','XEM','XLM','XMR','XRP'], 
                                 "2013_Average": [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0], 
                                 "2014_Average": [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
                                 "2015_Average": [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0], 
                                 "2016_Average": [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
                                 "2017_Average": [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0]})

YOY_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2013_Average</th>
      <th>2014_Average</th>
      <th>2015_Average</th>
      <th>2016_Average</th>
      <th>2017_Average</th>
      <th>Top15 Coins</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>ADA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>BCC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>BTG</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>DASH</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Extracting data with Date, Close and Coin for all the historical years[2013, 2014, 2015, 2016, 2017]
#To plot the graph for the year over year growth.
top15 = top15[["Date", "Close", "coin"]]
top15['Date'] = pd.to_datetime(top15['Date'])

mask = (top15['Date'] > '2012-12-31') & (top15['Date'] <= '2017-12-31')
 
top15 = top15.loc[mask]
top15 = top15.reset_index(drop=True)
 
top15.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Close</th>
      <th>coin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-12-31</td>
      <td>14156.4</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-12-30</td>
      <td>12952.2</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-12-29</td>
      <td>14656.2</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017-12-28</td>
      <td>14606.5</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-12-27</td>
      <td>15838.5</td>
      <td>BTC</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Formatting dataframe 
top15_2017 = top15[["Date", "Close", "coin"]]
top15_2017['Date'] = pd.to_datetime(top15['Date'])
mask = (top15_2017['Date'] > '2016-12-31') & (top15_2017['Date'] <= '2017-12-31')
top15_2017 = top15_2017.loc[mask]
top15_2017 = top15_2017.reset_index(drop=True)
top15_2017.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Close</th>
      <th>coin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-12-31</td>
      <td>14156.4</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-12-30</td>
      <td>12952.2</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-12-29</td>
      <td>14656.2</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017-12-28</td>
      <td>14606.5</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-12-27</td>
      <td>15838.5</td>
      <td>BTC</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Creating year over year growth
columns = ['Coin', '2017 Average']
year2017 = pd.DataFrame(columns = columns)

#appending to dataframe
coins = top15_2017.coin.unique()
for coin in coins:
    coin_df = top15_2017.loc[(top15_2017['coin'] == coin)]
    coin_df = coin_df.reset_index(drop=True)
    coin_list = []
    for i, value in enumerate(coin_df['Close'][:-1]):
        coin_list.append(value)
    coin_avg = np.sum(coin_list) 
    sum2017_sum = round(coin_avg, 2)
    sum2017_avg = sum2017_sum/i
    year2017 = year2017.append({'Coin': coin, 
                                              '2017 Average': sum2017_avg},
                                            ignore_index = True)
year2017
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Coin</th>
      <th>2017 Average</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BTC</td>
      <td>4025.355234</td>
    </tr>
    <tr>
      <th>1</th>
      <td>XRP</td>
      <td>0.204904</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ETH</td>
      <td>225.126584</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ADA</td>
      <td>0.129111</td>
    </tr>
    <tr>
      <th>4</th>
      <td>XEM</td>
      <td>0.180882</td>
    </tr>
    <tr>
      <th>5</th>
      <td>LTC</td>
      <td>50.295069</td>
    </tr>
    <tr>
      <th>6</th>
      <td>XLM</td>
      <td>0.034105</td>
    </tr>
    <tr>
      <th>7</th>
      <td>MIOTA</td>
      <td>1.047550</td>
    </tr>
    <tr>
      <th>8</th>
      <td>DASH</td>
      <td>249.619972</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NEO</td>
      <td>15.527741</td>
    </tr>
    <tr>
      <th>10</th>
      <td>EOS</td>
      <td>2.345604</td>
    </tr>
    <tr>
      <th>11</th>
      <td>XMR</td>
      <td>76.281901</td>
    </tr>
    <tr>
      <th>12</th>
      <td>BTG</td>
      <td>45.402754</td>
    </tr>
    <tr>
      <th>13</th>
      <td>ETC</td>
      <td>12.030799</td>
    </tr>
    <tr>
      <th>14</th>
      <td>BCC</td>
      <td>105.383692</td>
    </tr>
  </tbody>
</table>
</div>




```python
# graph individually to see the growth pattern with year over year growth average of the year 2017
#I am plotting the graph for only 2017 because this is the only year has will all the data for top15 coins.

 
plt.style.use('seaborn')
x = np.arange(15)
year2017.plot(kind = 'bar', x = 'Coin', y = '2017 Average', 
                     legend = False, figsize = (20, 10))
plt.ylabel('Average Price', fontsize = 20)
plt.xlabel('', fontsize = 20)
plt.title('2017 Average Closing Price', fontsize = 28)

plt.xticks(fontsize = 17)
plt.yticks(fontsize = 17)
for a,b in zip(x, year2017['2017 Average']):
    b = round(b,2)
    plt.text(a-0.2, b + 1.5, str(b), color='black',fontsize = 15)
plt.show()

# Save the Figure
plt.savefig("2017_Average_Closing_Price.png")
```


![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_30_0.png)



    <matplotlib.figure.Figure at 0x116e32da0>



```python
#Formatting dataframe 
top15_2016 = top15[["Date", "Close", "coin"]]
top15_2016['Date'] = pd.to_datetime(top15_2016['Date'])
mask = (top15_2016['Date'] > '2015-12-31') & (top15_2016['Date'] <= '2016-12-31')
top15_2016 = top15_2016.loc[mask]
top15_2016 = top15_2016.reset_index(drop=True)
top15_2016.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Close</th>
      <th>coin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016-12-31</td>
      <td>963.74</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-12-30</td>
      <td>961.24</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-12-29</td>
      <td>973.50</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-12-28</td>
      <td>975.92</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-12-27</td>
      <td>933.20</td>
      <td>BTC</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Creating volatility for 2016 
columns = ['Coin', '2016 Average']
year2016 = pd.DataFrame(columns = columns)

# appending to dataframe
coins = top15_2016.coin.unique()
for coin in coins:
    coin_df = top15_2016.loc[(top15_2016['coin'] == coin)]
    coin_df = coin_df.reset_index(drop=True)
    coin_list = []
    for i, value in enumerate(coin_df['Close'][:-1]):
        coin_list.append(value)
    coin_avg = np.sum(coin_list) 
    sum2016_sum = round(coin_avg, 2)
    sum2016_avg = sum2016_sum/i
    year2016 = year2016.append({'Coin': coin, 
                                              '2016 Average': sum2016_avg},
                                            ignore_index = True)
year2016
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Coin</th>
      <th>2016 Average</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BTC</td>
      <td>570.422500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>XRP</td>
      <td>0.006923</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ETH</td>
      <td>9.829121</td>
    </tr>
    <tr>
      <th>3</th>
      <td>XEM</td>
      <td>0.003379</td>
    </tr>
    <tr>
      <th>4</th>
      <td>LTC</td>
      <td>3.799918</td>
    </tr>
    <tr>
      <th>5</th>
      <td>XLM</td>
      <td>0.002005</td>
    </tr>
    <tr>
      <th>6</th>
      <td>DASH</td>
      <td>8.079093</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NEO</td>
      <td>0.184732</td>
    </tr>
    <tr>
      <th>8</th>
      <td>XMR</td>
      <td>3.707115</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ETC</td>
      <td>1.252453</td>
    </tr>
    <tr>
      <th>10</th>
      <td>BTG</td>
      <td>0.070000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Formatting dataframe 
top15_2015 = top15[["Date", "Close", "coin"]]
top15_2015['Date'] = pd.to_datetime(top15_2015['Date'])
mask = (top15_2015['Date'] > '2014-12-31') & (top15_2015['Date'] <= '2015-12-31')
top15_2015 = top15_2015.loc[mask]
top15_2015 = top15_2015.reset_index(drop=True)
top15_2015.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Close</th>
      <th>coin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-12-31</td>
      <td>430.57</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015-12-30</td>
      <td>426.62</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-12-29</td>
      <td>432.98</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015-12-28</td>
      <td>422.28</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015-12-27</td>
      <td>422.82</td>
      <td>BTC</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Creating historical data for 2015
columns = ['Coin', '2015 Average']
year2015 = pd.DataFrame(columns = columns)

#Calculating  appending to dataframe
coins = top15_2015.coin.unique()
for coin in coins:
    coin_df = top15_2015.loc[(top15_2015['coin'] == coin)]
    coin_df = coin_df.reset_index(drop=True)
    coin_list = []
    for i, value in enumerate(coin_df['Close'][:-1]):
        coin_list.append(value)
    coin_avg = np.sum(coin_list) 
    sum2015_sum = round(coin_avg, 2)
    sum2015_avg = sum2015_sum/i
    year2015 = year2015.append({'Coin': coin, 
                                              '2015 Average': sum2015_avg},
                                            ignore_index = True)
year2015
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Coin</th>
      <th>2015 Average</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BTC</td>
      <td>273.088678</td>
    </tr>
    <tr>
      <th>1</th>
      <td>XRP</td>
      <td>0.008843</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ETH</td>
      <td>0.936690</td>
    </tr>
    <tr>
      <th>3</th>
      <td>XEM</td>
      <td>0.000147</td>
    </tr>
    <tr>
      <th>4</th>
      <td>LTC</td>
      <td>2.702121</td>
    </tr>
    <tr>
      <th>5</th>
      <td>XLM</td>
      <td>0.002810</td>
    </tr>
    <tr>
      <th>6</th>
      <td>DASH</td>
      <td>2.768017</td>
    </tr>
    <tr>
      <th>7</th>
      <td>XMR</td>
      <td>0.492039</td>
    </tr>
    <tr>
      <th>8</th>
      <td>BTG</td>
      <td>0.154945</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Formatting dataframe 
top15_2014 = top15[["Date", "Close", "coin"]]
top15_2014['Date'] = pd.to_datetime(top15_2014['Date'])
mask = (top15_2014['Date'] > '2013-12-31') & (top15_2014['Date'] <= '2014-12-31')
top15_2014 = top15_2014.loc[mask]
top15_2014 = top15_2014.reset_index(drop=True)
top15_2014.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Close</th>
      <th>coin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014-12-31</td>
      <td>320.19</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014-12-30</td>
      <td>310.74</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2014-12-29</td>
      <td>312.67</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2014-12-28</td>
      <td>317.24</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014-12-27</td>
      <td>315.86</td>
      <td>BTC</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Creating year over year 2014
columns = ['Coin', '2014 Average']
year2014 = pd.DataFrame(columns = columns)

#Calculating volatility values & appending to dataframe
coins = top15_2014.coin.unique()
for coin in coins:
    coin_df = top15_2014.loc[(top15_2014['coin'] == coin)]
    coin_df = coin_df.reset_index(drop=True)
    coin_list = []
    for i, value in enumerate(coin_df['Close'][:-1]):
        coin_list.append(value)
    coin_avg = np.sum(coin_list) 
    sum2014_sum = round(coin_avg, 2)
    sum2014_avg = sum2014_sum/i
    year2014 = year2014.append({'Coin': coin, 
                                              '2014 Average': sum2014_avg},
                                            ignore_index = True)
year2014
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Coin</th>
      <th>2014 Average</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BTC</td>
      <td>528.016474</td>
    </tr>
    <tr>
      <th>1</th>
      <td>XRP</td>
      <td>0.009532</td>
    </tr>
    <tr>
      <th>2</th>
      <td>LTC</td>
      <td>9.831460</td>
    </tr>
    <tr>
      <th>3</th>
      <td>XLM</td>
      <td>0.002721</td>
    </tr>
    <tr>
      <th>4</th>
      <td>DASH</td>
      <td>3.702727</td>
    </tr>
    <tr>
      <th>5</th>
      <td>XMR</td>
      <td>1.562703</td>
    </tr>
    <tr>
      <th>6</th>
      <td>BTG</td>
      <td>1.229107</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Formatting dataframe 
top15_2013 = top15[["Date", "Close", "coin"]]
top15_2013['Date'] = pd.to_datetime(top15_2013['Date'])
mask = (top15_2013['Date'] > '2012-12-31') & (top15_2013['Date'] <= '2013-12-31')
top15_2013 = top15_2013.loc[mask]
top15_2013 = top15_2013.reset_index(drop=True)
top15_2013.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Close</th>
      <th>coin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2013-12-31</td>
      <td>754.01</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2013-12-30</td>
      <td>756.13</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013-12-29</td>
      <td>745.05</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013-12-28</td>
      <td>727.83</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2013-12-27</td>
      <td>735.07</td>
      <td>BTC</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Creating year over year data for 2013
columns = ['Coin', '2013 Average']
year2013 = pd.DataFrame(columns = columns)

# appending to dataframe
coins = top15_2013.coin.unique()
for coin in coins:
    coin_df = top15_2013.loc[(top15_2013['coin'] == coin)]
    coin_df = coin_df.reset_index(drop=True)
    coin_list = []
    for i, value in enumerate(coin_df['Close'][:-1]):
        coin_list.append(value)
    coin_avg = np.sum(coin_list) 
    sum2013_sum = round(coin_avg, 2)
    sum2013_avg = sum2013_sum/i
    year2013 = year2013.append({'Coin': coin, 
                                              '2013 Average': sum2013_avg},
                                            ignore_index = True)
year2013
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Coin</th>
      <th>2013 Average</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BTC</td>
      <td>259.022195</td>
    </tr>
    <tr>
      <th>1</th>
      <td>XRP</td>
      <td>0.013716</td>
    </tr>
    <tr>
      <th>2</th>
      <td>LTC</td>
      <td>6.703130</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BTG</td>
      <td>0.490674</td>
    </tr>
  </tbody>
</table>
</div>




```python
#TRied veryhard and spent couple of days for fillining na, removing empty cells and looping with data structures of mutiple, unfortunately does not work. 
# I did not want to waste anymore time, as I need to do the presentation.

#Creating historical average growth year over year dataframe
#YOY_df # initialized dataframe
#columns = ["Top15 Coins", '2013_Average', '2014_Average','2015_Average','2016_Average','2017_Average']

#YOY_df = pd.DataFrame(columns = columns)
#each_year = []
 
    
# Calculate the Average Scores for each year over year for all Top15 coins
#years = ["2013", "2014", "2015", "2016", "2017"] 
#coins = top15.coin.unique()
 
#dataframe = {'Coins': topcoins, 'Year': years} 
#df = pd.DataFrame(dataframe) 

#for coin in coins:
#   coin_df = top15.loc[(top15['coin'] == coin)]
#    coin_df = coin_df.reset_index(drop=True)
#    coin_list = []
    
#    for year in years: 
#        closeprice_lastday_list = []
#        closeprice_firstday_list = []
#        year_list = []
#        year_percent_list = []
#        year_over = []
#        yoy_coin_list = [] 
#        yoy_avg_list = []

 #       start_date = year + '-01-01'
#        end_date = year + '-12-31'

#        mask = (coin_df['Date'] > start_date) & (coin_df['Date'] <= end_date) & (coin_df['coin'] == coin)
#        #print(mask)
#        #print(coin)
        #print(start_date)
        #print(end_date)
#        year_value = 'sum' + year
#        year_sum = year_value + '_sum'
#        year_avg = year_value + '_avg'
        
        
 #       for i, value in enumerate(coin_df['Close'][:-1]):
            #print(i, value)
#            coin_list.append(value)
            
             
             
#        coin_avg = np.sum(coin_list)
#       #print( i)
#        #print(coin_avg)
#        year_sum = round(coin_avg, 2)
#        year_avg = year_sum/i
#       year_title = year + '_Average'
        
#        each_year.append({'Top15 Coins': coin, 
#                          year_title : year_avg})
                           #ignore_index=True)
 

        # Add each value to the appropriate array
#        yoy_coin_list.append(coin_list)
#        yoy_avg_list.append(each_year)
            
 #    coin_avg = np.sum(coin_list)
    #print( i)
    #print(coin_avg)
#    year_sum = round(coin_avg, 2)
#    year_avg = year_sum/i
    #YOY_df = YOY_df.append({'Top15 Coins': coin, 
                            #year_title : each_year},
                            #ignore_index=True )

 
    
#YOY_df 
#my_list = each_year
#df = pd.DataFrame(np.array(my_list).reshape(15,6), columns = list("abc"))
#print (df)
#df
```

# 3) Historical Volatility


```python
top15 = crypto_df.loc[(crypto_df["coin"]=="BTC")|(crypto_df["coin"]=="ETH")|
                      (crypto_df["coin"]=="LTC")|(crypto_df["coin"]=="MIOTA")|
                      (crypto_df["coin"]=="XRP")|(crypto_df["coin"]=="DASH")|
                      (crypto_df["coin"]=="XEM")|(crypto_df["coin"]=="XMR")|
                      (crypto_df["coin"]=="BTG")|(crypto_df["coin"]=="ETC")|
                      (crypto_df["coin"]=="ADA")|(crypto_df["coin"]=="EOS")|
                      (crypto_df["coin"]=="XLM")|(crypto_df["coin"]=="NEO")|
                      (crypto_df["coin"]=="BCC")
                      ,:]
```


```python
#Formatting dataframe 
top15 = top15[["Date", "Close", "coin"]]
top15['Date'] = pd.to_datetime(top15['Date'])
mask = (top15['Date'] > '2016-12-31') & (top15['Date'] <= '2017-12-31')
top15 = top15.loc[mask]
top15 = top15.reset_index(drop=True)
top15.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Close</th>
      <th>coin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-12-31</td>
      <td>14156.4</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-12-30</td>
      <td>12952.2</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-12-29</td>
      <td>14656.2</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017-12-28</td>
      <td>14606.5</td>
      <td>BTC</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-12-27</td>
      <td>15838.5</td>
      <td>BTC</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Creating historical volatility dataframe
columns = ['Coin', 'Historical Volatility']
volatility_data = pd.DataFrame(columns = columns)

#Calculating volatility values & appending to dataframe
coins = top15.coin.unique()
for coin in coins:
    coin_dataframe = top15.loc[(top15['coin'] == coin)]
    coin_dataframe = coin_dataframe.reset_index(drop=True)
    coin_list = []
    for i, value in enumerate(coin_dataframe['Close'][:-1]):
        coin_list.append(value/coin_dataframe['Close'][i+1] -1)
    coin_stdv = np.std(coin_list)
    annualization_factor = np.sqrt(365)
    volatility_value = round(coin_stdv * annualization_factor, 2)
    volatility_data = volatility_data.append({'Coin': coin, 
                                              'Historical Volatility': volatility_value},
                                            ignore_index = True)
volatility_data.sort_values(by=['Historical Volatility'])
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Coin</th>
      <th>Historical Volatility</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BTC</td>
      <td>0.95</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ETH</td>
      <td>1.40</td>
    </tr>
    <tr>
      <th>11</th>
      <td>XMR</td>
      <td>1.53</td>
    </tr>
    <tr>
      <th>8</th>
      <td>DASH</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>13</th>
      <td>ETC</td>
      <td>1.63</td>
    </tr>
    <tr>
      <th>5</th>
      <td>LTC</td>
      <td>1.66</td>
    </tr>
    <tr>
      <th>14</th>
      <td>BCC</td>
      <td>2.13</td>
    </tr>
    <tr>
      <th>7</th>
      <td>MIOTA</td>
      <td>2.29</td>
    </tr>
    <tr>
      <th>4</th>
      <td>XEM</td>
      <td>2.49</td>
    </tr>
    <tr>
      <th>6</th>
      <td>XLM</td>
      <td>2.65</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NEO</td>
      <td>2.69</td>
    </tr>
    <tr>
      <th>1</th>
      <td>XRP</td>
      <td>2.75</td>
    </tr>
    <tr>
      <th>10</th>
      <td>EOS</td>
      <td>3.19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ADA</td>
      <td>4.13</td>
    </tr>
    <tr>
      <th>12</th>
      <td>BTG</td>
      <td>89.51</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Plotting data
plt.style.use('seaborn')
x = np.arange(15)
volatility_data.plot(kind = 'bar', x = 'Coin', y = 'Historical Volatility', 
                     legend = False, figsize = (20, 10))
plt.ylabel('Historical Volatility Value', fontsize = 20)
plt.xlabel('', fontsize = 20)
plt.title('Crytocurrency Historical Volatility Values (2017)', fontsize = 28)

plt.xticks(fontsize = 17)
plt.yticks(fontsize = 17)
for a,b in zip(x, volatility_data['Historical Volatility']):
    b = round(b,2)
    plt.text(a-0.2, b + 1.5, str(b), color='black',fontsize = 15)
plt.show()
```


![png](Crypto%2BAnalysis.Final_files/Crypto%2BAnalysis.Final_44_0.png)


# 4) A day in the life of a day trader


```python
top15 = crypto_df.loc[(crypto_df["coin"]=="BTC")|(crypto_df["coin"]=="ETH")|
                      (crypto_df["coin"]=="LTC")|(crypto_df["coin"]=="MIOTA")|
                      (crypto_df["coin"]=="XRP")|(crypto_df["coin"]=="DASH")|
                      (crypto_df["coin"]=="XEM")|(crypto_df["coin"]=="XMR")|
                      (crypto_df["coin"]=="BTG")|(crypto_df["coin"]=="ETC")|
                      (crypto_df["coin"]=="ADA")|(crypto_df["coin"]=="EOS")|
                      (crypto_df["coin"]=="XLM")|(crypto_df["coin"]=="NEO")|
                      (crypto_df["coin"]=="BCC")
                      ,:]
```


```python
print("-----------------------ANALYSIS----------------------")
print("")    
print("Two scenarios were analyzed.")
print("")
print("In the first one, a day trader, noticing a large drop in a coin stock value in one day, would buy it right")
print("before the end of that day betting on a possible significant rebound the day after.  In that case, selling it")
print("at a conveient time during the next day, he/she could make a quick gain.")
print("In order to limit the number of stocks to follow, the trader was interested in knowing, among the 15 coin")
print("stock being examined, those with the highest propensity to frequenly have large growth from their daily")
print("opening values.  This was measured in terms of percentage of days when the stock during the day would become")
print("more than 10% higher than at its opening value.")
print("From this analysis, the best coins to do so were BTG, ADA, EOS, and BCC.  For them, one every three or four")
print("days this situation occurs.  Particular attention should be given to BTG, for which this happens an amazing")
print("44% of the days.")
print("")
print("In the second scenario, a day trader would monitor stocks growing excessively during a given day and then short")
print("them right before the closing bell, hoping that the next day they will drop.  By buying them back sometimes the")
print("next day, the trader could make a quick gain on this short sale.")
print("In this case the propensity to fall more than 10% from the opening bell was examined and BTG, ADA, EOS,and NEO")
print("stocks were observed to show this behavior once or twice per trading week.  Particularly BTG was to be paid")
print("close attention, with an amazing 42% probability that this could happen any given day.")
print("")
print("Given BTG particularly extreme intraday volatility, perhaps the trader could just concentrate on this stock,")
print("buying it at the end of rough days, and shorting it towards the end of good days.")
print("Perhaps an analysis of BTG streaks of positive or negative days (analysis not done here) could further help the")
print("trader to decide the right day to choose for these end-of-the-day trades.")
```

    -----------------------ANALYSIS----------------------
    
    Two scenarios were analyzed.
    
    In the first one, a day trader, noticing a large drop in a coin stock value in one day, would buy it right
    before the end of that day betting on a possible significant rebound the day after.  In that case, selling it
    at a conveient time during the next day, he/she could make a quick gain.
    In order to limit the number of stocks to follow, the trader was interested in knowing, among the 15 coin
    stock being examined, those with the highest propensity to frequenly have large growth from their daily
    opening values.  This was measured in terms of percentage of days when the stock during the day would become
    more than 10% higher than at its opening value.
    From this analysis, the best coins to do so were BTG, ADA, EOS, and BCC.  For them, one every three or four
    days this situation occurs.  Particular attention should be given to BTG, for which this happens an amazing
    44% of the days.
    
    In the second scenario, a day trader would monitor stocks growing excessively during a given day and then short
    them right before the closing bell, hoping that the next day they will drop.  By buying them back sometimes the
    next day, the trader could make a quick gain on this short sale.
    In this case the propensity to fall more than 10% from the opening bell was examined and BTG, ADA, EOS,and NEO
    stocks were observed to show this behavior once or twice per trading week.  Particularly BTG was to be paid
    close attention, with an amazing 42% probability that this could happen any given day.
    
    Given BTG particularly extreme intraday volatility, perhaps the trader could just concentrate on this stock,
    buying it at the end of rough days, and shorting it towards the end of good days.
    Perhaps an analysis of BTG streaks of positive or negative days (analysis not done here) could further help the
    trader to decide the right day to choose for these end-of-the-day trades.



```python
# GROWTH FROM OPENING VALUE
    
# Let's imagine to be a day trader who like to wait each days for the last few tradind minutes to buy stocks that
# are falling significantly hoping that the next day they will experience a natural rebound.
# He/she can see in real time the significant decline.  What he/she can't really predict is how well is going to 
# rebound the next day.
# In any case, it would be important for these trader to start concentrating on stocks that more often than others
# grow a lot from their opening value.
# Therefore, among the 15 proposed stocks, we will now established which ones are the one that, for instance, more
# often show a >10% growth during any given day from their opening value.

# To determine this, first we need to insert in the dataframe a column ("GrowthFromOpen") that captures this 
# percentage growth.

top15["GrowthFromOpen"]=100*(top15["High"]/top15["Open"]-1)
top15.head()
```

    /anaconda/lib/python3.6/site-packages/ipykernel_launcher.py:15: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      from ipykernel import kernelapp as app





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Market.Cap</th>
      <th>coin</th>
      <th>Delta</th>
      <th>GrowthFromOpen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1/4/18</td>
      <td>15270.7</td>
      <td>15739.7</td>
      <td>14522.2</td>
      <td>15599.2</td>
      <td>21,783,200,000</td>
      <td>256,250,000,000</td>
      <td>BTC</td>
      <td>0.021512</td>
      <td>3.071241</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1/3/18</td>
      <td>14978.2</td>
      <td>15572.8</td>
      <td>14844.5</td>
      <td>15201.0</td>
      <td>16,871,900,000</td>
      <td>251,312,000,000</td>
      <td>BTC</td>
      <td>0.014875</td>
      <td>3.969769</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1/2/18</td>
      <td>13625.0</td>
      <td>15444.6</td>
      <td>13163.6</td>
      <td>14982.1</td>
      <td>16,846,600,000</td>
      <td>228,579,000,000</td>
      <td>BTC</td>
      <td>0.099604</td>
      <td>13.354862</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1/1/18</td>
      <td>14112.2</td>
      <td>14112.2</td>
      <td>13154.7</td>
      <td>13657.2</td>
      <td>10,291,200,000</td>
      <td>236,725,000,000</td>
      <td>BTC</td>
      <td>-0.032242</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>12/31/17</td>
      <td>12897.7</td>
      <td>14377.4</td>
      <td>12755.6</td>
      <td>14156.4</td>
      <td>12,136,300,000</td>
      <td>216,326,000,000</td>
      <td>BTC</td>
      <td>0.097591</td>
      <td>11.472588</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Next, we can create a series that captures, for each stock, the percentage of trading days in which the growth from 
# the opening value was more than 10%.
# The first step to do this is to count the number of days that each coin was traded.

tradingDays=top15.groupby("coin")["GrowthFromOpen"].count()
# tradingDays
```


```python
# Then, to count the number of days with growth exceeding 10%, we can create a dataframe that contains only these days.

growDays_df=top15.loc[top15["GrowthFromOpen"]>10,:]
# growDays_df.head(20)
```


```python
# In this new dataframe , counting the number of elements for each stock is the same as counting the number of days
# in which that stock has grown more than 10% from its opening value.

growingDays=growDays_df.groupby("coin")["GrowthFromOpen"].count()
# growingDays
```


```python
# Now we can create a list containing, for each stock, the percentage of days in which the growth from opening was
# more than 10%.  Then, we convert this list into a dataframe.

percGrowthDays=growingDays/tradingDays
percGrowthDays_df=pd.DataFrame(percGrowthDays)
# percGrowthDays_df
```


```python
# Sort the dataframe from highest to lowest ratio of growing days.

sortedPercGrowthDays_df=percGrowthDays_df.sort_values(by="GrowthFromOpen",ascending=False)
print("For each coin, the percentage of days when its maximum stock value during the day exceeed its opening value by")
print("more than 10% is shown below.")
sortedPercGrowthDays_df
```

    For each coin, the percentage of days when its maximum stock value during the day exceeed its opening value by
    more than 10% is shown below.





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GrowthFromOpen</th>
    </tr>
    <tr>
      <th>coin</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BTG</th>
      <td>0.435603</td>
    </tr>
    <tr>
      <th>ADA</th>
      <td>0.385417</td>
    </tr>
    <tr>
      <th>MIOTA</th>
      <td>0.281553</td>
    </tr>
    <tr>
      <th>EOS</th>
      <td>0.250000</td>
    </tr>
    <tr>
      <th>BCC</th>
      <td>0.242857</td>
    </tr>
    <tr>
      <th>NEO</th>
      <td>0.227743</td>
    </tr>
    <tr>
      <th>XEM</th>
      <td>0.206931</td>
    </tr>
    <tr>
      <th>XMR</th>
      <td>0.165408</td>
    </tr>
    <tr>
      <th>ETC</th>
      <td>0.164151</td>
    </tr>
    <tr>
      <th>XLM</th>
      <td>0.156926</td>
    </tr>
    <tr>
      <th>ETH</th>
      <td>0.156463</td>
    </tr>
    <tr>
      <th>DASH</th>
      <td>0.144265</td>
    </tr>
    <tr>
      <th>XRP</th>
      <td>0.098452</td>
    </tr>
    <tr>
      <th>LTC</th>
      <td>0.082896</td>
    </tr>
    <tr>
      <th>BTC</th>
      <td>0.040864</td>
    </tr>
  </tbody>
</table>
</div>




```python
# DROP FROM OPENING VALUE
    
# In a similar scenario as explained above, the day trader may also be looking at stocks that have grown excessively
# during a day and, during the last few minutes of trading, decide to short them, hoping that the next day they will
# fall.
# The process of course is similar to the one followed above, except that now we need to test the propensity to fall
# more than 10% from the opening value, as opposed to the one of growing more than 10%.

# Add to dataframe column that tracks daily percentage declines from opening value.
top15["FallFromOpen"]=100*(top15["Low"]/top15["Open"]-1)
top15.head()
```

    /anaconda/lib/python3.6/site-packages/ipykernel_launcher.py:10: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      # Remove the CWD from sys.path while we load stuff.





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Market.Cap</th>
      <th>coin</th>
      <th>Delta</th>
      <th>GrowthFromOpen</th>
      <th>FallFromOpen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1/4/18</td>
      <td>15270.7</td>
      <td>15739.7</td>
      <td>14522.2</td>
      <td>15599.2</td>
      <td>21,783,200,000</td>
      <td>256,250,000,000</td>
      <td>BTC</td>
      <td>0.021512</td>
      <td>3.071241</td>
      <td>-4.901543</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1/3/18</td>
      <td>14978.2</td>
      <td>15572.8</td>
      <td>14844.5</td>
      <td>15201.0</td>
      <td>16,871,900,000</td>
      <td>251,312,000,000</td>
      <td>BTC</td>
      <td>0.014875</td>
      <td>3.969769</td>
      <td>-0.892631</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1/2/18</td>
      <td>13625.0</td>
      <td>15444.6</td>
      <td>13163.6</td>
      <td>14982.1</td>
      <td>16,846,600,000</td>
      <td>228,579,000,000</td>
      <td>BTC</td>
      <td>0.099604</td>
      <td>13.354862</td>
      <td>-3.386422</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1/1/18</td>
      <td>14112.2</td>
      <td>14112.2</td>
      <td>13154.7</td>
      <td>13657.2</td>
      <td>10,291,200,000</td>
      <td>236,725,000,000</td>
      <td>BTC</td>
      <td>-0.032242</td>
      <td>0.000000</td>
      <td>-6.784910</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>12/31/17</td>
      <td>12897.7</td>
      <td>14377.4</td>
      <td>12755.6</td>
      <td>14156.4</td>
      <td>12,136,300,000</td>
      <td>216,326,000,000</td>
      <td>BTC</td>
      <td>0.097591</td>
      <td>11.472588</td>
      <td>-1.101747</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Count the number of days with decline exceeding 10%.

fallDays_df=top15.loc[top15["FallFromOpen"]<-10,:]
fallingDays=fallDays_df.groupby("coin")["FallFromOpen"].count()
fallingDays
```




    coin
    ADA       22
    BCC       46
    BTC       78
    BTG      510
    DASH     139
    EOS       41
    ETC       60
    ETH       89
    LTC      124
    MIOTA     62
    NEO      104
    XEM      147
    XLM      147
    XMR      189
    XRP      108
    Name: FallFromOpen, dtype: int64




```python
# Now we can create a list containing, for each stock, the percentage of days in which the decline from opening was
# more than 10%.  Then, we convert this list into a dataframe.

percFallDays=fallingDays/tradingDays
percFallDays
```




    coin
    ADA      0.229167
    BCC      0.131429
    BTC      0.045534
    BTG      0.418376
    DASH     0.097818
    EOS      0.218085
    ETC      0.113208
    ETH      0.100907
    LTC      0.072388
    MIOTA    0.300971
    NEO      0.215321
    XEM      0.145545
    XLM      0.117694
    XMR      0.142749
    XRP      0.066873
    dtype: float64




```python
percFallDays_df=pd.DataFrame(percFallDays)
percFallDays_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
    <tr>
      <th>coin</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ADA</th>
      <td>0.229167</td>
    </tr>
    <tr>
      <th>BCC</th>
      <td>0.131429</td>
    </tr>
    <tr>
      <th>BTC</th>
      <td>0.045534</td>
    </tr>
    <tr>
      <th>BTG</th>
      <td>0.418376</td>
    </tr>
    <tr>
      <th>DASH</th>
      <td>0.097818</td>
    </tr>
    <tr>
      <th>EOS</th>
      <td>0.218085</td>
    </tr>
    <tr>
      <th>ETC</th>
      <td>0.113208</td>
    </tr>
    <tr>
      <th>ETH</th>
      <td>0.100907</td>
    </tr>
    <tr>
      <th>LTC</th>
      <td>0.072388</td>
    </tr>
    <tr>
      <th>MIOTA</th>
      <td>0.300971</td>
    </tr>
    <tr>
      <th>NEO</th>
      <td>0.215321</td>
    </tr>
    <tr>
      <th>XEM</th>
      <td>0.145545</td>
    </tr>
    <tr>
      <th>XLM</th>
      <td>0.117694</td>
    </tr>
    <tr>
      <th>XMR</th>
      <td>0.142749</td>
    </tr>
    <tr>
      <th>XRP</th>
      <td>0.066873</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sort the dataframe by the second column.
sortedPercFallDays_df=percFallDays_df.sort_values(by=0,ascending=False)
print("For each coin, the percentage of days when its minimum stock value during the days was below its opening value")
print("by more than 10% is shown below.")
sortedPercGrowthDays_df
sortedPercFallDays_df
```

    For each coin, the percentage of days when its minimum stock value during the days was below its opening value
    by more than 10% is shown below.





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
    <tr>
      <th>coin</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BTG</th>
      <td>0.418376</td>
    </tr>
    <tr>
      <th>MIOTA</th>
      <td>0.300971</td>
    </tr>
    <tr>
      <th>ADA</th>
      <td>0.229167</td>
    </tr>
    <tr>
      <th>EOS</th>
      <td>0.218085</td>
    </tr>
    <tr>
      <th>NEO</th>
      <td>0.215321</td>
    </tr>
    <tr>
      <th>XEM</th>
      <td>0.145545</td>
    </tr>
    <tr>
      <th>XMR</th>
      <td>0.142749</td>
    </tr>
    <tr>
      <th>BCC</th>
      <td>0.131429</td>
    </tr>
    <tr>
      <th>XLM</th>
      <td>0.117694</td>
    </tr>
    <tr>
      <th>ETC</th>
      <td>0.113208</td>
    </tr>
    <tr>
      <th>ETH</th>
      <td>0.100907</td>
    </tr>
    <tr>
      <th>DASH</th>
      <td>0.097818</td>
    </tr>
    <tr>
      <th>LTC</th>
      <td>0.072388</td>
    </tr>
    <tr>
      <th>XRP</th>
      <td>0.066873</td>
    </tr>
    <tr>
      <th>BTC</th>
      <td>0.045534</td>
    </tr>
  </tbody>
</table>
</div>



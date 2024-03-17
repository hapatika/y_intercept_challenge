**Update after challenge ended (17 March)** 
After contemplation, I realised why volume and price data would be the right indicator. I apologise for my oversight, and if you would like to consider it, below is the amended code (I did the same thing as before, but with the correct data). I understand that this may not be considered, however I just wanted to correct my oversight. 
```
January_Prices = last[last['date'].str.contains('2021-01')]
January_Prices['weight'] = mkt_cap['weight'].where(mkt_cap['date'].str.contains('2021-01'))
January_Prices['volume'] = volume[volume['date'].str.contains('2021-01')]
January_Prices['amt'] = January_Prices['last']*January_Prices['volume']

January_Prices["shifted"] = January_Prices.groupby('ticker')['last'].shift(1)
January_Prices['shifted_vol'] = January_Prices.groupby('ticker')['volume'].shift(1)
January_Prices['shifted_amt'] = January_Prices['shifted']*January_Prices['shifted_vol']

January_Prices["idx_move"] = (January_Prices['shifted_amt'] - January_Prices['amt'])*January_Prices['weight']


contributors = {'date' : [], 'positive' : [], 'negative' : [] }

for date in January_Prices['date'].unique():
  top_pos_cont = January_Prices.loc[January_Prices['date'] == date].sort_values('idx_move', ascending=False).head(5)
  top_neg_cont = January_Prices.loc[January_Prices['date'] == date].sort_values('idx_move', ascending=True).head(5)
  contributors['date'].append(date)
  contributors['positive'].append(top_pos_cont)
  contributors['negative'].append(top_neg_cont)
```


Points to note : 

1. I used Google Colab for the challenge, hence the drive mount and Colab-speciifc imports at the start. Please ignore the data comprehension part, it is simply some preliminary analysis.
2. In task 2, I evaluated the daily returns at close instead of at open, however the situations are symmetric. The other point of conflict in my methodology might be that I used the market capitallzation instead of the daily stock price, however since index movement is capitalization weighted it seemed that was a better index than stock price and volume, which would have just been an extra step in computation. Also, I thought that the stock pice * volume would be linearly related to the market capitalization so it would be the same relation in the difference. 
3. Some references I used:
   
https://www.investopedia.com/terms/c/capitalizationweightedindex.asp
https://www.hsi.com.hk/eng/resources-education/about-hsi-family
https://www.jpx.co.jp/english/markets/indices/line-up/files/e_cal2_36_indexcalculate.pdf

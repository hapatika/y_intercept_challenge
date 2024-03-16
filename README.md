Points to note : 

1. I used Google Colab for the challenge, hence the drive mount and Colab-speciifc imports at the start. Please ignore the data comprehension part, it is simply some preliminary analysis.
2. In task 2, I evaluated the daily returns at close instead of at open, however the situations are symmetric. The other point of conflict in my methodology might be that I used the market capitallzation instead of the daily stock price, however since index movement is capitalization weighted I thought that was a better index than stock price and volume, which would have just been an extra step in computation. Also, the stock pice * volume would be linearly related to the market capitalization so it would be the same relation in the difference.
3. Some references I used:
   
https://www.investopedia.com/terms/c/capitalizationweightedindex.asp
https://www.hsi.com.hk/eng/resources-education/about-hsi-family
https://www.jpx.co.jp/english/markets/indices/line-up/files/e_cal2_36_indexcalculate.pdf

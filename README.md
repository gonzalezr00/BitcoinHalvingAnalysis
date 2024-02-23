# Halving Events Impact on Block Transaction Fees

# 1.Abstract
This study aims to analyze the dynamics of cryptocurrencies, focusing mainly on Bitcoin, and aims to decipher the relationship between halving events and transaction fees. Miners constantly face trade-offs between mining empty blocks for faster completion or maximizing transaction fees by including more transactions, albeit with a higher time investment. Bitcoin miners' fees, consisting of both a fixed amount of coinbase and transactional fees, illustrate this strategic dilemma. 

This study employs an econometric analysis using ARIMAX models to understand the influence of halving events on transaction fees while controlling for exogenous variables such as transaction count and size. Using event-based segmentation to explore the relationship between miners' fees and confirmation times, crucial to understanding the impact of various events on these variables. This analysis seeks to reveal how these events influence miner fees and transaction confirmation times. This research provides insights into miners' strategic decisions, shedding light on the dynamics that shape cryptocurrency transaction processing within the blockchain.

# 2. Introduction

The research focuses on understanding the impact of halving events on the cryptocurrency market, specifically on the behavior of Bitcoin transaction fees. Existing literature has pointed to the relationship between halving and the value of the Bitcoin market, suggesting that halving the reward for miners can directly influence the supply of Bitcoin and thereby increase its value. However, understanding how these events affect transaction fees remains an underexplored area. Therefore, this research aims to examine the behavior of Bitcoin transaction fees in relation to halving events, using a time series approach, ARIMAX models.

The dataset used for this research spans from the creation of Bitcoin in January 2009 to January 2021, including three halving events. This dataset provides detailed information on key aspects such as block timing, miner rewards, transaction fees, among others. To better understand the implications of halving events on transaction fees, a methodology is employed that divides the data into four distinct segments, analyzing the evolution of fees before, during and after each event.

Preliminary results suggest significant changes in fees before and after halving events, supporting the hypothesis that these events have a noticeable impact on the behavior of transaction fees in the Bitcoin ecosystem.

Understanding how these events affect market dynamics is crucial for investors, financial institutions and users, as it allows them to anticipate and better understand rate fluctuations, thus contributing to more informed decision-making in a financial environment increasingly influenced by blockchain technology and cryptocurrencies. Furthermore, this study provides a solid foundation for future research that could delve deeper into other key aspects of the functioning of the cryptocurrency market.


# 3. Research question and null hypothesis

Does proximity to a halving event create a significant difference in the total block transaction fees? Does transaction fees somehow compensate for the loss in coinbase due to a halving event?

The null hypothesis of this study postulates that there is no significant difference in Bitcoin transaction fees before, during and after halving events. 

The alternative hypothesis suggests that there are statistically significant changes in Bitcoin transaction fees in relation to halving events, implying a noticeable influence on the behavior of transaction fees during these specific periods. 

The analysis seeks to demonstrate whether proximity to halving events translates into significant fluctuations in transaction fees, which would support the alternative hypothesis and highlight the impact of these events on the cryptocurrency market.

Therefore;

H0 : There isn’t a significant fee delta due to proximity to the halving event.

# 4. Brief literature review


In the past few years, many researchers have investigated to seek better understanding of the functioning of cryptocurrencies. As the subject is recent, we see many questions and ambiguities around the development of the crypto market, especially Bitcoin, yet a considerable amount of  phenomena remains unexplained.  

According to Artur Meynkhard in Fair market value of bitcoin: halving effect (2019), a relationship can be established between halving and the market value of Bitcoin. The analysis relies on the fact that reducing the miner’s reward by half can have a direct implication on the bitcoin supply, which then increases the value of bitcoin. We believe our study can provide complementary analysis explaining the effects of such an event on the transaction fees. In other words, the halving events can have multiple effects on bitcoin such as bitcoin price and transaction fees.

Halving events were first introduced by Satoshi Nakamoto, the creator of bitcoin. Thus, the paper only discussed the implications of these events on the supply of the currency, which aimed to reach a point where miner’s reward would only be composed of transaction fees, and the supply of bitcoin would remain unchanged. A state where there would be no inflation. However, the paper did not discuss the implications on the miner’s reaction to these before reaching that state. Our study aims therefore to provide analysis on the previous three halving events which can hopefully provide better understanding of the behavior of miners. 

# 5. Data Description

The dataset used in this study relies on the observation of each block since the creation of bitcoin from 03/01/2009 to 11/01/2021. The dataset covers the three halving events and is sufficient to conduct the study. The data history of bitcoin is public and easily accessible. 

This list describes the fields in the dataset (and their unit):

time: Block timestamp, as set by the miner (Datetime, UTC)
height: Block height (Height)
revenue: Total revenue collected by the miner, that is, sum of outputs of the coinbase transaction. This is equal to the block reward pocketed by the miner (i.e. new bitcoins created) plus total fees collected by the miner. (Satoshi)
fee: Total fees collected by the miner: sum for all transactions (but excluding the coinbase) of the difference between the total input and total output of the transaction. (Satoshi)
tx_count: Number of transactions in the block (including the coinbase) (Number)
base_size: Size of the part of the block which counts against the 1MB (1 million bytes) block size limit. (Byte)
input_count: Total number of inputs of all transactions in the block (Number)
input_value: Total input value of all transactions in the block (Satoshi)
output_count: Total number of outputs of all transactions in the block (including the coinbase transaction) (Number)
output_value: Total output value of all transactions in the block (including the output of the coinbase transaction) (Satoshi)
protocol_block_reward: Block reward as set by the protocol (note: this value is not stored into the block itself; according to the protocol, a block is considered as invalid if the miner tries to collect more than this value) (Satoshi)
difficulty: Block difficulty (Difficulty)

First we will divide the data into four segments, we will use the daily average of the transaction fees to provide our analysis for simplicity. We will conduct an event study for each segment separately and then compare the results. It seems important to mention that in some cases we will be converting the value of transaction fees from satoshi to bitcoin when it’s necessary.  

For the studied period, we have 665568 observations therefore the distribution of the data is quite unique and requires some attention. First of all, we can see that for the first couple of years the transaction fees were zero most of the time, we will take this into account while analyzing the first segment. On the other hand, we also see that the mean is remarkably higher than the median, meaning there are some extremely high values that pull the mean higher, alternatively this joins the fact that there is a high number of observations having a very low value. During our study, we will ignore any observations that might mislead or blur our results. whether it's an extremely high value or the zero observations, for which time window is stated accordingly.


# 6. Methodology

As transactions fee vary from one block to the next one, and each block is created/mined roughly every ten minutes, therefore one could understand transactions fee as a variable that depends on time (block height), and thus use a time series proxy to assess the impact of the halving event. Therefore an ARMA or ARIMA approach is considered.

Nevertheless, it is also important to note that we want to control for exogenous variables like difficulty or block size, that's why we will be using an ARIMAX, in which we will try to understand the time effect while controlling for other variables.

In addition to that, in order to clearly differentiate if there is an impact of the halving effect on the transactions fee, we purpose an ARIMAX model in which we will include 3 positional dummy variables to allow us identify the influence of the data in the coefficients given its position relative to the halving event.

For this, we will divide our data into four data windows, each will include data prior to the halving event and data after the halving event (the last data window will only include data prior to the halving event, as in the sample there are only 3 halving events registered). Thus, each of the data windows will be categorized in four segments; Training (A), Pre - Event (B), Post - Event (C), Training After Event (D). 


The aim of this approach is to establish relationships between the coefficients of dummy variables A, B and C (D variable will be understood as the case where others dummies are 0), and then understand if there’s indeed enough statistic significant to understand a compensation in the transaction fee given the halving effect. For this we will not only interpret the coefficients but also do certain t-tests in order to ensure that statistically the coefficients are different from each other and are not zero either.

Finally, we will test to ensure stationarity and try different models to understand which one fits better the aim of our study, while maintaining being able to understand the mechanics behind it and most importantly contrast its narrative with our own intuition.


Our model:

feet =  + i=1NiExoi+AA +BB + CC + MA(d) + t

where:

feet : Total transaction fee per block (satoshis)
Exoi:  Exogenous variables than will be used in the model, i.e. Size (bytes) and Transaction 
count per block (number)
A, B, C :  Positional dummies representing segments in the corresponding window, i.e. when
A = B = C  = 0 then the block is in segment D
MA(d) :  Number of lags in the moving average part of the model is given by the letter d.

# 7. Results

At first, in order to begin with the time series approach, we decided to run Autocorrelation and Partial-Autocorrelation functions for the variable fee using the entire sample in order to try and have a hint in the high level of the best approach, autoregressive, mobile average or both. 

As we obtain a constant positive autocorrelation function and a geometrically decreasing partial autocorrelation function, it is possible to believe an MA approach to be the best for the entire sample, nevertheless as its possible to see on the autocorrelation function, the more lags we take the better as up to 40 lags have a positive and significant correlation with the independent variable. Therefore, as our approach is not necessarily to predict but instead to assess an impact by the use of positional dummies, we made an initial division to our data trying to see if the shape of these functions holds for each of the segments.


# 7.1. Data Segmentation

In order to create these segments, the data was splitted at first into four by the date of each halving event, i.e. from block 0 to block 210.000 was segment 1, from block 210.000+1 to block 420.000 segment 2, and further from segment to segment. 

Here their respective ACF and PACF:

Segment 1.



As it is possible to appreciate, the behavior of the entire sample does not hold for the first segment, as in this case ACF and PACF are identical, positive and show a 2-lag suggestion. This is due to the fact that at the beginning of bitcoin the first thousands of blocks were mined by very few users with very few transactions and most of them didn’t include any fee, that's why only with this segment its not possible to really discern in between the effect of the halving effect as behavior was significantly affected by the early stage of acceptance of the coin. This is the case as well of the second segment. 

Segment 2.





Segment 3.


Segment 4.


# 7.2. Establishing Event Reaction

Once initial segments were created, we established two very simple models MA(1) and MA(3) and ran them multiple times subtracting observations through every segment, with the idea of plotting its betas and looking for significant changes in them which may potentially be related to the halving events. It is important to notice that a significant change in beta, either positive or negative will state a gain or a loss in the predictivity of the error lags for the case of the Moving Average approach.

Here the results:





As it is possible to see for data windows 1, 2 and 3, there is a significant and abrupt decrease in the Beta at a very specific point in the data, meaning that the explicative power of the lags decreased, therefore indicating a market reaction. This market reaction is very likely to be correlated with an increase in fees as the abrupt change in Betas suggests a market breaker reaction that we can observe in the scatter plots. Nevertheless, for data window 4 this changes as there is not enough proximity for the halving event, then this abrupt change in beta is explained by another event therefore supporting the movements of 1, 2 and 3.

# 7.3 Segment Driven Data Window Creation

Once we establish the possible block from which the market reacted to each halving event we then establish what will be called Pre - Event (B) segment, that goes from the beta significant variation block up to the exact halving event date. This segment’s size varies for each halving event, we noticed that for the first ever halving event the market reacted relatively late as the beta dropped significantly 220 blocks (three and a half days) before the actual halving event, while for the third halving event market’s reaction occurred almost 8.000 blocks (two months) before.

Analogously, we established the Post - Event (C) segment, making it symmetrical in size compared to the Pre - Event (B) segment, this with the intention of equal sized close-to-event segments, under the assumption that market will take a similar time to assimilate the event as it took to predict it, but we acknowledge that this segment size could vary in function of how further the impact should be assessed.

Consecutively, we established the Training After Event (D) segment by selecting an arbitrary amount of blocks for which, under our assumption, the market will already have assimilated the event and will enter a more stable period. The arbitrary amount chosen was 5.000 blocks which is equivalent to roughly one month.

Finally, segment Training (A) was constructed in a more event specific manner, as our data exploration results evidence backed with Bitcoin intuitive narrative, transactions fee had a natural behavior at the beginning of Bitcoin therefore for more than four years fees where basically zero as the usage of the coin was significantly low, therefore the beginning of segment Training (A) for the first halving event was decided to take place once transaction fees passed the threshold of 0.001 bitcoins per block as we can infer a significant use of the coin. Similar cases occurred with other halving events, nevertheless the minimum start for those consecutive events was the end of the previous Training After Event (D) segment.

It is important to note that last data window do not contain an event, therefore one could only state Training (A) and maybe Pre - Event (B) segments if one were to assume a very early estimate of the event, therefore this window it’s only illustrative and mostly used to compare its values with those of the third window that show a more organical behavior as the crypto currency is significantly more mature.

# 7.4. Model and Result Discussion

Once the windows were stated, we run different specifications of our model looking for the best possible model to assess the mentioned impact, here the results;

Models:
feet =  + 1Size+2tx_count +AA +BB + CC + MA(3) + t



Each of the previous models corresponds to the data windows previously established. 

In the first model (1), it is possible to see that the estimated Training (A) coefficient is lower than the estimated Pre - Event (B) coefficient, i.e.
+ A <+ B; which is equivalent to  A < B

Therefore, there is enough statistical evidence to reject the null hypothesis where all estimated coefficients for the positional dummies are similar, this means that the fact of being close to the halving event, creates indeed a higher estimate of the fee, showing the market reaction to the halving event. In addition to that, one could see that once the event occurred our model still estimates a higher coefficient than afterwards we therefore can establish the following relationship:

< + A < + C <+ B

Where, the highest estimated fee occurs at Pre - Event (B), followed by Post - Event (C) , Training (A) and lastly Training After Event (D).

Having in mind that  is the estimated impact of being at the Training After Event (D) segment, it is quite unexpected that the estimated fee is lower than the one at Training (A) segment, nevertheless there are multiple explanations possible as this was the first phase of Bitcoin and its behavior is rather unusual compared to the other windows.

Analogically, for the second data window or second model (2), we find the following relationship:
 + A < + B <+ C<

For this case, dynamics change substantially, as now the model estimations of the fee increases the furthest one goes in height (time), meaning that there are other unobserved components that estimate a bigger transaction fee, this could be explained by the acceptance and higher incorporation of the coin in the market. Nevertheless, one cannot discard that there exists indeed a reaction caused by proximity to the second halving event, creating higher fees that kept on growing even after the event was assimilated, according to our estimations.

In the same way, we find the following relationship for the third halving event window or model (3):

 < + B <+ C< + A

In this case, the relationship is similar to the one present in the second halving event where deltas for B and C are consecutive. Nevertheless, it is important to notice that the difference between the coefficients of A and B is the significantly higher than the one from B to C, i.e.

B-C <A-B

Which suggests a significant anticipation reaction to the third halving event that holds even after the event.

Finally for the last model, one can not draw any significant relationship between the estimated coefficients as data is not sufficiently close to the next halving event and very likely is capturing other exogenous events or characteristics as this model describes a downward sloping tendency of the estimated fees.

As a last remark, it is important to note that the sigma2 is interpreted as the estimated variance of the residuals (or errors) in the model. For which we can observe that its values across all of the models are outstandingly high, meaning that there are multiple data points that significantly discern from the mean on each regression. This is explained in multiple ways, like network congestion which imply higher transaction fees in certain specific points or significant variations in mining nodes or computing power, but principally it is explained by miners who validate transactions to themselves for multiple purposes with exceptionally high transfer fees or more simply mistakes done from specific transactions which most are properly documented.

On the other hand, we controlled for variables like Block Size and Transaction Count, which are highly related to the total transfer fee per block.

For Block Size, as the variable accounts for the total bits in each block, it is normal to expect that the more filled the block is, the more possible total transaction fees are collected, keeping in mind that almost all transactions have a different fee. In this case, it's possible to evidence that this variable’s statistical significance is very high for the first three models (significant at 1%), while it’s not significant for the last one, this as explained is due to the limited amount of data and how far the last data point is to the next halving event.

Lastly, for Transaction Count, one can state that the variable is significant at 1% for all of the models, which means that the number of transactions significance can be possibly due to a frequent average fee per transaction thus explaining the total transaction fee. It is important to highlight that in the third model, the coefficient is negative, stating very likely that the average transaction fee was in its highest while the third halving event occurred.

# 7.5 Testing

T-test for A = B = C (data window 1), 


T-test for A = B = C (data window 2), 


T-test for A = B = C (data window 3),  


T-test for A = 0 (data window 4), 


We then ran a t-test for the coefficients of all of our models to ensure enough statistical difference in between them so that we can reject the null hypothesis where we state that coefficients for A, B and C are identical, and for the last window we ensured that there’s indeed a difference in between the first segment of data and the last.

Stationarity:

Data Window 1:


Data Window 2:


Data Window 3:


Data Window 4:


Finally we ensured that we could not reject stationarity by testing using the Aumented Dicky-Fuller test and we observed that we have sufficient statistical evidence to reject the null hypothesis of the existence of a unitary root, therefore the time series part of our model carries enough information to explain the data.

# 8. Conclusion

The results of this study reveal a significant impact of halving events on Bitcoin transaction fees. There is a clear correlation between proximity to these events and changes in fees, showing a market response as the halving approaches, which influences fees before and after the event.

In addition, we can see that the behavior of transaction fees varies over time, depending on the proximity of halving events. The models constructed indicate significant differences in fare estimates in different time segments, reflecting changes in market dynamics in response to these events.

Differential behavior is observed in the market response to halving events as the cryptocurrency gains wider adoption and consolidates in the financial market. For the approach of the study it is not possible to totally discern the transaction fees expected increase over time from the halving effect, nevertheless it is clear that we do have enough statistical significance to reject that there isn’t a significant fee delta due to proximity to the halving event.

Finally, in order to answer this study’s questions, we can state that indeed there's a significant delta due to proximity of a halving event that indeed compensates the coinbase loss with a diluted increment on the transaction fees that holds after the halving events.


# 9. Bibliography

Satoshi Nakamoto, A Peer-to-Peer Electronic Cash System. 2008.
Meynkhard, Artur. (2019). Fair market value of bitcoin: halving effect. Investment Management and Financial Innovations. 16. 72-85. 10.21511/imfi.16(4).2019.07. 
Financial Econometrics, 2023, Patric Coen, Toulouse School of Management.
Chan JY-L, Phoong SW, Phoong SY, Cheng WK, Chen Y-L. The Bitcoin Halving Cycle Volatility Dynamics and Safe Haven-Hedge Properties: A MSGARCH Approach. Mathematics. 2023; 11(3):698. https://doi.org/10.3390/math11030698


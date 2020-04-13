---
layout: default_articles
mathjax: true
---
[Roadmap Homepage](../articles_index.md)

#  Introduction to Limit Order Books 
*Limit Order Books (Order Books, or LOB) are collection of outstanding limit orders to buy and sell a security on a particular venue. The LOB plays a crucial role in the execution of trades, price-discovery, and is the centre of a variety of market-making strategies. *

![Canyon](canyon.jpg)
*Thomas Moran, The Grand Canyon of the Yellowstone (1872)*


In previous articles, we discussed the bid-ask spread, and how this spread is determed by the use of limit orders set by market-makers. Let's set up a quick example, stock XYZ has the current quote: MID: 100, BID: 99.99, ASK: 100.01. What's missing here is the volume available at the Bid, and Ask. In terms of limit-orders, let's assume there a limit-order to Buy 10 shares at a price of 99.99, and a limit-order to Sell 25 shares at a price of 100.01. We can represent this in a simple *limit order book* display as follows. 

*XYZ -Top of Book*

| Bid Volume | Bid Price | Ask Price | Ask Volume |
|:----------:|:---------:|:---------:|:----------:|
|     10     |   99.99   |   100.01  |     25     |

The bid and ask price that we see above are considered the *top of the book* meaning that they reflect the best prices to buy or sell the security, respectively. Specifically, the highest bid, that is the limit-order to buy the security at the highest price, is called the **Best Bid (BB)**, and the highest ask, that is the limit-order to sell the security at the lowest price, is called the **Best Offer (BO)**.

Now, suppose there are other market-makers and other participants who are willing to buy and sell the security at prices that differ from the Best Bid or Best Offer. For example, there are the  additional limit orders. 

1. Buy 20 XYZ at 99.98
2. Sell 10 XYZ at 100.02
3. Sell 1 XYZ at 100.10

We can add this to our book as follows:

| Bid Volume | Bid Price | Ask Price | Ask Volume |
|:----------:|:---------:|:---------:|:----------:|
|     10     |   99.99   |   100.01  |     25     |
|     20     |   99.98   |   100.02  |     10     |
|     -     |   -  |   100.10  |     1     |


### TODO
1. Market Orders impact on the book - do a simple market order 
2. Market Depth - Compute VWAP
3. Market Imbalance - 
4. Price Impact - buy large shares
5. Relationship to Liquidity - tie back to liquidity 
6. Queues and priorities
7. 

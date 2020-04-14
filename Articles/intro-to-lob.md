---
layout: default_articles
mathjax: true
---
[Roadmap Homepage](../articles_index.md)

#  Introduction to Limit Order Books 
*Limit Order Books (Order Books, or LOB) are collection of outstanding limit orders to buy and sell a security on a particular venue. The LOB plays a crucial role in the execution of trades, price-discovery, and is the centre of a variety of market-making strategies.*

![Canyon](canyon.jpg)   
*The Grand Canyon of the Yellowstone, Thomas Moran (1872)*


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



Now that we have a collection of our limit orders, we can analyze how market orders impact the book. Suppose there was a market order to sell 15 shares. Recall that market orders to sell are executed at the bid. Here's what will happen step by step.

1. Market order arrives to sell 15 shares.
2. 10 shares will get filled at \$99.99, since this is the available volume at that price.
3. The 5 remaining shares will get filled at \$99.98. 

The market order was completely filled! However we note the following:

$$
\begin{align*}
\text{Received from Market Sell} &= 10*(\$99.99) + 5*(\$99.98)\\
&= \$1499.80\\
\text{Price Per Share } &= \frac{1499.8}{15}\\
&= \$99.987
\end{align*}
$$

Thus the price per share recieved for this market order was not the Bid of \$99.99 as in the quote, but rather \$99.987 which is slightly lower! Further more our book now looks like:

| Bid Volume | Bid Price | Ask Price | Ask Volume |
|:----------:|:---------:|:---------:|:----------:|
|     5     |   99.98   |   100.01  |     25     |
|     -     |   -   |   100.02  |     10     |
|     -     |   -  |   100.10  |     1     |


From the book, the new mid price is \$99.995, which is lower than the previous mid! This simple example engenders two very important mechanics of markets.

1. Larger market orders have a price impact, meaning that the price per share received/paid is *worse* than the current quote.
2. Market orders to buy(sell) will result in a lower(higher) mid price, all else being constant. 

From our first article, "What is a Market Maker" we looked at an example of how one pays the bid-ask spread when buying or selling a stock immediately. Let's re-examine a similiar example now, expect incorporating price impact. 

First we reset the book:

 Bid Volume | Bid Price | Ask Price | Ask Volume |
|:----------:|:---------:|:---------:|:----------:|
|     20     |   99.99   |   100.01  |     25     |
|     10     |   99.98   |   100.02  |     25     |
|     10     |   99.97   |   100.03  |     15     |
|     5     |   99.96   |    100.05 |     10     |
|     5     |   99.90   |   100.10  |     25     |
|     1     |   99.00   |   -  |     -     |

Again, the quote is: MID \$100.00, BID: \$99.99, ASK: \$100.01.
You are now going to buy, and then sell 50 shares immediately. Let's calculate the cashflows.

$$
\begin{align*}
\text{Paid for Buy} &= 25*(\$100.01) + 25*(\$100.02)\\
&= \$5000.75\\
\text{Paid Per Share } &= \frac{5000.75}{50}\\
&= \$100.015\\\\
\text{Received for Sell} &= 20*(\$99.99) + 10*(\$99.98) + 10*(\$99.97) + 5*(\$99.96) + 5*(\$99.90)\\
&= \$4998.60\\
\text{Paid Per Share } &= \frac{4998.6}{50}\\
&= \$99.972\\\\
\text{Spread per Share} &= 100.015 - 99.972\\
&= 0.043
\end{align*}
$$

In this example, we see that we have price impacts on both sides of our trades, where we paid \$100.015 per share for our buy market order and recieved \$99.972 per share for our sell market order. We note that the price impact on our sell order was greater than the price impact than our buy order (think of impact as difference from original bid/ask). We note that the spread paid per share is roughly \$0.04 as opposed to our original example where the bid-ask spread was \$0.01! 

Now, imagine instead of 50 shares, it was 1000 shares, or even 100,000 shares, as is often the case with institutional traders (banks/pension plans/hedge funds etc). It's clear why understanding limit-order book dynamics is imperative for ensuring that your trade is executed in a timely, and cost efficient manner. In another article, I will discuss more sophisticated execution strategies. 



 ### Coming soon for this article: 
1. Orderbook Imbalance 
6. Queues and priorities

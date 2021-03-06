---
layout: default_articles
mathjax: true
---

#  Price Discovery Process 
*Price discovery is the process in which a securities' price is determined through the interactions and mechanisms in a marketplace.* 

![CHECKERS](checkers.jpg)
*Checkers, Normal Rockwell (1928)*
<hr>

In the previous article about Liquidity and Microstructure, we introduced microstructure as the study of how prices are formed. The process of prices being formed is called the price-discovery process, and it is one of the main functions of a marketplace! What goes into the price discovery process in reality is incredibly complex, as it involves the minute details of specific exchanges, the type of traders who are trading, the availble public (or even private) news, and much more. 

That being said, price discovery remains a key focus of academic literature that intersects economics and mathematics. There are several canonical models in the price discovery process - each with varying levels of complexity as well as specific sets of assumptions. While these models may be a far cry from the complexity of real-world trading, studying the behavior of prices in these models help traders better understand the markets in which they trade. In this article I hope to outline several of these models in varying levels of details, starting with the essential Glosten Milgrom Model. For this model, I will dive into the mathematical deriviations of key results. 

## Glosten Milgrom (1985)

We start with a simple framework, as follows:

####  Setup 
1. There is a single security that has a fair value of one of two possible values, $V_H$ with probability $\theta$ or $V_L$ with probability $(1-\theta)$ where $V_H > V_L$. 

2. Currently,before any market orders are observed, it is trading at $V_0$ which is the expected value computed as follows:
$$
\begin{align*}
V_0 &=  \theta V_H+ (1-\theta) V_L\\
\end{align*}
$$
3. There will be a single order for one share that will arrive at time *t*. This sort of setup is used in various *One Period Models*
 
4. There are two types of traders placing these orders, an *informed trader* who knows what the true value of the security, and a *liqudity trader* who has no knowledge of the true value.

5. The probability that any given order comes from an informed trader is $\pi$ and coversely the probability that any given order froms a liquidity trader is $1-\pi$. 

6. If the fair value of the security is $V_H$, the informed trader will buy with probabililty 1, and sell with probability 0 (and vice-versa if the price of the security is $V_L$.)
 
7. Regardless of fair value, a liquidity trader will buy and sell with probability 0.5.

8. The market maker responsible for quoting the bid and the ask prices is *risk neutral*

#### Order Flow and Fair Value
Given this  setup, we can start analying how order flow affects a market maker's quotes. We start with the following dynamic. 

$$
\begin{align*}
a_t &= V_t^+ = E(V|d_t = +1) \\
b_t &= V_t^- = E(V|d_t = -1)
\end{align*}
$$

Where $a_t$ and $b_t$ reflect the Ask and Bid respectively, and $d_t$ represents the direction of an order, where +1 represents a *Buy* and -1. Here we see that the ask represents the market maker's expected fair value of the security, given that they reveived a buy order, and vice-versa for the bid. Let's look at finding closed form representations of these expected values. 

We start by looking at the conditional probability that the fair value of the security is $V_H$ given that we see a Buy order.

$$
\begin{align*}
P(d_t = 1 | V_H) &= P(d_t=1 | V_H \cap \text{Inf})P(\text{Inf}) \\
&+(d_t=1 | V_H \cap \text{Liq})P(\text{Liq})\\
&= \pi + \frac{1-\pi}{2}\\
&= \frac{1+\pi}{2}
\end{align*}
$$

Following a similiar computation, we see that the probability of a Buy order given that the fair value is $V_L$ is just 
$$\begin{align*}
P(d_t = 1 | V_L)=\frac{1-\pi}{2} 
\end{align*}$$ since the probability that the informed trader buys when the fair value is $V_l$ is simply 0. This simple relationship engenders an import fact about this model, and one that has strong real world implications.

**Order flow has a positive correlation with value.** This means that if we see a sequence of Buys, the fair value of a security is more likely to be higher than its current value. Conversly, we expect a lower fair value given we observe a sequence of sell orders. 

#### Finding the Bid-Ask Spread from the Glosten Milgrom Model. 

Now that we know order flow is possitively correlated with value, how can market-maker's use this information to determine their bid-ask quote? I turn your attention back to point 8 in our framework setup where we specified that the marker-maker's are risk neutral. This means that the market-makers expects to break-even, i.e make 0 profit, on average! 

Suppose that an Buy order is sent in, getting executed at the market-maker's Ask quote. Either this buy was sent by an informed trader in which the market-maker can expect to lose $a_t - V_H$, since the informed trader would only buy if the fair value was $V_H$. On the other hand, if this buy order was sent in by a liquidity trader, , then the market-maker doesn't gain any more insight as to whether the fair is $V_H$ or $V_L$, so on average they can expect to make $a_t - V_0$ off of liquidity traders. The expected profit gained from trading with liquidity traders needs to offset the expected losses from trading with informed traders. Using this, we can find a closed form solution for $a_t$. In the below prood, let $E(\text{Prof}_B)$ be the expected value for profit given a buy order, $\text{Inf}$ represent informed trade, $\text{Liq}$ represent liquidity.

$$
\begin{align*}
E(\text{Prof}_B) &= E(\text{Prof}_B | \text{Inf})P(\text{Inf}) + E(\text{Prof}_B | \text{Liq})P(\text{Liq}) \\
&= \theta \pi (a_t - V_H) + \frac{1}{2}(1-\pi) (a_t - V_0)\\
\end{align*}
$$

Setting the expected profit to 0, and rearranging we find the following. 
$$
\begin{align*}
a_t(\theta \pi + (1-\pi)\frac{1}{2}) &=  \theta \pi V_H + (1 - \pi)\frac{1}{2}V_0\\
\end{align*}
$$

Now, there are alot of ways to rearrange the above to solve for $a_t$ but using some lookahead bias (since I know what closed form answer we hope to get), let's find an expression for $a_t$ that is in the form of $V_0 + \text{some half-spread term}$. In the next stage of the proof, we make use of point 2 in our framework, where we stated $V_0 = \theta V_H + (1- \theta V_L)$

$$
\begin{align*}
a_t(\theta \pi + (1-\pi)\frac{1}{2}) &=  \theta \pi V_H + (1 - \pi)\frac{1}{2}V_0\\
&= \theta \pi V_H + (1 - \pi)\frac{1}{2})V_0 + \theta \pi V_H  - \theta \pi V_H\\
&= \theta \pi (V_H - V_0)+ (\theta \pi + (1 - \pi)\frac{1}{2})V_0 \\
a_t &= V_0 + \frac{\theta \pi}{\theta \pi + (1-\pi)\frac{1}{2}} (V_H - V_0)\\
&= V_0 + \frac{\theta \pi}{\theta \pi + (1-\pi)\frac{1}{2}} (V_H - \theta V_H + (1-\theta)V_L)\\
a_t &= V_0 + \frac{\theta \pi (1 - \theta)}{\theta \pi + (1-\pi)\frac{1}{2}} (V_H - V_L)\\
\end{align*}
$$

Similiarly, we can find a closed form solution for $b_t$ as:

$$
\begin{align*}
b_t &= V_0 - \frac{\theta \pi (1 - \theta)}{\theta \pi + (1-\pi)\frac{1}{2}} (V_H - V_L)\\
\end{align*}
$$

In the special case that we assign equal probabilty to $V_H$ and $V_L$, that is, $\theta = 0.5$ we can collapse the expressions for $a_t$ and $b_t$ as follows:

$$
\begin{align*}
b_t &= V_0 - \frac{\pi}{2} (V_H - V_L)\\
a_t &= V_0 + \frac{\pi}{2} (V_H - V_L)\\
S_t &= (a_t - b_t) = \pi(V_H - V_L)
\end{align*}
$$

Where S represents the spread. **In conclusion**, the Glosten-Milgrom model is a very simple, but powerful model that shows how one can go from a basic set of assumptions about the market maker and trader behaviour, and end with a closed form model to determine bids and asks! 
-Write about what the equations mean at a high level

Next I will briefly outline a few more models that are much more complex, but will spare the mathematical derivations. If the Glosten Milgrom model was interesting, I urge you to check out Market Liquidity by Thierry Foucalt, Marco Pagaano, Ailsa Roell. 

- Kyles Model, description only 
- Ho-Stoll description and result
- Amihud Medelson
- Inventory Models

<hr>
### References
- [Glosten, Milgrom, 1985, "Bid, ask and transaction prices in a specialist market with heterogeneously informed traders](https://www.sciencedirect.com/science/article/abs/pii/0304405X85900443y)


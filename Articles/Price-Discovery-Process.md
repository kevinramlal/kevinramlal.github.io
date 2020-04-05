---
layout: default
mathjax: true
---
[Kevin Ramlal Homepage](https://kevinramlal.github.io)


#  Price Discovery Process 
*Price discovery is the process in which a securities' price is determined through the interactions and mechanisms in a marketplace.* 

There are several important models in the price discovery process - each with varying levels of complexity as well as specific sets of assumptions. While these models may be a far cry from the complexity of real-world trading, studying the behavior of prices in these models help traders better understand the markets in which they trade. In this article I hope to outline several of the canonical models used through literature - and perhaps provide some insight as to why these models can be useful in real applications. 

### 1. Glosten Milgrom (1985)

We start with a simple framework, as follows:

####  Setup 
1. There is a single security that has a fair value of one of two possible values, $V_H$ with probability $\theta$ or $V_L$ with probability $(1-\theta)$ where $V_H > V_L$. 

2. Currently,before any market orders are observed, it is trading at $V_0$ which is the expected value computed as follows:

$$
\begin{align}
V_0 =  \theta V_H+ (1-\theta) V_L
\end{align}$$.

3. There will be a single order for one share that will arrive at time *t*. This sort of setup is used in various *One Period Models*
 
4. There are two types of traders placing these orders, an *informed trader* who knows what the true value of the security, and a *liqudity trader* who has no knowledge of the true value.

5. The probability that any given order comes from an informed trader is $\pi$ and coversely the probability that any given order froms a liquidity trader is $1-\pi$. 

6. If the fair value of the security is $V_H$, the informed trader will buy with probabililty 1, and sell with probability 0 (and vice-versa if the price of the security is $V_L$.)
 
7. Regardless of fair value, a liquidity trader will buy and sell with probability 0.5.

8. You are the market maker responsible for quoting the bid and the ask prices. Furthermore you are *risk neutral*

Given this  setup, we can start analying how order flow affects a market maker's quotes. We start with the following dynamic. 
$$
\begin{*align}
a_t & = V_t^+ = E(V|d_t = +1) \\
b_t & = V_t^- = E(V|d_t = -1)
\end{*align}
$$
Where $a_t$ and $b_t$ reflect the Ask and Bid respectively, and $d_t$ represents the direction of an order, where +1 represents a *Buy* and -1. Here we see that the ask represents the market maker's expected fair value of the security, given that they reveived a buy order, and vice-versa for the bid. Let's look at finding closed form representations of these expected values. 

We start by looking at the conditional probability that the fair value of the security is $V_H$ given that we see a Buy order.

$$
\begin{*align}
P(d_t = 1 | V_H) &= P(d_t=1 | V_H, \text{informed trade})P(\text{informed trade}) \\
&+(d_t=1 | V_H, \text{liqudity trade})P(\text{liquidity trade})\\
&= 1*\pi + \frac{1-\pi}{2}\\
&= \frac{1+\pi}{2}
\end{*align}
$$
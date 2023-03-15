---
description: Liquidity Safety Conditions
---

# Virtual Balances

## Introduction

To guarantee the safety of the pool, there are some conditions which need to be fulfilled when adding liquidity to KyberSwap Classic pools:

1. After LP contributions, the token price remains unchanged.
2. $$P_{min}$$ and $$P_{max}$$ are also unchanged after LP contributions.

In KyberSwap, the pool for pair X-Y needs to maintain 4 parameters:

1. The initial amount of token $$X$$ that is used for amplification, denoted by $$x_0​$$
2. The initial amount of token $$Y$$ that is used for amplification, denoted by $$y_0​$$
3. The change in token $$X$$ amount after trading activities, denoted by $$Δx_0​$$
4. The change in token $$Y$$ amount after trading activities, denoted by $$Δy_0​$$

Therefore, the real balances and virtual balances of the reserves are:

`Real Balances`

$$
x = x_0 + \Delta x_0 \\
  y = y_0 + \Delta y_0
$$

`Virtual Balances`

$$
x' = a \cdot x_0 + \Delta x_0 \\
  y' = a \cdot y_0 + \Delta y_0
$$

where $$a$$ is the [amplification factor](dynamic-pricing-curves.md#amplification-factor-amp). \


The constant product $$x' \cdot y' = (a \cdot x_0 + \Delta x_0) \cdot (a \cdot y_0 + \Delta y_0) = k'$$. Note that $$P_{min}$$ and $$P_{max}$$ at this time are:

$$
\begin{cases}
  P_{min} = \cfrac{(y_0 \cdot a - y_0)^2}{k'} \\
  \\
  P_{max} = \cfrac{k'}{(x_0 \cdot a - x_0)^2}
\end{cases}
$$

The current price: $$P = \cfrac{y'}{x'} = \cfrac{a \cdot y_0 + \Delta y_0}{a \cdot x_0 + \Delta x_0}$$

Liquidity Providers have to contribute in the same proportion for all 4 amount types. We denote the contribution ratio to be $$b$$. LPs have to contribute $$x_1 + \Delta x_1$, $y_1 + \Delta y_1$$in which:

$$
\begin{cases}
  x_1 = b \cdot x_0 \\
  \Delta x_1 = b \cdot \Delta x_0 \\
  y_1 = b \cdot y_0 \\
  \Delta y_1 = b \cdot \Delta y_0
\end{cases}
$$

The real balances and virtual balances of the reserve after contribution are:

`Real Balances`

$$
x = (x_0 + x_1) + (\Delta x_0 + \Delta x_1) = (b + 1) \cdot (x_0 + \Delta x_0) \\
  y = (y_0 + y_1) + (\Delta y_0 + \Delta y_1) = (b + 1) \cdot (y_0 + \Delta y_0)
$$

`Virtual Balances`

$$
x' = a \cdot (x_0 + x_1) + (\Delta x_0 + \Delta x_1) = (b + 1) \cdot (a \cdot x_0 + \Delta x_0) \\
  y' = a \cdot (y_0 + y_1) + (\Delta y_0 + \Delta y_1) = (b + 1) \cdot (a \cdot y_0 + \Delta y_0)
$$

The constant product, after the LP contribution, becomes:

$$
x' \cdot y' = (b + 1)^2 \cdot (a \cdot x_0 + \Delta x_0) \cdot (a \cdot y_0 + \Delta y_0)
= (b + 1)^2 \cdot k'
$$

$$P_{min}$$ and $$P_{max}$$ at this time are:

$$
\begin{cases}
  P_{min} = \cfrac{((y_0 + y_1) \cdot a - (y_0 + y_1))^2}{(b + 1)^2 \cdot k'} = \cfrac{(y_0 \cdot a - y_0)^2}{k'} \\
  P_{max} = \cfrac{(b + 1)^2 \cdot k'}{((x_0 + x_1) \cdot a - (x_0 + x_1))^2} = \cfrac{(x_0 \cdot a - x_0)^2}{k'}
\end{cases}
$$

The current price is updated to be $$P = \cfrac{y'}{x'} = \cfrac{(a \cdot y_0 + \Delta y_0) \cdot (b + 1)}{(a \cdot x_0 + \Delta x_0) \cdot (b + 1)} = \cfrac{a \cdot y_0 + \Delta y_0}{a \cdot x_0 + \Delta x_0}$$

We see that after LP contributes, the current price, $$P_{min}$$ and $$P_{max}$$ are unchanged. It is similar in the case of LPs withdrawals, where the ratio $$b$$ is negative.

## Example[​](https://docs.kyberswap.com/Classic/overview/adding-liquidity-in-kyberswap#example) <a href="#example" id="example"></a>

* Initially, the first LP put 100 $$X$$ and 100 $$Y$$ to the reserve, we have: $$x = 100, y = 100, \Delta x = 0, \Delta y = 0$$.
* A user trades 20 $$X$$ for 15 $$Y$$, so we have the updated parameters: $$x = 100, y = 100, \Delta x = 20, \Delta y = −15$$.
*   Suppose an LP wants to contribute 20% of the current token amounts in the pool, so he should deposit:

    $$
    0.2 · 100 + 0.2 · 20 = 24 (X) \\
      0.2 · 100 + 0.2 · (−15) = 17 (Y)
    $$

ie. deposit 24X and 17Y tokens.

The parameters are then updated to be: $$x = 120$, $y = 120$, $\Delta x = 24$, $\Delta y = −18$$.

---
description: Aggregated Amplified Price Curves
---

# Technical Comparison

## Elastic vs Classic[​](https://docs.kyberswap.com/overview/motivation#comparison-with-kyberswap-classic): Price curve implementation <a href="#comparison-with-kyberswap-classic" id="comparison-with-kyberswap-classic"></a>

In general, KyberSwap Classic can be represented as follows:

$$
\alpha x_0 \cdot  \alpha y_0 = L^2
$$

Where:

* alpha is the amplification factor
* L is the liquidity
* p\_max, p\_min will be the price max, min that KyberSwap Classic can support.

The current price p\_r can be calculated as follows:

$$
p_{max}=\frac{y'{max}}{x'{min}}=\frac{\alpha ^2}{(\alpha-1)^2} \cdot p_{r}
$$

$$
p_{min}=\frac{(\alpha-1)^2}{\alpha^2}\cdot p_{r}
$$

$$
\Rightarrow p_r=\sqrt{p_{max} \cdot p_{min}}
$$

From the price min, max and liquidity, we can represent the invariant equations of two reserves x,y in a KyberSwap Classic pool as follows:

$$
(x+\frac{L}{\sqrt{p_{max}}})(y+L \cdot \sqrt{p_{min}})=L^2
$$

Hence, the representation of KyberSwap Classic can be transformed from the original:

$$
(L,p_r,\alpha) \Rightarrow \begin{cases}L : Liquidity \\p_{r} : Reference  \quad price \\\alpha : Amplification  \quad factor \\\end{cases}
$$

to a new one:

$$
(L,p_{max},p_{min}) \Rightarrow \begin{cases}L : Liquidity \\p_{max} : Max \quad price  \quad supported\\p_{min} : Min  \quad price  \quad supported \\\end{cases}
$$

The following figure illustrates an example of the KyberSwap Classic curve:

![KyberSwap Classic Curve](https://docs.kyberswap.com/assets/images/Kyber-Classic-Curve-5f78b007d617e3290dee6618cbad3cec.png)

### Aggregated KyberSwap Classic[​](https://docs.kyberswap.com/overview/motivation#aggregated-kyberswap-classic) <a href="#aggregated-kyberswap-classic" id="aggregated-kyberswap-classic"></a>

In the early version, KyberSwap Classic allows people to add liquidity in a specific price range. However, this approach has a drawback: the liquidity provider has to add liquidity to a pre-defined range in a pool or create a pool with high gas cost. In KyberSwap Elastic, we want to aggregate different KyberSwap Classic pools into one single pool. In general, two KyberSwap Classic pools can be represented as:

$$
(L_1,p_{r_{1}},\alpha_1);(L_2,p_{r_{2}},\alpha_2)
$$

If the two price ranges do not have any overlap range, the combined reserves curve includes two parts. Otherwise, in the overlap price range, the liquidity equal is the sum of liquidity in two positions. Let's take an example when we have:

$$
p_{max_1} \geq p_{max_2} > p_{min_2} \geq p_{min_1}
$$

The liquidity in different price ranges are:

$$
(L_1,p_{max_{1}},p_{max_{2}})\\(L_1+L2,p_{max_{2}},p_{min_{2}})\\(L_1,p_{min_{2}},p_{min_{1}})
$$

The following figure illustrates how we aggregate liquidity in the three price ranges, where the blue line show the overlap price range, where the liquidity is the sum of liquidity in two positions.

![Aggregated Liquidity](https://docs.kyberswap.com/assets/images/Aggregated-Liquidity-25383b45f22d03aeb82dd724c90caf24.png)

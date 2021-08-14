# Notes on Barclays report regarding U.S Retail Options Trading Strategy

<b>I've just begun to work at an asset management company as a quant in Seoul, South Korea. I do not, and cannot provide any 
financial advices in this post. This is just my note on particular subject. If you want additional and more accurate information, 
please see the reference below.</b>

Reference
* Impact of Retail Options Trading, Barclays Equity Research, 14.09.2020
* Implied Volatility, Investopedia
* Delta hedge, Investopedia
* Straddle, Investopedia
* The Barclays Trading Strategy that Outperforms the Market, Benjamin(Youtube Channel)

<em>Note: The last youtube video is great. With a touch of pessimism, great meme use, and an insight regarding the market, 
the channel owner is talking about the same report, I recommend go watch it.</em> 

## Strategy
Barclays offer 2 strategies.

1. Monetizing elevated volatility using selective VolScore based short delta hedged straddles on single stocks
2. Buying outright call spreads and call 1x2s on Resilient stocks to monetize extremely flat skew and attractive VRP.

Uh huh..
### 1.  Deciphering Strategy no.1
Keywords are

* <b>VolScore</b>: metrics used by Barclays. Uses Stock-sector implied volatility and the implied <em>adjusted</em> realized volatility spread.
Why use adjusted realized volatility? Because Barclays believe it can be impacted by large, unsustainable movements for single stocks.

* <b>Straddle</b>: Simultaneous purchase of options to buy both calls and puts with (1) same expiration, (2) same strike price,
  (3) same underlying. 

* <b>Delta hedge</b>: Offsetting the delta risk by buying or selling equivalent amount of stocks or ETF shares. In option delta
measures how much the option is exposed to the shifts of the underlying asset.

<p>
<b>Straddle</b> makes money regardless of their direction, because it buys both calls and puts.
Instead, they make money regarding the volatility of the stocks. 
If one buys straddle, and the price stays relatively stable, he/she loses money.
</p>

<p>
The Barclays is claiming that they are <b>shorting volatility</b>, which means they are willing to bet on the fact that the 
volatility would go down at some point. They are looking for stocks that has big VRPs, which mean a wide
spread between implied volatility and realized volatility. 
And they are choosing these stocks based on the <b>VolScore metrics</b>. 
Barclays doesn't give us the exact formula, but the youtube vid I mentioned about is speculating that the Barclays is 
betting that the overblown company's volatility would soon revert back to sector volatility.
</p>

### 2. Deciphering Strategy no.2
Keywords are

* <b>Call 1x2s</b>: Call spread strategy. 1x2 ratio vertical spread is created by buying one <em>lower-strike call</em>(ITMs), 
and selling two <em>higher strike calls</em>(OTMs).

* <b>Resilient Names</b>: Stocks that quickly reacquires its particular course after a large amount of order. Large amount
of order can temporarily disrupt the stock prices. For example after a large amount of sell order can drop the stock price. 
Resilient stocks quickly recovers from the such drop. 

<p>
This means buying a long call, and selling OTMs on stocks where implied and realized volatility have converged(low VRP).
</p>


## Logic behind these strategies
### 1. Increase in single stock option trade volume
<p>
Single stock option volumes have increased 3x on a year to year basis.
The increase is concentrated in these three activities:
</p>

1. <b>short dated(<2weeks)</b>
2. <b>calls</b>
3. <b>large-capital tech stocks</b>

<p>
This traits indicates this is speculative intraday activity
</p>

### 2. Increase in volume is caused by retail investors
<p>
Proof:
</p>

1. The spike in volume coincides with commission cost cuts by major <em>retail brokerages</em>.
2. Buying small lot call options.


### 3. Increase in trading impacted volatility for affected 'stocks'
<p>
Implied volatility for shorter dated calls has increased compared to puts or longer dated options. 
However, volatility risk premium has not increased meaningfully.
</p>

1. Volatility risk premium: Difference between 'Implied Volatility' and predicted 'Realized Volatility'
2. Implied Volatility: Volatility gained by backward-calculating Black-Scholes model using 5 observable data.(Other ways are available)
3. Realized Volatility: In a pre-defined time period, one can assess the variation of returns for a particular asset.

<p>
With increase in Implied Volatility, and relatively stable Volatility risk premium, it can be assumed that realized volatility 
increased as well. 
</p>

### 4. Option activity is large enough to potentially impact the underlying assets
<p>
Stocks with large increase in option volumes have outperformed because of better fundamentals. However, in this case 
the call option demand has exaggerated the movement. 
</p>

<p>
Buying call options causes the market makers to hedge their position to neutralize their risk.
Barclays claims that ~30% of the stock volume were result of this, and show increased correlation of stock returns with normalized
option volume of this year.
</p>

* Gamma Squeeze: (More on this later)

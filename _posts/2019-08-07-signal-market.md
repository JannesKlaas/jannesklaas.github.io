# Adventures on the signal market
I have been thinking about a market for signals predicting security payoffs for a while. Interestingly, there was not really one, until regulators tried to force the industry to create one with MIFID II, which did not really work. There is however a fairly big market for data which can be mined into signals. **This is a sketch of a model aiming to explain why there data market looks the way it does, comments are welcome!**

**Abstract**: In a market for information about security payoffs, the value of the information depends on how many investors it is sold to. As information can be copied costlessly and privately, buyers and sellers of information can not contract on exclusivity. Therefore, no market for information can exist, unless some degree of sophistication is required so that not all investors can make use of the information.

## Introduction
Investment funds are in many ways vertically integrated businesses that do many things that have little to do with each other: They employ analysts who form opinions about future developments and how they affect security prices. In quantiative funds these opinions are called signals, which is the term used throughout this text. The fund places bets on those signals, and needs to employ a number of other functions (lawyers, sales people, risk managers, etc.) to run the fund itself. Many of these functions can be outsourced: Specialized fund marketing firms for instance can help raise capital. But there are only very few funds that outsource signal generation. [When regulators tried to create a transparent market for research (speak: signals) with MIFID II, they unexpectedly killed many firms that were producing research before](https://www.ft.com/content/42d13ff8-f489-11e8-ae55-df4bf40f9d0d). This text argues that **1. markets for signals suffer from a contracting problem, and 2. the best way to solve that problem is to only sell information of which not all buyers can make sense.**

## The contracting problem
As we have seen, the value of a signal strongly depends on how many other traders have access to it. Trading signals are a lot like positional goods, but with two twists A) the marginal cost of the signal is zero, once it is generated it can be copied for free and B) it is not possible to check if others have the signal because it is private information why others make a certain trade. Therefore the buyer and the seller have a contracting problem. The buyer can never be sure that the seller is not selling the signal to others. Unlike in traditional positional goods, other buyers can not be priced out because the marginal cost is zero, so the seller can secretly give away the signal to everyone who can not afford a high fee. This contracting problem might explain why the vast majority of funds creates their signals in house. Since you can only hope to achieve superior returns if you make them in house, there is no market for alpha signals. There may however be a market for data from which signals can be extracted and about which buyers think they are better at signal extraction than others, we will get to that.

There seem to be three ways out of this problem 
1. Performance dependent pay, in which the buyer incentivizes the seller buy paying a share of the profits. WorldQuant and Quantopian follow that model. But this requires that the funds commit to allocate a certain amount of capital to a strategy and encourages data mining which is probably why it has not been picked up more. 
2. Encrypting the data and putting the copying in a public ledger: There are quite a few startups operating marketplaces in which blockchain is supposed to enable restrictions on data distribution. However, they are all still very small, and it is not clear how they would prevent a seller from copying data outside of the system.
3. Selling data that requires a competitive advantage to turn into an alpha signal. That is, vendors sell only "raw data" that still requires the fund to extract the actual signal. The data must be of such quality, that not all funds have the capability of extracting the signal. **This is the kind of data we see on data marketplaces such as Quandl**. Selling only raw inputs while keeping the competitive advantage of the signal within the fund seems to be the most common workaround to the contracting problem found in the industry.

## Sell-side research and the contracting problem
The fact that you can only sell data or information of which not everyone can make sense has wide reaching implications. For a long time, sell side firms have given away research (read: signals) away for free, bundled with other services. This makes perfect sense if you consider that every investor should be able to make sense of good sell side research and you can therefore not sell the research. Once MIFID II forced sell side firms to sell their research separately [sell side research coverage decreased, a price war for sell side research ensued while buy-side research increased](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3422155). Even the regulators themselves were surprised by [the low rates sell side research fetched on this new market](https://www.ft.com/content/9a037d90-3908-11e9-b72b-2c7f526ca5d0), but once you consider the contracting problem it makes perfect sense: Because they can not contract for exclusivity, buyers of sell side research have to assume that all other investors have the information too. There is still value in buying the information, but this value is very low. Even if other investors did not buy the sell-side research, buyers would never be able to verify this and may this not be willing to pay more.

## Signals of which not everyone can make sense
This text argues that the best solution to the contracting problem is to sell data of which not every buyer can make use. That is, not every buyer can extract the signal predicting security payoffs from the data. This might be because they lack the sophistication to e.g. perform complex analytics or are not able to contextualize it. Highly sophisticated hedge funds might be able to make better use of signals than retail investors. Because there are only a few investors that can make use of a signal, buyers are not as worried about the contracting problem, because there is a limit to how many investors the seller can sell the signal. There are many examples of such signals in the alternative data space: Not every investor can make use of real time information of executive private jet flight paths, but some can and **are willing to pay for that information _because_ they are the only ones that can use it**. Consequently, data which requires a higher degree of sophistication to use fetches higher prices.

## Comparison to conventional Grossman-Stiglitz
There is a large literature providing ample of models of the value of information to the buyer. Without going into the math, there usually is a set of informed traders, a set of uninformed (or noise) traders and a zero-profit market maker. The market maker sets prices after performing a bayesian belief update about the security's payoffs after observing order flow, keeping in mind how many of these orders came from informed and uninformed traders. The market maker does not know who the informed traders are, just how many of them there are around. Therefore, all gains to the informed traders are losses for the uninformed traders, and if the cost of information is smaller than the gain from becoming informed, traders will buy the information. Our model can extend the classical model very easily: Instead of keeping the cost of information constant, we assign a different cost of information to each trader: The cost of extracting signal from the data. The distribution of information cost will then influence the proportion of investors buying information and the maximum price they would be willing to pay for it.
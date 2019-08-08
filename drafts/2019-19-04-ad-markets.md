# What finance can learn from marketing
## Hint: There are other people better at designing markets

When you visit pretty much any website, your attention is sold at an auction. Most people know that websites such as Facebook or The New York Times are in large parts funded through ads. Most people do not know, who or what decides what ads appear on their screen. And even fewer people, especially not in the financial industry, understand that the blueprint for the future of finance is in ads.

## The algorithms that decide which ads you see 
At the core of advertising lies an auction, in which inventory (speak ad spaces) is sold to advertisers. This is not new. If you wanted to run a front page ad in your local newspaper back in the day, you would call them and tell them how much you would be willing to pay. If you were the highest bidder, your ad was printed. In the internet age, something changed: Ads are now sold on an impression basis and the same website can serve different ads to different users at different times. Every website visit is unique and has different values to different advertisers. The value of displaying an ad to the advertiser is driven by the probability that the user will end up buying something because of it and the value of the purchase. The probability that a 40 year old father of two will buy a family vacation is much higher than that a 20 year old college student will. Thus, while both might visit the same website, they should not be shown the same ad, because that would not take advantage of their different values to different advertisers. Advertisement slots are unique goods, not commodities. A complex ecosystem has developed to auction millions of these unique goods every second. Fully automated, data driven and extremely profitable. 

<p><a href="https://commons.wikimedia.org/wiki/File:Adservingfull.svg#/media/File:Adservingfull.svg"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Adservingfull.svg/1200px-Adservingfull.svg.png" alt="Adservingfull.svg"></a><br>By <a href="//commons.wikimedia.org/wiki/User:Nagle" title="User:Nagle">Nagle</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/4.0" title="Creative Commons Attribution-Share Alike 4.0">CC BY-SA 4.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=44514492">Link</a></p>

## The journey of an ad
Imagine you run a website about cats: cats-and-ads.com, and I visit it. This is what happens:

- My browser sends a http request to your website. 
- Your website gathers some information such as my IP address, browser language (e.g. English) and stored cookies that might identify me and sends it to the **supply side platform** (SSP) that you are working with.
- The job of the supply side platform is to make your life easier and make sure there are ads on your website. It adds some extra information to your request (e.g. what type of ads are not allowed on your site) and then sends a request to an **ad exchange**
- The ad exchange has a list of **demand side platforms** (DSP) and sends them an invitation to bid on the ad slot, together with the data that you and the supply side platform provided.
- The demand side platform might then merge your data with even more data that they have on me and use different predictive models to come up with a value they are willing to pay to display a certain ad. They send the valuation and the ad back to the ad exchange.
- The ad exchange then runs an auction. The ad with the highest bid is sent back to your supply side platform.
- The supply side platform forwards the ad to your website.
- Your website responds to my http request and is displayed (together with the ad) in my browser.

This entire process usually takes less than 100 milliseconds. SSPs, DSPs and ad exchanges might potentially buy additional data from **data vendors** to improve outcomes. Advertisers might engage **agencies** to design campaigns, which then again hire **trading desks** to make sure ads are well placed. The ad might go through several **creative optimization** and **retargeting** steps to fit well into the space of the ad slot and be maximally applicable to me. This system can customize or even create and then sell millions of unique items to millions of unique users every second. And this, as we will soon see, is very useful for the financial industry.

## What Wall Street can not sell 
The financial industry prides itself on its markets. Some even say they are "efficient" which basically means they can not be improved. The bull statue on Wall Street is perhaps _the_ symbol of capitalism. But it is worth remembering that there are not that many things traded on financial exchanges. The U.S. stock market (by far the biggest in the world) is home to less than [4,000](https://www.bloomberg.com/opinion/articles/2018-04-09/where-have-all-the-u-s-public-companies-gone) listed firms. Most other things are traded by people, in a slow and expensive process. Let's walk through the steps of an entrepreneur selling her company:

- The entrepreneur contacts a **sell side** firm (usually an investment bank) and tells them she would like to sell and under which conditions.
- The sell side firm gathers some additional data on the firm and the industry and creates a prospectus which is then sent to **buy side firms**, usually private equity firms. There is no exchange.
- The buy side firms gather even more information on the firm, its competitors, the industry and so on and come up with a valuation. Using this valuation they then submit a bid. The money to buy the firm comes from **limited partners** who engage the buy side firm to manage their money. 
- Once all bids are in, the highest bidder wins. The limited partners transfer money to the buy side firm, the buy side to the sell side, and the sell side to the entrepreneur. Everyone takes a cut in the process. 

As you can see, this process is relatively similar to the ad auction. It is just much slower and much more expensive, costing usually around 10% of the sold firm's value. Because of its cost, only firms with a value of $100 million and more can be sold that way (there are exceptions but they are few). This means many things are _not_ traded on financial markets: Small businesses, single home real estate, individual insurance contracts, etc. Sometimes, a large number of assets that are too small to be traded individually is bundled into e.g. a mortgage backed security, but valuing those bundles without really understanding what is in them can be tricky and has led to high profile disasters. And if Wall Street does trade smaller firms like small public companies, it often is not very good at it. Investors often find that small firms have little analyst coverage and poor liquidity, meaning it can take a long time to sell shares of they have to be deeply discounted. 

## Systematic investing for everything

Lets see how the ad sales model would apply to the entrepreneur selling a business: 

- The entrepreneur contacts a sell side platform. The SSP requirers a lot of data to go with the request, such as the location of stores, the typical customer target group and so on.
- The SSP then posts the information of the company available for sale on an exchange. The exchange contacts relevant buy side platforms, to let them know that a new relevant listing is available.
- The BSPs then add even more information to the listing and programmatically come up with a valuation. 




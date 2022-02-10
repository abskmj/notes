---
title: "TradingView Charts for PancakeSwap Tokens"
date: 2021-06-08T17:30:00+05:30
tags: ["TradingView", "Charts", "PancakeSwap"]
summary: " "
---

# Update - Live Preview
I have added a live preview of the charts using the Technical charts from TradingView. [Source code]({{< ref "bmc-extra-pancake/index.md" >}}) of these charts is available.

{{< iframe 
    src="//tradingviewcharts.gitlab.io/pancakeswap-bitquery/"
    desc="Live Preview - Chart for PancakeSwap Token (CAKE)"
>}}


>  [**PancakeSwap**](https://pancakeswap.finance/) Cheaper and faster than Uniswap? Discover PancakeSwap, the leading DEX on Binance Smart Chain (BSC) with the best farms in Defi and a lottery for CAKE.

This showcases a couple of OHLC Charts for Pancakeswap Tokens implemented using the [TradingView Lightweight Charts](https://www.tradingview.com/lightweight-charts/) and [Bitquery.io](https://bitquery.io/) APIs.

[TradingView Techincal Analysis Charts](https://in.tradingview.com/HTML5-stock-forex-bitcoin-charting-library/?feature=technical-analysis-charts) can replace the Lightweight Charts. You would need to request access to the technical charts on their website to use them.

I run a gig on [Fiverr.com](https://www.fiverr.com/share/Gd8pwL) to help with such integrations and customizations. You can also connect with me on [Discord](https://discordapp.com/users/220585271983472650).

> If you are new to Fiverr, you can use [my referral link](http://www.fiverr.com/s2/730602a4fa) to signup and get 20% off on your first order. 


# OHLC Chart with Bitquery GraphQL API
- Uses TradingView Lightweight Charts library
- Integrates with [Bitquery.io GraphQL API](https://graphql.bitquery.io/ide)
- Shows prices (WBNB) for Pancakeswap tokens
- Plots both candlestick and bar charts

{{< iframe 
    src="//tradingviewcharts.gitlab.io/lightweight-bitquery-parcel/"
    desc="CAKE/WBNB - A sample integration of TradingView Lightweight Chart library with Bitquery GraphQL API to showcase candlestick chart for PancakeSwap Tokens. Uses Parcel as the bundler."
>}}

# Chart for another Token
By default, plots a chart for PancakeSwap (CAKE) token. Setting `?token=<token_address>` URL parameter plots for another by its address. Below is a sample for UniSwap (UNI) token.

{{< iframe 
    src="//tradingviewcharts.gitlab.io/lightweight-bitquery-parcel/?token=0xbf5140a22578168fd562dccf235e5d43a02ce9b1"
    desc="UNI/WBNB - A sample integration of TradingView Lightweight Chart library with Bitquery GraphQL API to showcase candlestick chart for PancakeSwap Tokens. Uses Parcel as the bundler."
>}}

# Looking for a Developer?
Connect with me on [Fiverr.com](https://www.fiverr.com/share/Gd8pwL) or [Discord](https://discordapp.com/users/220585271983472650)
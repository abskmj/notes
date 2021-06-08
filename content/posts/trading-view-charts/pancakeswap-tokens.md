---
title: "TradingView Charts for PancakeSwap Tokens"
date: 2021-06-08T17:30:00+05:30
tags: ["TradingView", "Charts", "PancakeSwap"]
summary: " "
---

>  [**PancakeSwap**](https://pancakeswap.finance/) Cheaper and faster than Uniswap? Discover PancakeSwap, the leading DEX on Binance Smart Chain (BSC) with the best farms in DeFi and a lottery for CAKE.


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
By default, plots a chart for PancakeSwap (CAKE) token. Setting `?token=<token_address>` URL parameter plots for another token by its address. Below is a sample for UniSwap (UNI) token.

{{< iframe 
    src="//tradingviewcharts.gitlab.io/lightweight-bitquery-parcel/?token=0xbf5140a22578168fd562dccf235e5d43a02ce9b1"
    desc="UNI/WBNB - A sample integration of TradingView Lightweight Chart library with Bitquery GraphQL API to showcase candlestick chart for PancakeSwap Tokens. Uses Parcel as the bundler."
>}}

# Looking for a Developer?
Connect with me on [Fiverr.com](https://www.fiverr.com/share/Gd8pwL)
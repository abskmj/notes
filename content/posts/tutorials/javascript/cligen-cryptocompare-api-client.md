---
title: "Implement a Javascript Client for Crypto Compare API "
date: 2018-12-16T07:30:14Z
tags: ["Tutorial","Cligen","NPM","API","Client","JavaScript","Browser"]
---
# Crypto Compare
[Crypto Compare](https://www.cryptocompare.com/) is a website and API provider which brings you all the latest streaming pricing data in the world of cryptocurrencies. Their API documentation is available [here](https://min-api.cryptocompare.com/documentation).

# Javascript Client
I'm writing a javascript based client for few commonly used crypto compare APIs which can be used on both nodejs and browser. I'm using an NPM module called [Cligen](https://github.com/abskmj/cligen) to generate the client. The module only needs a corresponding JSON specification of the API endpoints to generate the client.

# Cligen Specification
I'm writing the specification for 2 of the commonly used endpoints. You can follow a similar way for other endpoints as well.

- Single Symbol Price
- Historical Minute OHLCV

## spec.json
```json
{
    "baseUrl": "https://min-api.cryptocompare.com/data",
    "operations": {
        "price": {
            "uri": "/price",
            "data": {
                "query": {
                    "parameters": [
                        { "name": "tryConversion" },
                        {
                            "name": "fsym",
                            "required": true
                        },
                        {
                            "name": "tsyms",
                            "required": true
                        },
                        { "name": "e" },
                        { "name": "extraParams" },
                        { "name": "sign" }
                    ]
                }
            }
        },
        "histominute": {
            "uri": "/histominute",
            "data": {
                "query": {
                    "parameters": [
                        { "name": "tryConversion" },
                        {
                            "name": "fsym",
                            "required": true
                        },
                        {
                            "name": "tsym",
                            "required": true
                        },
                        { "name": "e" },
                        { "name": "aggregate" },
                        { "name": "aggregatePredictableTimePeriods" },
                        { "name": "limit" },
                        { "name": "toTs" },
                        { "name": "extraParams" },
                        { "name": "sign" }
                    ]
                }
            }
        }

    }
}
```

# NodeJS

## Installing Cligen Module

```bash
npm install -save github:@abskmj/cligen
```

## Generating and Using the client

```jvascript
const cligen = require('@abskmj/cligen');

const spec = require('./spec.json');

const client = cligen.getClient(spec);


// supports callback
client.price({ fsym: 'BTC', tsyms: 'USDT' }, (error, response) => {
    if (error) {
        console.log(error);
    }
    else {
        console.log(response);
        
        /*
            { headers: 
               { server: 'nginx/1.10.3',
                 date: 'Sun, 16 Dec 2018 08:09:00 GMT',
                 'content-type': 'application/json; charset=UTF-8',
                 'transfer-encoding': 'chunked',
                 connection: 'close',
                 vary: 'Accept-Encoding',
                 'access-control-allow-origin': '*',
                 'access-control-allow-methods': 'GET, POST, OPTIONS',
                 'access-control-allow-headers': 'Content-Type, Cookie, Set-Cookie',
                 'access-control-allow-credentials': 'true',
                 'cache-control': 'public, max-age=10',
                 'cryptocompare-cache-hit': 'false' },
              data: { USDT: 3261.81 },
              status: 200,
              request: 
               { url: 'https://min-api.cryptocompare.com/data/price?fsym=BTC&tsyms=USDT',
                 method: 'GET',
                 headers: {},
                 body: undefined } }
        
        */
    }
});

// supports promise
client.histominute({ fsym: 'BTC', tsym: 'USDT' })
.then((response) => {
    console.log(response);
    
    /*
        { headers: 
           { server: 'nginx/1.4.6 (Ubuntu)',
             date: 'Sun, 16 Dec 2018 08:41:46 GMT',
             'content-type': 'application/json; charset=UTF-8',
             'transfer-encoding': 'chunked',
             connection: 'close',
             vary: 'Accept-Encoding',
             'access-control-allow-origin': '*',
             'access-control-allow-methods': 'GET, POST, OPTIONS',
             'access-control-allow-headers': 'Content-Type, Cookie, Set-Cookie',
             'access-control-allow-credentials': 'true',
             'cache-control': 'public, max-age=10',
             'cryptocompare-cache-hit': 'false' },
          data: { USDT: 3263.88 },
          status: 200,
          request: 
           { url: 'https://min-api.cryptocompare.com/data/price?fsym=BTC&tsyms=USDT',
             method: 'GET',
             headers: {},
             body: undefined } }
        { headers: 
           { server: 'nginx/1.4.6 (Ubuntu)',
             date: 'Sun, 16 Dec 2018 08:41:46 GMT',
             'content-type': 'application/json; charset=UTF-8',
             'transfer-encoding': 'chunked',
             connection: 'close',
             vary: 'Accept-Encoding',
             'access-control-allow-origin': '*',
             'access-control-allow-methods': 'GET, POST, OPTIONS',
             'access-control-allow-headers': 'Content-Type, Cookie, Set-Cookie',
             'access-control-allow-credentials': 'true',
             'cache-control': 'public, max-age=40',
             'cryptocompare-cache-hit': 'true' },
          data: 
           { Response: 'Success',
             Type: 100,
             Aggregated: false,
             Data: 
              [ ... ],
             TimeTo: 1544949660,
             TimeFrom: 1544863260,
             FirstValueInArray: true,
             ConversionType: { type: 'direct', conversionSymbol: '' },
             RateLimit: {},
             HasWarning: false },
          status: 200,
          request: 
           { url: 'https://min-api.cryptocompare.com/data/histominute?fsym=BTC&tsym=USDT',
             method: 'GET',
             headers: {},
             body: undefined } }
    */
}). catch((error) => {
    console.log(error);
})

```
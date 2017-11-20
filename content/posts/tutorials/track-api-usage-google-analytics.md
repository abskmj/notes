---
title: "Track API usage with Google Analytics"
date: 2017-11-15T18:02:07+05:30
tags: ["Google Analytics", "Node.js", "NPM" , "Tutorial"]
---

Google analytics is a popular tool to track your website usage. Usage of server APIs can also be tracked with this tool. Measurement Protocol APIs can be used to post the usage data to Google Analytics.

> [Measurement Protocol](https://developers.google.com/analytics/devguides/collection/protocol/) can be used to track user interactions in any environment of internet connected devices. It allows developers to collect user-interaction in form of event or hit.

# API Hit
Each invocation of an API can be tracked as a unique event. Optionally, the response time in millisecond can be included as well.

```
&t=event            // Event hit type
&ec=api             // Event category: api
&ea=invoke          // Event action: invoke
&el=registration    // Event label: name of the API
&ev=300             // Event value: (optional) response time in milliseconds
```

## User Session
Multiple APIs can be invoked by multiple users over multiple sessions. Multiple sessions is automatically handled by Google Analytics. Multiple users can be handled by setting `cid` field appropriately. Each unique value set will correspond to a new user.

```
&cid=555    // Anonymous Client ID.
```

User's IP can be used to set this field uniquely.

```javascript
var cid = hash(request.headers['x-forwarded-for'] || request.connection.remoteAddress);
```

- [`x-forwarded-for`](https://en.wikipedia.org/wiki/X-Forwarded-For) header is generally used by proxies to pass originating client's IP.
- IP value should be hashed to avoid collecting sensitive user or client information.

## User Analytics
Most of this data is captured by processing user's IP address and browser's [user agent](https://en.wikipedia.org/wiki/User_agent). In this case, user's IP and UA is not passed to Google Analytics rather the server's IP is passed. All the analytics will have details of the servers only.

To fix this, `uip` & `ua` fields can be used to set user information.

```
&uip=1.2.3.4     // IP address override.
&ua=Opera/9.80   // User agent override.
```

> I have published a npm module which allows such overrides [@abskmj/google-analytics-tracker](https://www.npmjs.com/package/@abskmj/google-analytics-tracker).

## Sample Request

```javascript
// nodejs
var request = require('request');

request({
    baseUrl: 'https://www.google-analytics.com',
    uri: '/collect',
    body: 'v=1&tid=UA-XXXXXXXX-X&cid=XXXXXXX&t=event&ec=api&ea=invoke&el=registration&ev=300&uip=1.2.3.4&ua=Opera/9.80',
    method: 'POST'
}, function (error, response, body) {
    if(error){
        console.error(error);
    }
    else{
        console.log(body)
    }
});
```
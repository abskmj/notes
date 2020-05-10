---
title: "Express middleware to log request / response headers"
date: 2020-05-10T13:03:19+05:30
tags: ["Express", "Headers", "Middleware", "Request", "Response"]
---

# Express Middleware
Logging request and response headers for tracing purpose

```javascript
app.use((req, res, nxt) => {
  const requestHeaders = req.headers

  console.log('Request Headers:', requestHeaders)

  // Request Headers: {
  //     'user-agent': 'PostmanRuntime/7.24.1',
  //     accept: '*/*',
  //     'cache-control': 'no-cache',
  //     'postman-token': '74416f71-0d09-453f-b714-3737dfd9f6b4',
  //     host: 'localhost:3000',
  //     'accept-encoding': 'gzip, deflate, br',
  //     connection: 'keep-alive'
  //   }

  res.on('finish', () => {
    const responseHeaders = res.getHeaders()

    console.log('Response Headers:', responseHeaders)

    // Response Headers: [Object: null prototype] {
    //     'x-powered-by': 'Express',
    //     'content-type': 'text/html; charset=utf-8',
    //     'content-length': '12',
    //     etag: 'W/"c-Lve95gjOVATpfV8EL5X4nxwjKHE"'
    //   }
  })

  nxt()
})

```

> More details on response `finish` event and others at [nodejs.org](https://nodejs.org/api/http.html#http_event_finish)

> There is a codebase for reference at [gist.github.com](https://gist.github.com/abskmj/cef6d790d1b8778ce37eafc178b550ce)
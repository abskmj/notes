---
title: "Setup DNS over HTTPS (DOH) on Firefox Android"
date: 2023-07-15T00:00:00+05:30
tags: ["Android", "Firefox", "Privacy", "DOH"]
---

Setup DNS over HTTPS (DOH) in a Firefox browser, on an Android device for privacy and security.

# Configuration Editor on Firefox
Firefox on an Android device currently does not support setting up [DNS over HTTPS (DOH)](https://en.wikipedia.org/wiki/DNS_over_HTTPS) under the settings menu. However, as a workaround, it can be configured through [Configuration Editor for Firefox](https://support.mozilla.org/en-US/kb/about-config-editor-firefox).

Access it using the `about:config` keywords in the address bar of the browser. It is available only in beta and nightly versions of Firefox.

This setup also works on other variants of Firefox, for example,  Focus and Mull.

Update the configuration related to [Trusted Recursive Resolver(TRR)](https://wiki.mozilla.org/Trusted_Recursive_Resolver).

- network.trr.mode = 3

I set it to `3` instead of `2` as there is no way to know when the connection falls back when in mode `2`.

- network.trr.uri = https://dns.adguard-dns.com/dns-query

If this is not set, Firefox uses Cloudflare DNS as the default provider. I set it to [AdGuard DNS](https://adguard-dns.io/en/welcome.html) mainly to block ads and trackers. AdGuard has a [test page](https://adguard.com/en/test.html) to check if their DNS is configured correctly and working. 
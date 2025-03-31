---
title: "Endpoint Base URLs"
slug: "endpoint-base-urls"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Sep 10 2018 02:06:55 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 15 2020 05:48:09 GMT+0000 (Coordinated Universal Time)"
---
There are two base URLs for interacting with the Gateway, depending on the environment required:

| Environment       | URL                                 |
| :---------------- | :---------------------------------- |
| Sandbox (Test)    | <https://gateway.pmnts-sandbox.io/> |
| Production (Live) | <https://gateway.pmnts.io/>         |

Where merchants require statically addressed endpoints (such as for IP Whitelisting of outbound network traffic to the internet) the following endpoints can be used, however merchants must understand that due to the nature of these endpoint configurations **_there may be a longer delay during a network failover in the event of a technical fault, compared to the above endpoints._**  This is usually around 60 seconds as opposed to 10-30 seconds normally. If this is of concern to you please contact our Support team to discuss further.

[block:parameters]
{
  "data": {
    "h-0": "Environment",
    "h-1": "URL",
    "h-2": "IP addresses",
    "0-0": "Sandbox (Test)",
    "0-1": "<https://gateway-static.pmnts-sandbox.io>",
    "0-2": "75.2.69.3  \n99.83.178.72",
    "1-0": "Production (Live)",
    "1-1": "<https://gateway-static.pmnts.io>",
    "1-2": "75.2.13.242  \n99.83.244.137"
  },
  "cols": 3,
  "rows": 2,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


For the Hosted Payment Page the following URLs apply:

| Environment       | URL                                |
| :---------------- | :--------------------------------- |
| Sandbox (Test)    | <https://paynow.pmnts-sandbox.io/> |
| Production (Live) | <https://paynow.pmnts.io/>         |

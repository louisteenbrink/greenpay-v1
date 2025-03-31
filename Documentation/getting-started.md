---
title: "Getting Started"
slug: "getting-started"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Oct 13 2017 01:46:43 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 19:35:30 GMT+0000 (Coordinated Universal Time)"
---
Fat Zebra provides a simple to use REST API. It is designed to be simple, have predictable URLs and uses HTTP response codes to indicate errors. In addition to this, it uses HTTP features such as Basic Authentication and HTTP verbs (GET, PUT, POST etc). This means that it is highly compatible with most HTTP clients including `Net::HTTP`, `cURL` and `System.Net.WebClient` and `httplib`.

The API expects to receive and will respond with JSON payloads. It is recommended if you are having problems to test the formatting of your data against a lint tool, such as JSONLint (<https://jsonlint.com/>).

> 🚧 Note:
> 
> It is important that you ensure no sensitive data is included in the data you are validating - this includes card numbers and CVV/CVC numbers. We also recommend that you replace card holder names with example data, however names with diacritics, umlauts or accents may cause validation issues, so remember this while you are testing.

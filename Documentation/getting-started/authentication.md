---
title: "Authentication"
slug: "authentication"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Jul 17 2018 07:36:49 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 19:35:46 GMT+0000 (Coordinated Universal Time)"
---
Authentication with the Fat Zebra API is via HTTP Basic Authentication. When your account is setup you are provided with two sets of credentials - one for the test environment (also known as the Sandbox), and one for the live system. Your test username will always be prefixed with `TEST`.

API requests must be made over HTTPS - any requests over HTTP will fail. All requests require authentication.

> 🚧 Note:
> 
> It is important to note that your username is not case sensitive however your API token (password) is.

```curl
$ curl https://gateway.pmnts-sandbox.io/v1.0/purchases -u TEST:TEST
```

---
title: "Get Apple Pay Session"
slug: "get-apple-pay-session"
excerpt: "Get an opaque Apple Pay session object that can be used to call the Apple Pay Javascript SDK's completeMerchantValidation method"
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Aug 10 2020 06:47:59 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Nov 10 2022 02:22:01 GMT+0000 (Coordinated Universal Time)"
---
In order to display the Apple Pay payment sheet when integrating Apple Pay on the Web, you will need to retrieve an opaque Apple Pay session object. The following Fat Zebra API endpoint can be used to retrieve the opaque Apple Pay session object.

## Request Details

[block:parameters]
{
  "data": {
    "h-0": "Property",
    "h-1": "Description",
    "0-0": "**Method** ",
    "0-1": "`GET`",
    "1-0": "**URL** ",
    "1-1": "**Sandbox:** <https://paynow.pmnts-sandbox.io/v2/apple_pay/payment_session>  \n  \n**Production:** <https://paynow.pmnts.io/v2/apple_pay/payment_session>",
    "2-0": "**Authentication** ",
    "2-1": "Refer to [Authentication](doc:authentication)"
  },
  "cols": 2,
  "rows": 3,
  "align": [
    "left",
    "left"
  ]
}
[/block]


## Request Parameters

[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`url`",
    "0-1": "String",
    "0-2": "The Validation URL provided by the Apple Pay JS SDK's [**onvalidatemerchant**](https://developer.apple.com/documentation/apple_pay_on_the_web/apple_pay_js_api/providing_merchant_validation) event handler  \n  \nThe Validation URL provided must come from one of the [whitelist Apple Pay domains](https://developer.apple.com/documentation/apple_pay_on_the_web/setting_up_your_server) or a `400 Bad Request` response will be returned",
    "1-0": "`domain_name`",
    "1-1": "String",
    "1-2": "The fully qualified domain name of your website that initiated the Apple Pay payment sheet via an Apple Pay button",
    "2-0": "`display_name`",
    "2-1": "String, maximum 64 UTF-8 characters",
    "2-2": "The display name for the merchant in the Apple Pay Session. This will be displayed in the Touch Bar, and in the Payment Sheet when displayed to the customer"
  },
  "cols": 3,
  "rows": 3,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


## Example Request

```curl Get Payment Session Request
curl https://paynow.pmnts-sandbox.io/v2/apple_pay/payment_session\?url\=https://apple-pay-gateway-cert.apple.com/paymentservices/startSession\&domain_name\=fatzebra.com -u TEST:TEST
```

## Example Response

```json Opaque Apple Pay Session response
{
  "epochTimestamp": 1597042910373,
  "expiresAt": 1597046510373,
  "merchantSessionIdentifier": "<identifier>",
  "nonce": "<nonce>",
  "merchantIdentifier": "<merchant-identifier>",
  "domainName": "fatzebra.com",
  "displayName": "Fat Zebra",
  "signature": "<signature>"
}
```

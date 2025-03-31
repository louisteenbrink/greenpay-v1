---
title: "ApplePaySetupParams"
slug: "applepaysetupparams"
excerpt: ""
hidden: true
createdAt: "Mon Aug 12 2024 02:39:09 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Aug 22 2024 00:46:41 GMT+0000 (Coordinated Universal Time)"
---
The **ApplePaySetupParams** object defines how the Apple Pay Button should be instantiated via fatzebra.js, as well as setting the [PaymentIntent](doc:paymentintent).

`ApplePaySetupParams` is used in the following methods:

- [renderApplePayButton](doc:renderApplePayButton) 

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Required/Optional",
    "h-4": "Default",
    "0-0": "`containerId`",
    "0-1": "string",
    "0-2": "The `id` of the HTML div element where the Hosted Payment Page iframe will be rendered",
    "0-3": "required",
    "0-4": "",
    "1-0": "`environment`",
    "1-1": "string",
    "1-2": "Production or sandbox environment can be set",
    "1-3": "required",
    "1-4": "",
    "2-0": "`paymentIntent`",
    "2-1": "[PaymentIntent](doc:paymentintent)",
    "2-2": "See [PaymentIntent](doc:paymentintent)",
    "2-3": "required",
    "2-4": "",
    "3-0": "`options.allowed_card_networks`",
    "3-1": "string",
    "3-2": "Specifies a whitelist of accepted cards.  \n  \nPossible values are:  \n  \n`amex`, `chinaUnionPay`, `discover`, `jcb`, `maestro`, `masterCard`, `visa`",
    "3-3": "optional",
    "3-4": "`visa` and `masterCard`",
    "4-0": "`options.allowed_card_types`",
    "4-1": "string, comma separated",
    "4-2": "Specifies a whitelist of accepted card.  \n  \nPossible values are:  \n  \n`supportsCredit`, `supportsDebit`, `supportsEMV`                    ",
    "4-3": "optional",
    "4-4": "`supportsCredit`,  \n`supportsDebit`, `suporrts3DS`",
    "5-0": "`options.domain_name`",
    "5-1": "string",
    "5-2": "Specifies the domain linked to the apple pay web certification. It also needs to match the origin of the request",
    "5-3": "optional",
    "5-4": "window.location.hostname is used to get origin url"
  },
  "cols": 5,
  "rows": 6,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]

---
title: "PayPalConfig"
slug: "paypal-config"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Aug 27 2020 07:21:03 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Nov 15 2023 00:24:41 GMT+0000 (Coordinated Universal Time)"
---
**PayPalConfig** is the input to the [setupPayPal](doc:setup-paypal) method for rendering the PayPal Button.

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Required/Optional",
    "0-0": "currency",
    "0-1": "String",
    "0-2": "AUD, USD, …",
    "0-3": "required",
    "1-0": "payment",
    "1-1": "[PayPalPaymentObject](doc:paypal-payment-object)",
    "1-2": "Required object for creating a PayPal Order (**authorize** or **capture**) or a PayPal Billing Agreement (subscription for recurring payments)  \n  \n{  \n   paymentIntent: {...}    // (optional),  \n    paymentMethod: {...} // (required)  \n}",
    "1-3": "required",
    "2-0": "containerId",
    "2-1": "String",
    "2-2": "The ID of the HTML tag which loads the PayPal Button",
    "2-3": "required",
    "3-0": "style",
    "3-1": "",
    "3-2": "Determines the layout/style of the PayPal Button  \n  \nRefer to [PayPal Button Style](https://developer.paypal.com/docs/archive/checkout/how-to/customize-button/#button-styles)",
    "3-3": ""
  },
  "cols": 4,
  "rows": 4,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


```javascript
var fz = new FatZebra({
  username: MERCHANT_USERNAME,
})

const paymentObject = {
  paymentIntent: {...},
  paymentMethod: {...}
}

fz.setupPayPal({
  currency: "AUD",
  payment: paymentObject,
  containerId: "paypal-button-container",
  style: {
    layout: "vertical",
    color: "blue",
    shape: "rect",
    label: "paypal"
  }
})
```

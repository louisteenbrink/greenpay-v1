---
title: "setupPayPal"
slug: "setup-paypal"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Aug 27 2020 06:49:58 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Nov 15 2023 00:26:06 GMT+0000 (Coordinated Universal Time)"
---
# setupPayPal ([PayPalConfig](doc:paypal-config))

This method renders the PayPal Button in the specified HTML DOM element. This method can be used for 2 flows:

1. Create a PayPal Order (**capture** or **authorization**). Refer to [PayPalPaymentObject](doc:paypal-payment-object).
2. Create a PayPal Billing Agreement (subscription). Refer to [PayPalPaymentObject](doc:paypal-payment-object).

```javascript
var fz = new FatZebra({
  username: MERCHANT_USERNAME,
})

fz.on("fz.paypal.success", function(event) {
  console.log(event.detail.data)
})

fz.on("fz.paypal.error", function(event) {
  console.log(event.detail.errors)
})

const paymentObject = {
  paymentIntent: {...},
  paymentMethod: {...}
}

// This method should be called after setting event listeners above!
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

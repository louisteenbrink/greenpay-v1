---
title: "PayPal"
slug: "paypal-events"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Aug 27 2020 07:56:52 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Nov 15 2023 00:28:40 GMT+0000 (Coordinated Universal Time)"
---
With the PayPal integration, merchants can subscribe to the following events to get response or error objects from our Gateway.

[block:parameters]
{
  "data": {
    "h-0": "Event",
    "h-1": "Description",
    "0-0": "fz.paypal.error",
    "0-1": "Emitted when there is any PayPal errors including:  \n- Rendering the PayPal button  \n- Validation errors (e.g. invalid request payload)  \n- Any PayPal initiated errors",
    "1-0": "fz.paypal.processing",
    "1-1": "Emitted when Fatzebra is processing the payment. This can be used to inform users, e.g. with a processing message",
    "2-0": "fz.paypal.cancel",
    "2-1": "Emitted when user cancels a payment",
    "3-0": "fz.paypal.success",
    "3-1": "Emitted when user confirms the payment/billing agreement"
  },
  "cols": 2,
  "rows": 4,
  "align": [
    "left",
    "left"
  ]
}
[/block]


> 🚧 Note
> 
> Event listeners should be set up before calling `fz.setupPayPal()`.

# fz.paypal.error

```json
{
  data: null,
  errors: ['Invalid request payload']
}
```

# fz.paypal.processing

```json
{
  data: {},
  message: 'The request is being processed.' 
}
```

# fz.paypal.cancel

```json
{
  data: {
  	orderID: '335GS56ADSG5'
  },
  message: 'PayPal Checkout cancelled.'
}
```

# fz.paypal.success

This event is fired for a successful order or a billing agreement:

### 1. PayPal Order

```json
{
  message: 'PayPal order approved.'
  data: {
    id: "123-PPO-NJV6YOCZ60J8NISE",
    reference: "ref_12345_281973",
    amount: 12000,
    decimalAmount: 120.0,
    successful: true,
    message: "Approved",
    currency: "AUD",
    transactionId: "123-PPO-NJV6YOCZ60J8NISE",
    transactionDate: "2020-08-27T15:14:22+10:00",
    intent: "Capture",
    paypalReference: "ref_12345_281973",
    invoiceId: "ref_12345_281973",
    billingAgreementId: null,
    status: "Completed",
    paymentSource: null,
    authorizedAmount: 0.0,
    capturedAmount: 120.0,
    refundedAmount: 0.0,
    authorizations: [],
    captures: [
      {
        id: "123-PPC-BHG8DOSWRCVLGZOK",
        status: "Completed",
        captured: true,
        amount: 12000,
        decimalAmount: 120.0,
        successful: true,
        currency: "AUD",
        transactionId: "123-PPC-BHG8DOSWRCVLGZOK",
        transactionDate: "2020-08-27T15:14:22+10:00",
        invoiceId: "ref_12345_281973",
        paypalFee: 318,
        sellerReceivableNetAmount: 11682,
        noteToPayer: "Sporting Goods",
        isFinalCapture: true
      }
    ],
    refunds: [],
    payer: {
      id: "29E2S1DN8P7FY",
      email: "test-buyer@example.com",
      address: { countryCode: "AU" }
    },
    payee: {
      id: "JEUIDZ5Q5JE0E",
      email: "test-seller@example.com"
    }
  }
}
```

### 2. PayPal Billing Agreement

```json
{
  message: 'PayPal Billing Agreement created.'
  data: {
    id: "123-PBA-OPFHG40FRT6AHDENC",
    name: "Sample Billing Agreement",
    description: "Stored PayPal account",
    state: "Active",
    payer: {
      payerInfo: {
        email: "test-buyer@example.com",
        firstName: "Test Buyer",
        lastName: "Buyer",
        payerId: "4NGF92BA8UA5S"
      }
    },
    shippingAddress: {
      firstName: "John",
      lastName: "Doe",
      address_1: "100 Kent Street",
      address_2: "Cafe Lane",
      city: "Sydney",
      state: "NSW",
      postcode: "2000",
      country: "AU"
    },
    merchantCustomData: "",
    createdAt: "2020-08-27T15:15:13+10:00"
  }
}
```

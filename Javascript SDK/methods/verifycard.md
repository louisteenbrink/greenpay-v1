---
title: "verifyCard"
slug: "verifycard"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jul 23 2020 06:12:53 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon May 10 2021 04:01:58 GMT+0000 (Coordinated Universal Time)"
---
# verifyCard(VerifyCardParams)

Starts the 3DS2/SCA process. This method is used for API and Direct Post integration modes only. If you are integrating 3DS2 using the [Hosted Payments Page](doc:using-hosted-payments-page) you do not need to call `verifyCard` as the Hosted Payments Page will handle this for you.

The `verifyCard` method can be called with a new card (using the raw card number) or with an existing card (using a Fat Zebra card token). If using an existing card (Fat Zebra card token), specify `card_on_file` as the `paymentMethod`. Refer to the [PaymentMethod](doc:paymentmethod) object for more details.

See [VerifyCardParams](doc:verifycardparams) for more details on the available parameters.

## Usage

```json
const fz = new FatZebra({
  username: "MerchantXYZ"
});

fz.verifyCard({
   customer: {
    firstName: 'Captain',
    lastName: 'America',
    email: 'hello.world@fatzebra.com.au',
    address: '123 Australia Blvd.',
    city: 'Sydney',
    postcode: '2000',
    state: 'NSW',
    country: 'AU'
  },
  paymentIntent: {
    payment: {
      amount: 1000,
      currency: "AUD",
      reference: "ref_123490",
    },
    verification: "ver_123480"
  },
  paymentMethod: {
    type: "card",
    data: {
      number: "4111111111111111",
      holder: "John Doe",
      expiryMonth: "01",
      expiryYear: "2022",
      cvv: "123"
    }
  }
});
```

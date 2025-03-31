---
title: "VerifyCardParams"
slug: "verifycardparams"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jul 29 2020 23:10:09 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon May 10 2021 04:00:14 GMT+0000 (Coordinated Universal Time)"
---
The **VerifyCardParams** object holds the values necessary to perform a 3DS2 check against a new or existing card.

| Attribute       | Type                               | Description                            | Required/Optional |
| :-------------- | :--------------------------------- | :------------------------------------- | :---------------- |
| `customer`      | [Customer](doc:customer)           | See [Customer](doc:customer)           | required          |
| `paymentIntent` | [PaymentIntent](doc:paymentintent) | See [PaymentIntent](doc:paymentintent) | required          |
| `paymentMethod` | [PaymentMethod](doc:paymentmethod) | See [PaymentMethod](doc:paymentmethod) | required          |

```javascript
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

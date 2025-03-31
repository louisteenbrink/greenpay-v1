---
title: "renderPaymentsPage"
slug: "renderpaymentspage"
excerpt: ""
hidden: false
createdAt: "Fri Jul 24 2020 05:03:51 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Nov 07 2024 00:21:14 GMT+0000 (Coordinated Universal Time)"
---
# renderPaymentsPage(HppSetupParams)

Renders the Fat Zebra Hosted Payments Page within the specified div element (see `containerId` in the example below).

The version field will control what version of the iframe will be displayed. The field is optional and will default to V2 if not included.

```javascript
const fz = new FatZebra({
  username: "MerchantXYZ"
});

fz.renderPaymentsPage({
  containerId: "fz-paynow",
  version: 3,
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
      amount: 500,
      currency: "AUD",
      reference: "ref_123490"
    },
    verification: 'ver_123480'
  },
  options: { // Hpp display options
    hideButton: false,
    hideLogos: true
  }
});
```

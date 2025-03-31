---
title: "Using Custom Payments Form"
slug: "using-custom-payments-form"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Aug 19 2020 00:52:00 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Apr 29 2021 01:15:33 GMT+0000 (Coordinated Universal Time)"
---
# Overview

If you collect card details using your own payments form, you can perform 3DS2 checks using fatzebra.js.

> 📘 Before completing the steps below, speak to the Fat Zebra support team to have 3DS2 enabled on your account

### Step 1 - Obtain an OAuth access token

Follow the steps in [Obtain an OAuth token](doc:obtain-oauth-token) to obtain an access token for your checkout session.

### Step 2  - Include fatzebra.js on your page

```html
<script type="text/javascript" src="https://cdn.pmnts-sandbox.io/sdk/v1/fatzebra.js"></script>
```

### Step 3 -  Initialise the FatZebra SDK

```javascript
// Initialize the FatZebra object in the footer of your page
<script>
const fz = new FatZebra({
  username: "<YOUR MERCHANT USERNAME>"
});

...
</script>
```

Note: your merchant username can be obtained from the Fat Zebra Merchant Dashboard.

### Step 4 - Subscribe to fatzebra.js events

fatzebra.js will emit various javascript events. Subscribe to the ones relevant to you.

Available events:

- [Tokenization](doc:tokenization) - for success or failure of the tokenization of the card data
- [SCA](doc:sca) - for success or failure of the 3DS2 checks

```javascript
// Handle validation related errors, e.g. client-side validation
fz.on('fz.validation.error', function(event) {
  // ...
});

// Receive the result of the 3DS2 check.
fz.on('fz.sca.success', function(event) {
  // Obtain 3DS2 results which will be used to make a purchase in the backend
})

// Handle errors related to SCA
fz.on('fz.sca.error', function(event) {
  // Show an error message to the customer
});
```

### Step 5 - Perform 3DS2 checks on the card

Call the fatzebra.js `verifyCard` method to perform 3DS2 on a card.

See [verifyCard](doc:verifycard) and [VerifyCardParams](doc:verifycardparams) for more details.

```javascript
// Call this function when the checkout button on your page is clicked
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
    verification: "ver_123480" // made up value
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

### Step 6 - Frictionless or challenge flow presented to customer

The fatzebra.js `verifyCard` will send the payment and customer details onto the issuing bank of the cardholder. The issuing bank will then determine if:

a) The customer should be presented with a 3DS2 challenge to prove they are the cardholder. This normally involves the customer receiving a one-time pin (OTP) on their phone and then be required to enter the OTP into a modal dialog on the payment page. The fatzebra.js `verifyCard` method will automatically display this modal dialog, no additional code is required on your end.

b) If the issuing bank determines that the customer is low risk they may allow the customer to go through a "frictionless" flow, whereby the customer does not need to complete any additional steps (such as an OTP).

### Step 7 - Obtain 3DS check result

After the customer has completed the frictionless or challenge flow, fatzebra.js will emit one of the following events:

a) `fz.sca.success`: when 3DS validation completes successfully  
b) `fz.sca.error`: when 3DS enrolment or validation failed

In the event of a successful 3DS check, the `fz.sca.success` event will contain 3DS result data (`cavv`, `sli`, etc.) that can be sent in your backend purchase or refund call. The presence of valid 3DS result data in your Purchase or Refund API will enable a liability shift to the issuer for fraudulent transactions.

> 🚧 A separate check with successful 3DS result data is required for each payment you wish to make. The same 3DS result data cannot be used in multiple purchases.

### Step 8 - Make a purchase using 3DS result data

Provide the 3DS result data from the `fz.sca.success` event in the request payload `extra` field when making a [Purchase](ref:purchases) or [Refund](doc:refunds-1) API call. Please note that these API calls require `snake_case` keys, i.e. `directory_server_txn_id`, not `directoryServerTxnId`

See [3DS extra payload](doc:3d-secure) for more information.

```json
{
    "amount": 10,
    "currency": "AUD",
    "card_token": "syupxv5b1tqv4bqdsazr",
    "reference": "GfNStL8XJ1111",
    "customer_ip": "111.222.111.123",
    "extra": {
      "sli": "05",
      "cavv": "kAMRDwUADQVXiAPovxs+SQNhfGpb",
      "xid": "",
      "ver": "Y",
      "par": "Y",
      "directory_server_txn_id": "a8a35bcf-21d5-4f55-995a-a4b5e60d356d",
      "threeds_version": "2"
  }
}
```

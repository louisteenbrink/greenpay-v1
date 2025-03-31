---
title: "Using Hosted Payments Page"
slug: "using-hosted-payments-page"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Aug 19 2020 00:51:43 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Apr 29 2021 01:14:50 GMT+0000 (Coordinated Universal Time)"
---
> 🚧 3DS2 via the Hosted Payments is only supported via **fatzebra.js**. If you are currently using a direct integration with the Hosted Payments Page by creating your own iframe and Hosted Payments Page URL you will need to switch over to **fatzebra.js** in order to implement 3DS2

# Overview

Fat Zebra's Hosted Payments Page (HPP) provides a seamless way to perform 3DS2 checks on either new or existing cards before a purchase is made.

When your customers submit a payment, the Fat Zebra Hosted Payments Page form will perform the following operations behind the scenes and emit javascript events so that you can react appropriately:

1. Tokenise the card details entered into the Hosted Payments Page
2. Perform a 3DS2 check against the card (Note: the `enableSca` URL parameter must be set to **true** in order for this to happen, more details in Step 5 below)
3. Upon a successful 3DS2 check, HPP will then make a purchase call with the 3DS2 results to process the payment. If the 3DS2 check is unsuccessful, fatzebra.js will emit an event that you can react to.

> 📘 Before completing the steps below, speak to the Fat Zebra support team to have 3DS2 enabled on your account

### Step 1 - Obtain an OAuth access token

Follow the steps in [Obtain an OAuth token](doc:obtain-oauth-token) to obtain an access token for your checkout session.

### Step 2  - Include fatzebra.js on your page

```html
<script type="text/javascript" src="https://cdn.pmnts-sandbox.io/sdk/v1/fatzebra.js"></script>
```

### Step 3 -  Initialise the FatZebra JS SDK

Initialize the `FatZebra` object in the footer of your page:

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

Available events include:

- [Validation](doc:validation) - for validation errors
- [Tokenization](doc:tokenization) - for success or failure of the tokenization of the card data
- [SCA](doc:sca) - for success or failure of the 3DS2 checks
- [Payment](doc:payment) - for success or failure of the payment

```javascript
// Handle validation related errors, e.g. client-side validation
fz.on('fz.validation.error', function(event) {
  // ...
});

// Receive a FZ card token
fz.on('fz.tokenization.success', function(event) {
  // If required you can save the card token in your backend
});

// Handle errors related to payment processing
fz.on('fz.payment.error', function(event) {
  // Show an error message to the customer
});

fz.on('fz.payment.success', function(event) {
  // checkout ends
});

// Handle errors related to SCA
fz.on('fz.sca.error', function(event) {
  // Show an error message to the customer
});
```

### Step 5 - Load Hosted Payments Page

enableSca: **true** 

See [HppSetupParams](doc:hppsetupparams) for HPP options.

**Note**: The customer object is only required when enableSca is set to **true**.

```javascript
fz.renderPaymentsPage({
  containerId: "fz-paynow",
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
    verification: 'ver_123480' // made up value
  },
  options: { // Hpp display options
    hideButton: false,
    hideLogos: true,
    enableSca: true
  }
});

// Register click event handler to trigger Hosted Payment Page payment flow if
// you have a custom checkout button.
const handler = function() {
  fz.checkout();
}

document.getElementById('checkoutButton').addEventListener('click', handler);
```

Your payment page is now ready for 3DS2 checks. When your customers enter card details and submit a payment, 3DS2 checks will now occur and either prompt the customer for additional verification details (challenge flow) or submit the payment without a customer prompt (frictionless flow).

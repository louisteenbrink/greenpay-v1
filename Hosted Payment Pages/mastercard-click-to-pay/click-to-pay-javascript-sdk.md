---
title: "Click to Pay - JavaScript SDK"
slug: "click-to-pay-javascript-sdk"
excerpt: ""
hidden: false
createdAt: "Sun Nov 05 2023 23:44:00 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 04 2024 01:43:23 GMT+0000 (Coordinated Universal Time)"
---
To use Click to Pay with FatZebra's JavaScript SDK, you call the `renderClickToPay` function:

```javascript javascript
fz.renderClickToPay({
  containerId: 'fz-paynow',
  paymentIntent: {
    payment: {
      amount: 100,
      currency: "AUD",
      reference: "ABCD1234",
    },
    verification: hash,
  }
});
```

The `containerId` parameter here will render the Click to Pay UI within the element with that ID. An example element would be:

```ruby HTML
<div id='fz-paynow'></div>
```

You may wish to pass an email and/or mobile as options to identify a user for the Click to Pay flow

```
fz.renderClickToPay({
  containerId: 'fz-paynow',
  paymentIntent: {
    payment: {
      amount: 100,
      currency: "AUD",
      reference: "ABCD1234",
    },
    verification: hash,	
  },
  options: {
    email: "test@example.com",
    mobile: "0491 571 266",
  }
});
```

Calling this function will render an iframe within the specified element on the page. The User Flow here is identical to how it works on the ["Hosted Payment Page" version ](https://docs.fatzebra.com/reference/click-to-pay-hosted-payment-page)of this form. 

For other options, please see the `options` section below.

## Verification hash calculation

The verification hash is calculated by combining the reference, amount and currency into a string. Using the examples above:

```
ABCD1234:100:AUD
```

This string is then HMAC-MD5 encrypted using your account's shared secret value. If this secret value was `52ccce5a5c5`, then the way to calculate this hash would be:

```
HmacMD5("ABCD1234:100:AUD", "52ccce5a5c5").toString();
```

This would result in the hash of:

```
d02851631e2f836ac10bb33e58687dd4
```

### returnPath option is included in hash calculation

**Note:** if you also include the `returnPath` option, it will be appended to the end of your hash calculation:

```
HmacMD5("ABCD1234:100:AUD:https://example.com/purchase/successful", "52ccce5a5c5").toString();
```

The calculated hash for this is:

```
8db3bc06cf4c87f9ea6ed27bfb1ed4f6
```

### Check your verification hashes

You can check your hash calculation method by using our [Verification Hash Generator](https://fat-zebra-verification.vercel.app/).

## PaymentIntent.Payment

The payment intent options indicate the information about the payment once it gets completed.

| Option      | Description                             |
| :---------- | :-------------------------------------- |
| `amount`    | The amount (in cents) for the purchase. |
| `currency`  | The currency for this amount.           |
| `reference` | A unique reference for this purchase.   |

## Options

The `renderClickToPay` function takes several options.

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Default",
    "0-0": "`auth`",
    "0-1": "boolean",
    "0-2": "If this is set the card being tokenized or the transaction processed will have an auth for the **amount specified in the request** performed. This can be used to verify the card  details are valid before storing.",
    "0-3": "`false`",
    "1-0": "`cardListButtonText`",
    "1-1": "string",
    "1-2": "Sets the button text on the card list step of the flow. Default value is conditional based on `tokenizeOnly` value.",
    "1-3": "Confirm payment / Confirm payment method",
    "2-0": "`css`",
    "2-1": "string",
    "2-2": "HTTPS URL for external CSS - this must be a valid HTTPS URL, and serve up a valid CSS file. Depends on `css_signature`",
    "2-3": "blank",
    "3-0": "`cssSignature`",
    "3-1": "string",
    "3-2": "HMAC-MD5 of the css URL with the shared secret to sign the request.",
    "3-3": "blank",
    "4-0": "`displayName`",
    "4-1": "string",
    "4-2": "Sets the merchant name displayed in the 'Save card for future use' text block when checking out with a new card.",
    "4-3": "merchant trading name",
    "5-0": "`email`",
    "5-1": "string",
    "5-2": "An email address to identify the user for Click to Pay. Used to perform an ID lookup as soon as the component loads. Can be passed at the same time as `mobile`.",
    "5-3": "blank",
    "6-0": "`hideConfirmButton`",
    "6-1": "boolean",
    "6-2": "Determines whether or not to display the \"Confirm Payment\" button after a card has been selected during the Click to Pay flow.",
    "6-3": "`false`",
    "7-0": "`hideManualEntryLink`",
    "7-1": "boolean",
    "7-2": "Hides the \"Enter card details manually\" link at the bottom of all Click to Pay screens.",
    "7-3": "`false`",
    "8-0": "`mobile`",
    "8-1": "string",
    "8-2": "A mobile number to identify the user for Click to Pay. Used to perform an ID lookup as soon as the component loads. Can be passed at the same time as `email`.",
    "8-3": "blank",
    "9-0": "`mrt`",
    "9-1": "string",
    "9-2": "Token generated by the Click to Pay digital checkout flow to assist with user recognition.  ",
    "9-3": "blank",
    "10-0": "`returnPath`",
    "10-1": "string",
    "10-2": "(Used only for complete payment flow). A URL for where to return the user back to once their purchase is complete.  \n  \nIf you do not provide this option, the default \"Receipt Screen\" will appear instead.",
    "10-3": "blank",
    "11-0": "`returnTarget`",
    "11-1": "string, either \"\\_self\" or \"\\_parent\"",
    "11-2": "(Used only for the complete payment flow). Determines which part of the screen will be redirected once the payment completes. Use `_self` if you wish for the iframe to be redirected, or `_parent` if you want the containing page to be redirected instead.",
    "11-3": "defaults to \\_parent behaviour",
    "12-0": "`sharedData`",
    "12-1": "string",
    "12-2": "Comma-separated string that sets the shared data types specified in the 'Save card for future use' text block when checking out with a new card.  \n  \nOptions are:  \n  \n- card (=> \"card details\")  \n- billing (=> \"billing address\")  \n- email (=> \"email\")  \n- mobile (=> \"mobile number\")",
    "12-3": "card,billing,email,mobile",
    "13-0": "`submitPaymentButtonText`",
    "13-1": "string",
    "13-2": "Sets the button text on the new card checkout and manual card entry steps of the flow. Default value is conditional based on `tokenizeOnly` value.",
    "13-3": "Pay Now /  \nAdd payment method",
    "14-0": "`tokenizeOnly`",
    "14-1": "boolean",
    "14-2": "Determines whether a card will only be tokenized (when this is set to `true`), or if a payment will be captured (when this is set to `false`)  \n  \nYou will want to set this option if you wish to modify the payment amount before capturing the full payment, for example if you're applying a surcharge or a discount.",
    "14-3": "`false`"
  },
  "cols": 4,
  "rows": 15,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


**Note on external CSS:** When external CSS specified in the options the hosted payment page a number of verification and sanitisation steps are taken before rendering the CSS in the page, including:

- Verifying the URL specified is served over HTTPS and is in-fact a CSS file
- Verifying that the css_signature matches the URL
- Scrubbing any potentially dangerous CSS statements from the file

After successful verification and sanitising , the filtered CSS is cached by the Hosted Payment Page for 5 minutes. If the cache needs to be updated, the following options are available:

- Change the URL and update the signature to reflect - the CSS cache uses the filename and merchant ID as the cache key, so changing this will force the cache to be updated

## Events

The following events may be subscribed to during the Click to Pay flow:

- `fz.click_to_pay.dcf` - emitted when the Digital Checkout Flow (DCF) is loaded. The card scheme hosting the flow is indicated in the event data.

```
{
  message: 'Digital checkout form loaded.',
  data: {  
    cardScheme: <'visa'|'mastercard'|'amex'>  
  },
}
```

- `fz.click_to_pay.mrt` - emitted if a user elects to be remembered in the browser in a new user checkout/OTP flow AND a recognition token is returned during the Click to Pay checkout. The recognition token value is provided in the event data.
  - When a non-null token value is emitted, it should be persisted as a first-class cookie.
  - When a null token value is emitted (signifying user sign-out), any associated cookie should be removed. 
  - On the call to `renderClickToPay()`, the cookie value should be fetched and passed in via the `mrt`option. This value will then be used to initialise the Click to Pay checkout. 

```
{
  message: 'MRT created.',
  data: {
    mrt: <token value> 
  }
}
```

- `fz.click_to_pay.resize` - emitted when the Click to Pay container is resized. The new container height (in pixels) is provided in the event data. Note that this event will not be emitted when the DCF flow is entered as this content is controlled by the card schemes. We provide the `fz.click_to_pay.dcf`event to notify when this flow is launched, together with the hosting card scheme, to assist with appropriately sizing the container.  

```
{
  message: 'Container resized.',
  data: { 
    heightPx: <number> 
  }
}
```

- `fz.click_to_pay.tokenization.success` - emitted on tokenization success. This event's body and how to use it is explained further in the ["Using Tokenized Cards"](https://docs.fatzebra.com/reference/click-to-pay-using-tokenized-cards)  page.

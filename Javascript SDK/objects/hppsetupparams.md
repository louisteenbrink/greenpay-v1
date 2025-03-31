---
title: "HppSetupParams"
slug: "hppsetupparams"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jul 23 2020 12:30:18 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Oct 25 2023 23:50:39 GMT+0000 (Coordinated Universal Time)"
---
The **HppSetupParams** object defines how the Hosted Payment Page (HPP) should be displayed via fatzebra.js, as well as setting the [PaymentIntent](doc:paymentintent).

`HppSetupParams` is used in the following methods:

- [renderPaymentsPage](doc:renderpaymentspage) 

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
    "1-0": "`customer`",
    "1-1": "[Customer](doc:customer)",
    "1-2": "See [Customer](https://docs.fatzebra.com/docs/customer)",
    "1-3": "required",
    "1-4": "",
    "2-0": "`paymentIntent`",
    "2-1": "[PaymentIntent](doc:paymentintent)",
    "2-2": "See [PaymentIntent](doc:paymentintent)",
    "2-3": "required",
    "2-4": "",
    "3-0": "`options.buttonText`",
    "3-1": "string",
    "3-2": "Specifies the text to be displayed for the submit button (e.g. Pay Now or Submit)  \n  \nOnly applicable when hideButton is `false`",
    "3-3": "optional",
    "3-4": "empty",
    "4-0": "`options.cards`",
    "4-1": "string, comma separated",
    "4-2": "Specifies a whitelist or blacklist of accepted cards.  \n  \nIf the string is prefixed with an exclamation mark `!` the cards listed will not be permitted  \n  \nPossible values are:  \n  \n`AMEX`, `JCB`, `VISA`, `MasterCard`, `Diners`, `Discover`, `China UnionPay`  \n  \nExamples  \n  \n!`AMEX,JCB` - both AMEX and JCB are disabled  \n  \n`VISA,AMEX` - only enable VISA and AMEX  \n  \nNote if this field is present it is included in the end of the verification value string",
    "4-3": "optional",
    "4-4": "empty",
    "5-0": "`options.css`",
    "5-1": "string",
    "5-2": "HTTPS URL for external CSS. This must be a valid HTTPS URL that serves valid CSS. If specified, `cssSignature` is also required.",
    "5-3": "optional",
    "5-4": "empty",
    "6-0": "`options.cssSignature`",
    "6-1": "string",
    "6-2": "HMAC-MD5 of the css URL with the shared secret to sign the request",
    "6-3": "optional",
    "6-4": "empty",
    "7-0": "`options.hideButton`",
    "7-1": "boolean",
    "7-2": "Hides the button from the checkout form for when the checkout should be triggered by a purchase",
    "7-3": "optional",
    "7-4": "false",
    "8-0": "`options.hideCardHolder`",
    "8-1": "boolean",
    "8-2": "Hides the card holder entry field. If provided, needs to be in the verification hash calculation.",
    "8-3": "optional",
    "8-4": "false",
    "9-0": "`options.hideLogos`",
    "9-1": "boolean",
    "9-2": "",
    "9-3": "optional",
    "9-4": "true",
    "10-0": "`options.logoUrl`",
    "10-1": "string",
    "10-2": "HTTPS URL for the merchant logo. This must be a valid HTTPS URL that serves an image file.",
    "10-3": "optional",
    "10-4": "empty",
    "11-0": "`options.showEmail`",
    "11-1": "boolean",
    "11-2": "Indicates whether to show and require the email field or not",
    "11-3": "optional",
    "11-4": "false",
    "12-0": "`options.showExtras`",
    "12-1": "boolean",
    "12-2": "Indicates whether to display the invoice number and the amount to the customer",
    "12-3": "optional",
    "12-4": "false",
    "13-0": "`options.tokenizeOnly`",
    "13-1": "boolean",
    "13-2": "When set to `true`, HPP will only tokenise the card and return the token via `fz.tokenization.success` event. 3DS/SCA and purchase will not run.",
    "13-3": "optional",
    "13-4": "false",
    "14-0": "`options.enableSca`",
    "14-1": "boolean",
    "14-2": "When set to `true`,  3DS/SCA will run after card tokenisation and before payment is made  \n  \nWhen `false`, a payment will be made after card tokenisation  \n  \nPlease note that 3DS/SCA will not run when both `tokenizeOnly` and `enableSca` are set to `true`",
    "14-3": "optional",
    "14-4": "false",
    "15-0": "`options.challengeWindowSize`",
    "15-1": "string",
    "15-2": "The sizes are width x height in pixels of the window displayed in the cardholder browser.  \n  \n2-character long string  \nAvailable values are  \n  \n`'01'`: 250x400  \n`'02'`: 390x400  \n`'03'`: 500x600  \n`'04'`: 600x400  \n`'05'`: Full page (recommended)",
    "15-3": "optional",
    "15-4": "'05'"
  },
  "cols": 5,
  "rows": 16,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


```json Example
const fz = new FatZebra({
  username: "MerchantXYZ"
});

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
    verification: "ver_123480"
  },
  options: { // Hpp display options
    hideButton: false,
    hideLogos: true,
    enableSca: true
  }
});
```

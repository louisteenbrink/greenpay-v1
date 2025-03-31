---
title: "Click to Pay - Configuration"
slug: "click-to-pay-configuration"
excerpt: ""
hidden: false
createdAt: "Sun Nov 12 2023 22:10:12 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Sep 10 2024 04:37:01 GMT+0000 (Coordinated Universal Time)"
---
The following configuration documentation is for all forms of Click to Pay.

## URLs

There are two different URLs for the PayNow service - one for the Sandbox environment and one for the Live environment:

| Environment | BASE URL                                        |
| :---------- | :---------------------------------------------- |
| Sandbox     | `https://paynow.pmnts-sandbox.io/v3/clicktopay` |
| Live        | `https://paynow.pmnts.io/v3/clicktopay`         |

## Request

In order to direct the customer to the hosted payment page the merchants website should prepare the following URL and either use this as the redirect destination, or as the iframe source:

`https://paynow.pmnts.io/v3/clicktopay/[username]/[reference]/[currency]/[amount]/[hash]`

### User identification URL Parameters

The Click to Pay integration also allows you to pass in two parameters to identify your users.

| Name   | Type   | Description                                                                                                                   |
| :----- | :----- | :---------------------------------------------------------------------------------------------------------------------------- |
| email  | string | The email address for your user                                                                                               |
| mobile | string | The mobile number for your user. Can either be in a format of `0491 570 006` or can include a country code: `+61 491 570 006` |

If you pass both, a lookup will be attempted first for email, and then mobile. 

### URL Parameters

The following parameters are required and are used to build the URL which the user should be redirected to (or as the source for the IFRAME):

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "username",
    "0-1": "string",
    "0-2": "The merchants Fat Zebra username",
    "1-0": "reference",
    "1-1": "string",
    "1-2": "The invoice number or order reference",
    "2-0": "currency",
    "2-1": "string (3 characters)",
    "2-2": "The [ISO-4217](http://en.wikipedia.org/wiki/ISO_4217#Active_codes) 3-letter currency code for the transaction",
    "3-0": "amount",
    "3-1": "number",
    "3-2": "The amount of the transaction, as a decimal value.  \n  \nFor currencies which do not make use of the decimal/cent value this should be omitted as 00 (e.g. 300.00 for ¥300)",
    "4-0": "hash",
    "4-1": "string",
    "4-2": "The hash is a MD5 hexdigest of a string compiled from the request parameters.  \nSee below (**Verification Value Calculation**) for more details."
  },
  "cols": 3,
  "rows": 5,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


### Options

Provide any of the following as query parameters to specify display options - these are **optional** parameters:

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Default",
    "0-0": "auth",
    "0-1": "boolean",
    "0-2": "If this is set the card being tokenized or the transaction processed will have an auth for the **amount specified in the request** performed. This can be used to verify the card details are valid before storing.",
    "0-3": "false",
    "1-0": "card_list_button_text",
    "1-1": "string",
    "1-2": "Sets the button text on the card list step of the flow. Default value is conditional based on `tokenizeOnly` value.",
    "1-3": "Confirm payment / Confirm payment method",
    "2-0": "css",
    "2-1": "string",
    "2-2": "HTTPS URL for external CSS - this must be a valid HTTPS URL, and serve up a valid CSS file. Depends on `css_signature`",
    "2-3": "empty",
    "3-0": "css_signature",
    "3-1": "string",
    "3-2": "HMAC-MD5 of the css URL with the shared secret to sign the request.",
    "3-3": "empty",
    "4-0": "display_name",
    "4-1": "string",
    "4-2": "Sets the merchant name displayed in the 'Save card for future use' text block when checking out with a new card.",
    "4-3": "merchant trading name",
    "5-0": "email",
    "5-1": "string",
    "5-2": "An email address to identify the user for Click to Pay. Used to perform an ID lookup as soon as the component loads. Can be passed at the same time as `mobile`.",
    "5-3": "empty",
    "6-0": "hide_confirm_button",
    "6-1": "boolean",
    "6-2": "Hides the \"Confirm Payment\" button on the final \"Confirmation\" step of the Click to Pay checkout form for when the checkout should be triggered by the parent frame (via a postmessage)",
    "6-3": "false",
    "7-0": "hide_manual_entry_link",
    "7-1": "boolean",
    "7-2": "Hides the \"Enter card details manually\" link at the bottom of all Click to Pay screens.",
    "7-3": "false",
    "8-0": "iframe",
    "8-1": "boolean",
    "8-2": "If you're rendering Click to Pay in an iframe, this will need to be set to `true`.",
    "8-3": "false",
    "9-0": "mobile",
    "9-1": "string",
    "9-2": "A mobile number to identify the user for Click to Pay. Used to perform an ID lookup as soon as the component loads. Can be passed at the same time as `email`.",
    "9-3": "empty",
    "10-0": "return_path",
    "10-1": "string",
    "10-2": "The return URL for the transaction success - if this is omitted the result will be displayed on screen to the customer  \n**Note**: if the a URL is specified it must be included in the verification hash. This may be a non-resolving URL for callback handling in mobile  \napplications if required (e.g. paymentcallback://....)",
    "10-3": "empty",
    "11-0": "return_target",
    "11-1": "string",
    "11-2": "The target for the form post (e.g. post back to `_parent`, `_self` or specified)",
    "11-3": "empty",
    "12-0": "shared_data",
    "12-1": "string",
    "12-2": "Comma-separated string that sets the shared data types specified in the 'Save card for future use' text block when checking out with a new card.  \n  \nOptions are:  \n  \n- card (=> \"card details\")  \n- billing (=> \"billing address\")  \n- email (=> \"email\")  \n- mobile (=> \"mobile number\")",
    "12-3": "card,billing,email,mobile",
    "13-0": "submit_payment_button_text",
    "13-1": "string",
    "13-2": "Sets the button text on the new card checkout and manual card entry steps of the flow. Default value is conditional based on `tokenizeOnly` value.",
    "13-3": "Pay Now /  \nAdd payment method",
    "14-0": "tokenize_only",
    "14-1": "boolean",
    "14-2": "Used to store just the card details themselves, without authorizing or capturing a purchase.",
    "14-3": "false"
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

### Verification Value Calculation

There are two points of verification for requests - once when the request is received by Fat Zebra (when the hosted page is rendered to the user), and once when the response is returned to the merchant - it is important that the response is verified by the merchant to ensure that the response has not been tampered with by malicious users.

#### Request Verification (Redirect to Fat Zebra)

The request received by Fat Zebra will be verified with the following steps:

1. The reference, currency, amount will be concatenated into a string, joined by colons:

```
https://paynow.pmnts.io/v3/clicktopay/samsbooks/INV1121/AUD/100.25/xxxxxxxxxxx -> "INV1121:100.25:AUD"
```

2. The value of this string will then be hashed with a HMAC-MD5, using the shared-secret known by Fat Zebra and the merchant (please contact Fat Zebra Support if you are unsure of where to find this shared secret).

```
shared_secret = "<<sharedSecret>>"
verification = hmac_md5(shared_secret, "INV1121:100.25:AUD")
```

#### Response Verification (Purchases)

For purchases the response verification will consist of the response code, success indicator, amount, currency, transaction ID and the card token:

```
https://www.samsbooks.com/payment/callback?r=1&successful=true&amount=10025&currency=AUD&id=001-P-ABCDG1124&token=abcd1234&v=xxxxx....... -> "1:true:10025:AUD:001-P-ABCDG1123:abcd1234"
shared_secret = "<<sharedSecret>>"
verification = hmac_md5(shared_secret, "1:true:10025:AUD:001-P-ABCDG1123:abcd1234")
 
# v == verification should be true
```

The response for purchases will also include the following:

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "message",
    "0-1": "string",
    "0-2": "Any messages relating to the transaction",
    "1-0": "amount",
    "1-1": "integer",
    "1-2": "The amount, as an integer",
    "2-0": "reference",
    "2-1": "string",
    "2-2": "The transaction reference",
    "3-0": "id",
    "3-1": "string",
    "3-2": "The Fat Zebra transaction ID",
    "4-0": "currency",
    "4-1": "string",
    "4-2": "The [ISO-4217](http://en.wikipedia.org/wiki/ISO_4217#Active_codes) 3-letter currency code for the transaction",
    "5-0": "card_number",
    "5-1": "string",
    "5-2": "The masked credit card number (e.g. 512345XXXXXXXX2346)",
    "6-0": "card_holder",
    "6-1": "string",
    "6-2": "The card holders name",
    "7-0": "card_expiry",
    "7-1": "date (mm/yyyy)",
    "7-2": "The card expiry date",
    "8-0": "card_type",
    "8-1": "string",
    "8-2": "The card type of the credit card used. Possible values are:  \nVISA, MasterCard",
    "9-0": "successful",
    "9-1": "boolean",
    "9-2": "Indicator of transaction success"
  },
  "cols": 3,
  "rows": 10,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

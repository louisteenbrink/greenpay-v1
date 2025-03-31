---
title: "V3 - Overview"
slug: "v3-overview"
excerpt: "Fat Zebra provides a hosted payment page for merchants who wish to remove all PCI-DSS scope from their systems. This is known commercially as PayNow. Please note that merchants and service providers are required to complete Self-Assessment Questionnaire A to adhere to PCI DSS Compliance."
hidden: false
createdAt: "Tue May 09 2023 00:52:14 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Jul 08 2024 06:25:00 GMT+0000 (Coordinated Universal Time)"
---
Currently the hosted payment page supports three methods of implementation:

- Standard Hosted Page (i.e. redirection from the merchants website to the payment page)
- IFrame embedded page
- Accounting platform payment page (for example Xero or Saasu) 

The V3 UI looks like this, but it can be re-styled using the `css` parameter, documented below:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2f18059-image.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


## Usage

The data sent between the merchant and Fat Zebra, and from Fat Zebra to the merchant is sent in the request URL - to ensure that this has not been tampered with the payload includes a verification value, which is a signed-hash based on the payload values, using a shared secret between the merchant and Fat Zebra. This process has been closely modeled on the Fat Zebra Direct Post method - it is recommend you review this documentation for further details which may not be covered here.

## URLs

There are two different URLs for the PayNow service - one for the Sandbox environment and one for the Live environment:

| Environment | BASE URL                             |
| :---------- | :----------------------------------- |
| Sandbox     | `https://paynow.pmnts-sandbox.io/v3` |
| Live        | `https://paynow.pmnts.io/v3`         |

## Request

In order to direct the customer to the hosted payment page the merchants website should prepare the following URL and either use this as the redirect destination, or as the IFRAME source:

`https://paynow.pmnts.io/v3/[username]/[reference]/[currency]/[amount]/[hash]`

### URL Parameters

The following parameters are required and are used to build the URL which the user should be redirected to (or as the source for the IFRAME):

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "amount",
    "0-1": "number",
    "0-2": "The amount of the transaction, as a decimal value.  \n  \nFor currencies which do not make use of the decimal/cent value this should be omitted as 00 (e.g. 300.00 for ¥300)",
    "1-0": "hash",
    "1-1": "string",
    "1-2": "The hash is a MD5 hexdigest of a string compiled from the request parameters.  \nSee below (**Verification Value Calculation**) for more details.",
    "2-0": "reference",
    "2-1": "string",
    "2-2": "The invoice number or order reference",
    "3-0": "currency",
    "3-1": "string (3 characters)",
    "3-2": "The [ISO-4217](http://en.wikipedia.org/wiki/ISO_4217#Active_codes) 3-letter currency code for the transaction",
    "4-0": "username",
    "4-1": "string",
    "4-2": "The merchants Fat Zebra username"
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
    "0-0": "iframe",
    "0-1": "boolean",
    "0-2": "Indicates whether to show the stripped-down iframe layout or not",
    "0-3": "false",
    "1-0": "show_email",
    "1-1": "boolean",
    "1-2": "Indicates whether to show and require the email field or not",
    "1-3": "true",
    "2-0": "show_extras",
    "2-1": "boolean",
    "2-2": "Indicates whether to display the invoice number and the amount to the customer",
    "2-3": "true",
    "3-0": "return_path",
    "3-1": "string",
    "3-2": "The return URL for the transaction success - if this is omitted the result will be displayed on screen to the customer  \nNote: if the a URL is specified it must be included in the verification hash. This may be a non-resolving URL for callback handling in mobile  \napplications if required (e.g. paymentcallback://....)",
    "3-3": "empty",
    "4-0": "tokenize_only",
    "4-1": "boolean",
    "4-2": "If this is set the card will not be charged, and will only be tokenized for future use",
    "4-3": "false",
    "5-0": "auth",
    "5-1": "boolean",
    "5-2": "If this is set the card being tokenized or the transaction processed will have an auth for the **amount specified in the request** performed. This can be used to verify the card  \ndetails are valid before storing.",
    "5-3": "false",
    "6-0": "button_text",
    "6-1": "string",
    "6-2": "Specifies the text to be displayed for the submit button (e.g. Pay Now or Submit)",
    "6-3": "Pay Now",
    "7-0": "return_target",
    "7-1": "string",
    "7-2": "When used in iframe mode (iframe=true) specifies where the target for the form post (e.g. post back to \\_parent, \\_self or speficied)",
    "7-3": "empty",
    "8-0": "postmessage",
    "8-1": "boolean",
    "8-2": "When used in iframe mode (iframe=true) specifies that the response should be sent using postMessage instead of redirecting",
    "8-3": "false",
    "9-0": "css",
    "9-1": "string",
    "9-2": "HTTPS URL for external CSS - this must be a valid HTTPS URL, and serve up a valid CSS file. Depends on css_signature",
    "9-3": "empty",
    "10-0": "css_signature",
    "10-1": "string",
    "10-2": "HMAC-MD5 of the css URL with the shared secret to sign the request.  \n  \nFor example, the CSS signature for <https://example.com/example.css> with a shared secret of \"TEST\" would be:  \n  \n`21387fed0d8f862e19a79b346eb710b8`  \n  \nImportantly: this hash is not a hash of the _contents_ of the CSS file -- only the URL of the CSS file.",
    "10-3": "empty",
    "11-0": "logo_url",
    "11-1": "string",
    "11-2": "HTTPS URL for the merchant logo. This must be a valid HTTPS URL and serve up a valid image file.",
    "11-3": "empty",
    "12-0": "hide_button",
    "12-1": "boolean",
    "12-2": "Hides the button from the checkout form for when the checkout should be triggered by postMessage. Note this option is dependent on the v2 layout.",
    "12-3": "false",
    "13-0": "cards",
    "13-1": "string, comma separated",
    "13-2": "Specifies the whitelist or blacklist of accepted cards. If the string is prefixed with an exclamation mark (!) the cards listed will not be permitted.  \nPossible values are: AMEX, JCB, VISA, MasterCard, Diners  \n  \n**Examples**  \n  \n!AMEX,JCB - disabled AMEX and JCB  \n  \nVISA,AMEX - enabled only VISA and AMEX  \n  \n**Note** if this field is present it is included in the end of the verification value string.",
    "13-3": "empty",
    "14-0": "surcharge",
    "14-1": "boolean",
    "14-2": "Specifies if a surcharge will be applied. Surcharge rates are set in the Surcharging section of the Merchant Dashboard.  \n  \n**Note**: if the surcharge field is set to true, “:true” must be appended in the verification hash.",
    "14-3": "false",
    "15-0": "hide_card_holder",
    "15-1": "boolean",
    "15-2": "Specifies if the card holder name field should be hidden",
    "15-3": "false"
  },
  "cols": 4,
  "rows": 16,
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

1. The reference, currency, amount, and if present, hide_card_holder and return_path will be concatenated into a string, joined by colons:

```
https://paynow.pmnts.io/v3/samsbooks/INV1121/AUD/100.25/xxxxxxxxxxx&hide_card_holder=true -> "INV1121:100.25:AUD:true"
```

If hide_card_holder and/or return_path is not included, they will be omitted:

```
https://paynow.pmnts.io/v3/samsbooks/INV1121/AUD/100.25/xxxxxxxxxxx&hide_card_holder=true -> "INV1121:100.25:AUD"
```

2. The value of this string will then be hashed with a HMAC-MD5, using the shared-secret known by Fat Zebra and the merchant (please contact Fat Zebra Support if you are unsure of where to find this shared secret).

```
shared_secret = "<<sharedSecret>>"
verification = hmac_md5(shared_secret, "INV1121:100.25:AUD:true")
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
    "8-2": "The card type of the credit card used. Possible values are:  \nVISA, MasterCard, AMEX, JCB, Diners, Discover, China UnionPay, Unknown",
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


#### Response Verification (Tokenization)

For tokenization the response verification will consist of the response code, and the card token:

```
https://www.samsbooks.com/payment/callback?r=1&token=abcd1234&v=xxxxxxxxx........ -> "1:abcd1234"
shared_secret = "<<sharedSecret>>"
verification = hmac_md5(shared_secret, "1:abcd1234")
# v == verification should be true
```

The response for tokenization will also include the following:

| Name        | Type           | Description                                             |
| :---------- | :------------- | :------------------------------------------------------ |
| card_number | string         | The masked credit card number (e.g. 512345XXXXXXXX2346) |
| card_holder | string         | The card holders name                                   |
| card_expiry | date (mm/yyyy) | The card expiry date                                    |
| token       | string         | The token representing the card in Fat Zebra systems    |

### Response Codes

The following response codes are used when a redirect URL is provided:

| Code | Description                                                                                             |
| :--- | :------------------------------------------------------------------------------------------------------ |
| 1    | Successful                                                                                              |
| 2    | Declined - examine the message parameter for possible explanations                                      |
| 94   | Cancelled - the merchant clicked the Cancel button on the payment or checkout form                      |
| 95   | Merchant Not Found - possible incorrect username                                                        |
| 96   | Reference not unique                                                                                    |
| 97   | Validation error - check the errors\[] parameters for error messages                                    |
| 99   | Invalid Verification - the verification value does not match the parameters supplied                    |
| 999  | Gateway error - an unknown error has occurred and the merchant should investigate with Fat Zebra Suppor |

## Testing

Standard Fat Zebra test procedures apply for the Hosted Payment Page. You can use [our test card numbers](https://docs.fatzebra.com/docs/test-card-numbers) to check the behaviour of the hosted payment page.

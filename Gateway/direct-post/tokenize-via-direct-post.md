---
title: "Tokenize via Direct Post"
slug: "tokenize-via-direct-post"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Mar 01 2018 05:36:48 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Nov 24 2020 23:58:09 GMT+0000 (Coordinated Universal Time)"
---
## Request

When performing a Direct Post Tokenization the following parameters are required:

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "card_holder",
    "0-1": "String",
    "0-2": "The credit card holders name",
    "1-0": "card_number",
    "1-1": "String",
    "1-2": "The credit card number",
    "2-0": "expiry_month",
    "2-1": "Number",
    "2-2": "The card expiry month, 1 or 2 digits (e.g. 5, 12, 06)",
    "3-0": "expiry_year",
    "3-1": "Number",
    "3-2": "The card expiry year, 4 digits (eg. 2023)",
    "4-0": "cvv",
    "4-1": "String",
    "4-2": "The CVV or Security Code on the back of the card - 3 digits  \nAMEX Note: this number is printed on the front of an AMEX and is 4 digits in length.",
    "5-0": "is_billing",
    "5-1": "Boolean",
    "5-2": "For Recurring transactions this field can be included set to true, which will make the cvv field optional. Defaults to `false`"
  },
  "cols": 3,
  "rows": 6,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


In addition to these fields the following hidden fields should also be included:

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "return_path",
    "0-1": "String",
    "0-2": "The URL to redirect the customer to with the response.  \nThis will normally be a URL on the merchants website but it can also be a custom-scheme registered for mobile applications.",
    "1-0": "verification",
    "1-1": "String",
    "1-2": "The verification value. Details on how to calculate this are below."
  },
  "cols": 3,
  "rows": 2,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


The URL for the Direct Post form should be: 

**Sandbox**: `https://gateway.pmnts-sandbox.io/v2/credit_cards/direct/[MERCHANT USERNAME].json`  
**Live**: `https://gateway.pmnts.io/v2/credit_cards/direct/[MERCHANT USERNAME].json`

## Calculating the Verification Value

There are several hidden fields in this form which are submitted to the Gateway from the customers browser. These are:

- **return_path** - the URL to return the customer to on completion

In order to ensure these values are not changed a verification value is also included, which is determined by the following:

```text
verification = hmac_md5(shared_secret, "https://merchantswebsite.com/credit_card/callback");
```

## Response

Upon completion of the request the customer will be redirected back to the merchants website with a number of key/value pairs in the query string. These will be:

```text
r=1&successful=true&amount=100000&currency=AUD&id=071-P-W2MZP0IJ&v=c41844a09c1a14f484e94d3458a13930&token=w5o87fzy&message=Approved&card_holder=Jim+Citizen&card_number=512345XXXXXX2346&card_expiry=03%2F2018&reference=INV-21479&s=-1
```

| Name        | Type          | Description                                                                                                                    |
| :---------- | :------------ | :----------------------------------------------------------------------------------------------------------------------------- |
| r           | Number        | Response code indicating the outcome of the request - see the list below for details.                                          |
| token       | String        | The credit card token                                                                                                          |
| card_holder | String        | The card holders name                                                                                                          |
| card_number | String        | The masked card number - this can be stored if required                                                                        |
| card_expiry | String        | The card expiry date - this can be stored if required                                                                          |
| v           | String        | The verification value used to verify the response integrity - see below for details on verification                           |
| errors\[]   | Array<String> | Any errors related to the request - this will be populated if the response code is 90-999 (e.g. errors\[]=Invalid+Card+Number) |

## Response Codes

The following response codes are used for Direct Post transactions:

| Code | Description                                                                                                |
| :--- | :--------------------------------------------------------------------------------------------------------- |
| 1    | Successful Tokenization                                                                                    |
| 95   | Merchant Username not found                                                                                |
| 97   | Validation error - there was an error validating the customers input (e.g. bad card number)                |
| 99   | Invalid Verification - the verification was not successful indicating the data may have been tampered with |
| 999  | Gateway Error - contact support if this error persists                                                     |

## Response Verification

To verify the response hasn't been tampered with the merchants integration should perform the following verification calculation, and compare the result against the value of **v**:

`hmac_md5(shared_secret, "[r]:[token]")`

If these values do not match the response should be considered invalid. 

It is also important that a merchant's system be idempotent with handling responses, so that if a customer reloads the page they are redirected to the system will not treat each request as a new order.

## Echo Parameters

In addition to the parameters mentioned above we now support echo parameters, which are values returned in the transaction.

To use these simply include them in your form using the following format for the field name `echo[your_param_name]` and they will be included in the response URI.

As with the extra parameters above, the echo parameters are **not** included in the verification calculation.

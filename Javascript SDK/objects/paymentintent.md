---
title: "PaymentIntent"
slug: "paymentintent"
excerpt: ""
hidden: false
createdAt: "Thu Jul 23 2020 11:46:40 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Oct 10 2024 00:26:28 GMT+0000 (Coordinated Universal Time)"
---
The **PaymentIntent** object contains payment data. To ensure that this payment data is not tampered with (e.g. a customer amends the amount to be smaller), the `PaymentIntent` requires a HMAC `verification` field to be conducted in your backend using your Pay Now secret. 

`PaymentIntent` is used in the following methods.

- [load](https://docs.fatzebra.com/docs/load)
- [verifyCard](doc:verifycard) 

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`payment.amount`",
    "0-1": "number",
    "0-2": "Amount in subunit (non-decimal)",
    "1-0": "`payment.currency`",
    "1-1": "string",
    "1-2": "[ISO-4217 country codes](https://docs.fatzebra.com/docs/iso-currency-codes)",
    "2-0": "`payment.reference`",
    "2-1": "string",
    "2-2": "Reference or invoice number for the payment transaction/",
    "3-0": "`payment.hide_card_holder`",
    "3-1": "boolean",
    "3-2": "Determines if the \"Card Holder\" field should be shown on the page or not. **If this is included and true, it must be appended to the end of the verification hash**. See \"Verification Value Hash Calculation\" below for more details.",
    "4-0": "`verification`",
    "4-1": "string",
    "4-2": "For payments:  \nHash of amount, reference, currency.  \n  \nFor verifyCard [verifyCard](doc:verifycard):  \nHash of card_token  \n  \nSee **Verification Value Hash Calculation** below for more details on how to calculate this value."
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


```json Example
{
  payment: {
    amount: 10025,
    currency: "AUD",
    reference: "INV1121"
  },
  verification: "xxxxxx"
}
```

## Verification Value Hash Calculation

> ❗️ The Verification Value Hash should only ever be calculated on your backend server, and never in client-side code.
> 
> This is because your Pay Now token is a secret value that only you should know. Calculating the Verification Value Hash on the client-side (e.g. in client-side Javascript) would make your Pay Now token secret visible to public via browser developer tools.

Below is pseudo code demonstrating how the verification hash is calculated using a PayNow token. The Pay Now token can be obtained from the [Fat Zebra Merchant Dashboard](https://dashboard.fatzebra.com.au).

### VerifyCard

Please make sure that the hash calculation is **only** the shared_secret, card token

```ruby Ruby
shared_secret = "abc123" # Also known as your Pay Now token
card_token = "xyc12ce" # FatZebra issued token representing a debit or credit card

verification = hmac_md5(shared_secret, card_token)
# Expected value: 8cf7e7d50664d118c41a70b1ba22d916
```

### Payments

Please make sure that reference (invoice #), amount (subunit) and currency are in the correct order as shown:

```ruby
shared_secret = "abc123" # Also known as your Pay Now token

invoice_no = "INV4567" # Also known as reference
amount = "1000"
currency = "AUD"
hide_card_holder = true

hmac = HMAC::MD5.new(shared_secret)
data = [invoice_no, amount, currency]
data << [hide_card_holder] if hide_card_holder

# Data will be:
# INV4567:1000:AUD:true
verification = hmac_md5(shared_secret, data.join(":"))
# Expected value: c045c96c113ae660b91b60bd09feda20
# Hash will be 0a40877ca9f75152f27bf093af7fd44b if hide_card_holder is false
```

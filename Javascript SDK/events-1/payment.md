---
title: "Payment"
slug: "payment"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Jul 24 2020 02:05:18 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Jun 17 2021 06:30:52 GMT+0000 (Coordinated Universal Time)"
---
| Event                | Description                                     | Applicable Methods                           |
| :------------------- | :---------------------------------------------- | :------------------------------------------- |
| `fz.payment.success` | Emitted when payment is processed successfully. | [renderPaymentsPage](doc:renderpaymentspage) |
| `fz.payment.error`   | Emitted when a payment transaction failed.      | [renderPaymentsPage](doc:renderpaymentspage) |

## fz.payment.success data payload

```json fz.payment.success data payload
{
  "message": "Payment successful.",
  "data": {
    "transactionId": "40057-P-F7R7M9Q6",
    "responseCode": "00",
    "message": "Approved",
    "amount": 100,
    "currency": "AUD",
    "reference": "sgc99pycds20i97q",
    "cardNumber": "400000XXXXXX1091",
    "cardHolder": "XXX",
    "cardExpiry": "2023-12-31",
    "cardType": "VISA",
    "verification": "0aa8154b8cf0fe4168af0e3d0d752d10"
  }
}
```

It is recommended that you verify the returned data against the calculated verification (see below) before consumption.

## fz.payment.error data payload

```json fz.payment.error data payload
{
  "message": "Refer to Card Issuer",
  "data": {
    "transactionId": "40057-P-F7R7M9Q6",
    "responseCode": "05",
    "message": "Declined",
    "amount": 100,
    "currency": "AUD",
    "reference": "sgc99pycds20i97q",
    "cardNumber": "400000XXXXXX1091",
    "cardHolder": "XXX",
    "cardExpiry": "2023-12-31",
    "cardType": "VISA",
    "verification": "0aa8154b8cf0fe4168af0e3d0d752d10"
  }
}
```

## Transaction Data

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`transactionId`",
    "0-1": "string",
    "0-2": "Payment transaction id",
    "1-0": "`responseCode`",
    "1-1": "string",
    "1-2": "",
    "2-0": "`message`",
    "2-1": "string",
    "2-2": "",
    "3-0": "`amount`",
    "3-1": "number",
    "3-2": "amount in subunit.  \ne.g. AUB $10.25 -> 1025",
    "4-0": "`currency`",
    "4-1": "string",
    "4-2": "currency code. e.g. AUD",
    "5-0": "`reference`",
    "5-1": "string",
    "5-2": "payment reference or invoice #.",
    "6-0": "`cardNumber`",
    "6-1": "string",
    "6-2": "masked card number",
    "7-0": "`cardHolder`",
    "7-1": "string",
    "7-2": "card holder name",
    "8-0": "`cardExpiry`",
    "8-1": "string",
    "8-2": "card expiry date.  \nyyyy-mm-dd",
    "9-0": "`cardType`",
    "9-1": "string",
    "9-2": "card type.  \ne.g. VISA, MasterCard, etc",
    "10-0": "`verification`",
    "10-1": "string",
    "10-2": "calculated verification hash."
  },
  "cols": 3,
  "rows": 11,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


## Verification hash calculation

values = [transactionId]\:[responseCode]\:[message]\:[amount]\:[currency]\:[reference]\:[cardNumber]\:[cardHolder]\:[cardExpiry]\:[cardType]

shared_secret = <obtained from merchant dashboard or partner webhook>

verification = MD5(values, shared_secret)

**For example:**

values = "40057-P-F7R7M9Q6","00":"Declined": 100 :"AUD":"sgc99pycds20i97q":"400000XXXXXX1091":"XXX":"2023-12-31":"VISA":"0aa8154b8cf0fe4168af0e3d0d752d10"

shared_secret = "123"

verification = MD5(values, shared_secret)

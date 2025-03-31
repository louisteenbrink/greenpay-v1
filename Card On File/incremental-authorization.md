---
title: "Incremental Authorization"
slug: "incremental-authorization"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jun 03 2021 04:42:03 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Jun 03 2021 05:13:26 GMT+0000 (Coordinated Universal Time)"
---
Merchant can make incremental authorization to change the amount of authorization in the lifecycle of the authorization.

There are two types of incremental authorization:

1. Top up the amount - This increases the amount of the pre-authorization, and extend the chargeback expiry date.
2. Update the pre-authorization expiry date - This only extends the pre-authorization expiry date.

Note: 

- By default, pre-authorization stays for 7 days, and every extension will extend it by 7 days.
- Extension can only be done before it is expired.

## Incremental Auth Example

Below is a scenario example to illustrate how to do a top up and extend the chargeback expiry date

### Pre-authorization Transaction

You can reference [Create an authorization](ref:create-an-authorization) for more details. To show it is a pre-authorization, set `capture: false`.

```json Pre-authorization
/* 
 * Request: POST /v1.0/purchases
 */
{
  "amount": 100,
  "currency": "AUD",
  "card_holder": "John Smith",
  "card_number": "411111xxxxxx1111",
  "card_expiry": "01/2025",
  "cvv": "123",
  "reference": "first_preauth_transaction",
  "capture": false
}
```

```json Pre-authorization Response
/*
 * Response
 */
{
  "successful": true,
  "response": {
    "authorization": "123456",
    "id": "1-P-VBF4KCE9",
    "card_number": "411111xxxxxx1111",
    "card_holder": "John Smith",
    "card_expiry": "2025-01-31",
    "card_token": "lk78b0xadcdek2hffvkadif",
    "card_type": "VISA",
    "card_category": "Credit",
    "card_subcategory": "Standard",
    "amount": 100,
    "decimal_amount": 1.0,
    "successful": true,
    "message": "approved - balance avail",
    "reference": "first_preauth_transaction",
    "currency": "AUD",
    "transaction_id": "1-P-VBF4KCE9",
    "settlement_date": "2020-04-23",
    "transaction_date": "2020-04-23T10:21:31+10:00",
    "response_code": "00",
    "captured": false,
    "captured_amount": 100,
    "rrn": "042321000062",
    "cvv_match": "M",
    "metadata": {
      "authorization_tracking_id": "HNR0003960518",
      "card_sequence_number": "",
      "sca_exemption": "",
      "original_transaction_reference": ""
    },
    "addendum_data": {}
  },
  "errors": [],
  "test": false
}
```

### Top-up Transaction (incremental auth)

To top up the transaction, you have to provide an amount that is bigger than the original amount. In this case, we need to provide a value bigger than 100. Let's assume we need to increment the transaction by $1.00, then we should send 200. See more details in [Update an authorization](ref:update-an-authorization) 

Note that you will need to provide the previous response ID "1-P-VBF4KCE9" in the url.

```json Top Up Payment
/* 
 * Request: PUT /v1.0/purchases/1-P-VBF4KCE9
 */
{ 
  "amount": 200
}
```

Now the pre-authorization is extended to $2.00, and the new expiry date is 7 days after this transaction time.

```json Top Up Payment Response
{
  "successful": true,
  "response": {
    "authorization": "123456",
    "id": "1-P-VBF4KCE9",
    "card_number": "411111xxxxxx1111",
    "card_holder": "John Smith",
    "card_expiry": "2025-01-31",
    "card_token": "lk78b0xadcdek2hffvkadif",
    "card_type": "VISA",
    "card_category": "Credit",
    "card_subcategory": "Standard",
    "amount": 200,
    "decimal_amount": 2.0,
    "successful": true,
    "message": "Approved",
    "reference": "first_preauth_transaction",
    "currency": "AUD",
    "transaction_id": "1-P-VBF4KCE9",
    "settlement_date": null,
    "transaction_date": "2020-04-26T11:13:49+10:00",
    "response_code": "00",
    "captured": false,
    "captured_amount": 0,
    "rrn": "042321000062",
    "cvv_match": "U",
    "metadata": {
      "sca_exemption": "",
      "card_sequence_number": "",
      "authorization_tracking_id": "HNR0003960518",
      "original_transaction_reference": "",
      "original_amount": "100"
    },
    "addendum_data": {}
  },
  "errors": [],
  "test": false
}
```

You will notice that in the response, the authorization is being kept the same.

### Pre-authorization Expiry Extension

To extend the expiry date while keeping the amount the same, you should use `extend: true`. 

```json Preauthorization Extension
/* 
 * Request: PUT /v1.0/purchases/1-P-VBF4KCE9
 */
{ 
  "extend": true
}
```

This will allow the pre-authorization to be extended by 7 days from the day this transaction is sent.

> ❗️ "Amount" and "Extend" cannot be sent at the same time
> 
> When "amount" is provided in the payload, the expiry date of the pre-authorization will be extended, so you should not send "extend" if you are already doing a top up.

### Pre-authorization Completion

Once the payment is ready to settle, you should send pre-authorization completion to settle the payment. This has to be done before the pre-authorization expires. See more details in [Capture an authorization](ref:capture-an-authorization) .

```json Pre-authorzation Completion (Capture Payment)
/* 
 * Request: POST /v1.0/purchases/1-P-VBF4KCE9/capture
 */
{ 
  "amount": 200
}
```

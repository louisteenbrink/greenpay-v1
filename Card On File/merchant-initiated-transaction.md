---
title: "Merchant Initiated Transaction"
slug: "merchant-initiated-transaction"
excerpt: ""
hidden: false
createdAt: "Tue May 25 2021 00:53:14 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Jul 16 2024 02:01:05 GMT+0000 (Coordinated Universal Time)"
---
A merchant initiated transaction is a payment that is agreed with payer's consent, and is initiated by the merchant collecting the payment.

In order to apply for a merchant initiated transaction, the merchant needs to specify why this transaction is initiated, as well as the `authorization_tracking_id` of the original transaction, and `stored_credential_indicator` to show if it's the first card on file transaction on the subsequent one.

You can see different reasons [here](https://docs.fatzebra.com/docs/recurring-and-other-transaction-types#merchant-initiated-transactions).

## A Merchant Initiated Transaction Example

In order to apply a merchant initiated transaction, the customer will need to put their card on file first.

This transaction can be a zero dollar authorization just to put card on file, or it could be the initial payment customer is required to pay. We will assume customer is just doing a zero dollar authorization. We can create the transaction via [Create a purchase](ref:create-a-purchase) .

Note that since we are putting card on file, we will need to specify `card_on_file` to true.

```json Customer Initiated Transaction
/* 
 * Request: POST /v1.0/purchases
 */
{
  "amount": 0,
  "currency": "AUD",
  "card_holder": "John Smith",
  "card_number": "411111xxxxxx1111",
  "card_expiry": "01/2025",
  "cvv": "123",
  "reference": "customer_initiated_transaction",
  "extra": {
    "card_on_file": true,
    "stored_credential_indicator": "I"
  }
}
```

In the response, we will get the `card_token` as well as the `authorization_tracking_id`. These values will need to be stored for the merchant initiated transaction later.

```json Customer Initiated Transaction Response
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
    "reference": "first_recurring_transaction",
    "currency": "AUD",
    "transaction_id": "1-P-VBF4KCE9",
    "settlement_date": "2020-04-23",
    "transaction_date": "2020-04-23T10:21:31+10:00",
    "response_code": "00",
    "captured": true,
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

To apply for a merchant initiated transaction, you need to apply the `card_token`, the `auth_reason` and `authorization_tracking_id` in the payload.

Note: Not all schemes requires `authorization_tracking_id`. If this value is not found in the response, then it indicates this scheme does not support it, and this can be ignored for subsequent transactions.

> ❗️ Failure to present the authorization_tracking_id may result in the recurring or installment transaction being declined, particularly wallet transactions.

```json
{
  "amount": 100,
  "currency": "AUD",
  "card_token": "lk78b0xadcdek2hffvkadif",
  "reference": "merchant_initiated_transaction",
  "extra": {
    "auth_reason": "no_show",
    "authorization_tracking_id": "HNR0003960518",
    "stored_credential_indicator": "S"
  }
}
```

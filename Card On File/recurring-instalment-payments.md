---
title: "Recurring / Installment Payments"
slug: "recurring-instalment-payments"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon May 24 2021 06:56:24 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Jun 06 2023 01:06:59 GMT+0000 (Coordinated Universal Time)"
---
Merchants can make recurring and installment transactions. This is achieved by:

1. Set `ECM` value accordingly
2. Set `stored_credential_indicator` to indicate if it's the first or subsequent transaction.
3. Using the `card_token` from the initial transaction where the customer authorized the recurring or installment cycle, as well as specifying the `authorization_tracking_id` returned on the initial transaction in all subsequent recurring or installment transactions.
4. If the card is expired, you can set `omit_expiry` to true to allow payment to go through.

The definition of `ECM`, `card_on_file` and `omit_expiry` can be found [here](https://docs.fatzebra.com/docs/recurring-and-other-transaction-types).

## A Recurring Scenario Example

Below is a scenario example to illustrate how to use `card_token` and `authorization_tracking_id` for first and subsequent transactions:

### First Recurring Transaction

We can create the first recurring transaction via [**create a purchase**](https://docs.fatzebra.com/reference#purchases).

```json First Recurring Payment
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
  "reference": "first_recurring_transaction",
  "extra": {
    "ecm": 32,
    "stored_credential_indicator": "I"
  }
}
```

In the response, we will get the `card_token` as well as the `authorization_tracking_id`. These values will need to be stored for the subsequent transaction.

- `card_token`: this is a token for the card number used in the initial transaction and can be used in subsequent transactions so that the actual card number does not need to be entered
- `metadata.authorization_tracking_id`: this is an ID returned by the card schemes which must be presented on subsequent recurring or installment transactions.

```json First Recurring Payment Response
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

### Subsequent Transaction

The `authorization_tracking_id` should be supplied for every subsequent recurring transaction to increase approval rates.

> 📘 Some schemes do not return an `authorization_tracking_id` after a first recurring payment. If this is not present in the payload, it's safe to create recurring transactions without it.

```json Subsequent Recurring Transaction
/* 
 * Request: POST /v1.0/purchases
 */
{
  "amount": 100,
  "currency": "AUD",
  "card_token": "lk78b0xadcdek2hffvkadif",
  "reference": "second_recurring_transaction",
  "extra": {
    "ecm": 32,
    "authorization_tracking_id": "HNR0003960518",
    "stored_credential_indicator": "S"
  }
}
```

### Transact With Expired Tokenized Credit Card

If the tokenized credit card is expired, it will likely be rejected. You can set `omit_expiry:true` to attempt to increase approval rates. 

> 📘 Automatic Card Updates
> 
> Contact your account manager to enquire about Automatic Card Update capabilities (including automatic expiry date updates) to help uplift approval rates for expired cards.

```json Transact With Expired Tokenized Credit Card
/* 
 * Request: POST /v1.0/purchases
 */
{
  "amount": 100,
  "currency": "AUD",
  "card_token": "lk78b0xadcdek2hffvkadif",
  "reference": "second_recurring_transaction",
  "extra": {
    "ecm": 32,
    "omit_expiry": true,
    "authorization_tracking_id": "HNR0003960518",
    "stored_credential_indicator": "S"
  }
}
```

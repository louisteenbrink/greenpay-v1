---
title: "Tokenized Credit Cards"
slug: "tokenized-credit-cards"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Sep 10 2018 21:15:57 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue May 25 2021 01:37:18 GMT+0000 (Coordinated Universal Time)"
---
Tokenized Credit Cards is a method of storing your customers credit card details securely 'on file' in the Fat Zebra secure cardholder data environment.

Commonly this is used for recurring payments, however this can also be used to provide a streamlined customer experience, allowing them to save their payment details for future orders.

When a Credit Card is tokenized, the Gateway will return a token that is unique to your merchant account. To charge the Tokenized Credit Card, you should provide the card token in lieu of the other card details, and this is used when authorizing the payment.

Every Credit Card transaction within the Gateway results in the tokenization of a Credit Card, and the token is returned with every purchase request. This allows merchants to store the token after an order has been placed, or after an order has been processed in an out of band payment method (such as though Direct Post or a Hosted Payment Page).

Merchants can assign (if desired) an alias to the Tokenized Credit Card, which allows for a custom value to be associated with the Token for use when processing the payment. This allows for a merchant customer reference (such as a customer ID or number) to be used instead of the system generated token value.

Should a Tokenized Credit Card expire, you can update the record on file with a new expiry date when it is provided by the customer.

You can find more details on how to tokenize a credit card [here](https://docs.fatzebra.com/reference#tokenize-a-card).

## Transact With Tokenized Card Example

In order to transact with a tokenized credit card, you will need to tokenize the credit card first.

```json Tokenize Credit Card
/*
 * Request: POST /v1.0/credit_cards
 */
{
  "card_number": "5123456789012346",
  "card_holder": "Bob Smith",
  "card_expiry": "05/2030",
  "cvv": "987"
}
```

You will get a tokenized credit card in the response from `token`. In future transactions, you can just transact with this token instead of using the credit card.

```json Tokenize Credit Card Response
/*
 * Response
 */
{
  "successful": true,
  "response": {
    "token": "fke8jmra",
    "card_holder": "Bob Smith",
    "card_number": "512345XXXXXX2346",
    "card_expiry": "2030-05-31",
    "card_type": "MasterCard",
    "card_category": "Credit",
    "card_subcategory": "Standard",
    "card_issuer": "Banco Del Pichincha, C.A.",
    "card_country": "Ecuador",
    "authorized": true,
    "transaction_count": 0,
    "alias": null
  },
  "errors": [],
  "test": true
}
```

With your tokenized credit card, you can now transact with the card.

```json Transact With Tokenized Credit Card
/* 
 * Request: /v1.0/purchases
 */
{
  "amount": 100,
  "currency": "AUD",
  "card_token": "fke8jmra",
  "reference": "transact_with_token"
}
```

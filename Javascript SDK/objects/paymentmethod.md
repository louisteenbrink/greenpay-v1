---
title: "PaymentMethod"
slug: "paymentmethod"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jul 23 2020 12:01:00 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Sep 30 2020 06:28:39 GMT+0000 (Coordinated Universal Time)"
---
The **PaymentMethod** object contains card details and is used in the following methods:

- [renderPaymentsPage](doc:renderpaymentspage) 
- [verifyCard](doc:verifycard) 

It supports both new cards (where the raw card number and details are provided) or existing cards (where a Fat Zebra card token is provided).

## Pay with a new card

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`type`",
    "0-1": "string",
    "0-2": "Specify the following value: `card`",
    "1-0": "`data.number`",
    "1-1": "string",
    "1-2": "Card number",
    "2-0": "`data.holder`",
    "2-1": "string",
    "2-2": "Card holder name",
    "3-0": "`data.expiryMonth`",
    "3-1": "string",
    "3-2": "Expiry month  \n2 characters long  \nPadded with a leading zero, e.g. `01` for January",
    "4-0": "`data.expiryYear`",
    "4-1": "string",
    "4-2": "Expiry year  \n4 characters long",
    "5-0": "`cvv`",
    "5-1": "string",
    "5-2": "CVV or CVC value on the card  \n3 or 4 digits depending on the card scheme"
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


```json Example:  card
{
  type: "card",
  data: {
    number: "4005550000000001",
    holder: "John Doe",
    expiryMonth: "03",
    expiryYear: "2022",
    cvv: "123"
  }
}
```

## Pay with an existing card (card on file)

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`type`",
    "0-1": "string",
    "0-2": "Specify the following value: `card_on_file`",
    "1-0": "`data.token`",
    "1-1": "string",
    "1-2": "Card token.  \nSee [here](https://docs.fatzebra.com/reference#tokenize-a-card) for more details on how to tokenize a card."
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


```json Example: card on file
{
  type: "card_on_file",
  data: {
    token: "fke8jmra"
  }
}
```

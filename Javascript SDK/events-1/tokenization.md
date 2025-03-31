---
title: "Tokenization"
slug: "tokenization"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Jul 24 2020 02:03:26 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Sep 30 2020 05:14:02 GMT+0000 (Coordinated Universal Time)"
---
All cards entered into the Hosted Payment Page are tokenized first before 3DS verification and payment transaction.

| Event                     | Description                                  | Applicable Methods                           |
| :------------------------ | :------------------------------------------- | :------------------------------------------- |
| `fz.tokenization.success` | Emitted when card is successfully tokenized. | [renderPaymentsPage](doc:renderpaymentspage) |
| `fz.tokenization.error`   | Emitted when card tokenization fails.        | [renderPaymentsPage](doc:renderpaymentspage) |

## fz.tokenization.success Data Payload

| Attribute | Type   | Description |
| :-------- | :----- | :---------- |
| `token`   | string | Card token  |

```json fz.tokenization.success data payload
{
  message: "xxx",
  data: {
    token: "xxx",
  }
}
```

## fz.tokenization.error Data Payload

| Attribute | Type | Description |
| :-------- | :--- | :---------- |
| N/A       | N/A  | N/A         |

```json fz.tokenization.error data payload
{
  errors: ["xxx"],
  data: null
}
```

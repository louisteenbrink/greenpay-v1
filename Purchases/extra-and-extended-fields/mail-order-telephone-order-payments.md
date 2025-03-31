---
title: "Mail Order / Telephone Order Payments"
slug: "mail-order-telephone-order-payments"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon May 24 2021 05:35:39 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Feb 24 2022 00:48:51 GMT+0000 (Coordinated Universal Time)"
---
Mail Order / Telephone Order Payments should be identified using the `ecm` indicator. The field is two digits (mn) with the possible values being:

| First Digit (m)     | Second Digit (n) |
| :------------------ | :--------------- |
| Telephone Order - 1 | Single - 1       |
|                     | Recurring - 2    |
|                     | Instalment - 3   |
| Mail Order - 2      | Single - 1       |
|                     | Recurring - 2    |
|                     | Instalment - 3   |
| Internet Order - 3  | Single - 1       |
|                     | Recurring - 2    |
|                     | Instalment - 3   |

```json Telephone Order
{
  "extra": {
    "ecm": 11
  }
}
```

```json
{
  "extra": {
    "ecm": 21
  }
}
```

---
title: "Remittance Merchants"
slug: "remittance-overview"
excerpt: ""
hidden: false
metadata: 
  title: "Remittance Overview"
  image: []
  robots: "index"
createdAt: "Wed Feb 22 2023 01:37:10 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed May 24 2023 09:26:00 GMT+0000 (Coordinated Universal Time)"
---
## Remittance Parameters

Money remittance merchants (Merchant Category Code `4829` or `6540`) are required to provide additional data in the request payload under `extra` for these transactions:

- Purchase
- Auth
- Refund (standalone)

```json
{
  "extra": {
    "remittance": {
      "bai": "p2p",
      "sender": {
        "first_name": "Rachel",
        "last_name": "Remitter",
        "address": "1 Remittance Road",
        "city": "Sydney",
        "country": "AUS"
      },
      "recipient": {
        "first_name": "Richard",
        "last_name": "Remittee",
        "country": "NZL",
        "account_type": "06",
        "account_number": "6666667777777333"
      }
    }
  }
}
```

## Business Application Identifier (BAI)

### Visa

| Sender | Receiver           | Merchant supports Visa-OCT? | BAI        |
| :----- | :----------------- | :-------------------------- | :--------- |
| Person | Person (different) | YES                         | `p2p`      |
| Person | Person (different) | NO                          | `p2p_card` |
| Person | Person(same)       |                             | `self`     |

### Mastercard

| Sender   | Receiver             | Receiver Account Type   | BAI               |
| :------- | :------------------- | :---------------------- | :---------------- |
| Person   | Person (different)   | NOT CARD                | `p2p`             |
| Person   | Person (different)   | IS CARD                 | `p2p_card`        |
| Person   | Person (same)        | NOT CARD                | `self`            |
| Person   | Person (same)        | IS CARD (debit/prepaid) | `self_debit_card` |
| Business | Business (same)      |                         | `b2b`             |
| Business | Business (different) |                         | `b2b_card`        |

## Sender Data

| Field        | Type   | Length                 |
| :----------- | :----- | :--------------------- |
| `first_name` | String | Max: 35                |
| `last_name`  | String | Max: 35                |
| `address`    | String | Max: 35                |
| `city`       | String | Max: 25                |
| `country`    | String | 3 (ISO 3166-1 alpha-3) |

## Recipient Data

### Account Type

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Length",
    "0-0": "`first_name`",
    "0-1": "String",
    "0-2": "Max: 35",
    "1-0": "`last_name`",
    "1-1": "String",
    "1-2": "Max: 35",
    "2-0": "`country`",
    "2-1": "String",
    "2-2": "3 (ISO 3166-1 alpha-3)",
    "3-0": "`account_type`",
    "3-1": "String",
    "3-2": "2  \n`00` – Other  \n`01` – RTN + Bank Account  \n`02` – IBAN  \n`03` – Card Account  \n`04` – Email  \n`05` – Phone Number  \n`06` – Bank Account Number (BAN) + Bank Identification Code (BIC)  \n`07` – Wallet ID  \n`08` – Social Network ID",
    "4-0": "`account_number`",
    "4-1": "String",
    "4-2": "Max: 50"
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

---
title: "Tokenized Cards"
slug: "tokenized-cards"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jan 18 2018 06:12:38 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 20:39:08 GMT+0000 (Coordinated Universal Time)"
---
Fat Zebra is able to accept card details and process payments on behalf of merchants by interfacing with relevant switches. Tokenized cards can be used to create purchases.

## Tokenized Card

## Response format

| Field               | Type                     | Description                                |
| :------------------ | :----------------------- | :----------------------------------------- |
| `token`             | String                   | Generated token for card                   |
| `card_holder`       | String                   | Card holder name                           |
| `card_number`       | String                   | Obfuscated card number                     |
| `card_expiry`       | String / Date YYYY-MM-DD | Card expiry date                           |
| `card_type`         | String                   | Card schema                                |
| `card_category`     | String                   | Card type - Credit/Debit                   |
| `card_ subcategory` | String                   | Card category                              |
| `card_issuer`       | String                   | Card issuer                                |
| `card_country`      | String                   | Card country                               |
| `authorized`        | Boolean                  |                                            |
| `transaction_count` | Integer                  | Number of transactions made with this card |
| `alias`             | String                   | Card alias                                 |

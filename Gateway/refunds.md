---
title: "Refunds"
slug: "refunds"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jan 18 2018 06:43:41 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Nov 09 2021 00:24:53 GMT+0000 (Coordinated Universal Time)"
---
Fat Zebra provides a facility to issue refunds.

## Refund

## Response format

| Field                  | Type                     | Description                                                                                                                                                                                                                                               |
| :--------------------- | :----------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `authorization`        | String                   | Authorization number                                                                                                                                                                                                                                      |
| `id`                   | String                   | ID of the refund                                                                                                                                                                                                                                          |
| `amount`               | Integer                  | Amount of the refund in the smallest currency unit (e.g., 100 to refund $1.00, or 100 to refund ¥100, a zero decimal currency)                                                                                                                            |
| `refunded`             | String                   | Status of the refund                                                                                                                                                                                                                                      |
| `message`              | String                   | Message giving context to the outcome of the request                                                                                                                                                                                                      |
| `card_holder`          | String                   | Card holder name                                                                                                                                                                                                                                          |
| `card_number`          | String                   | Obfuscated card number                                                                                                                                                                                                                                    |
| `card_expiry`          | String / Date YYYY-MM-DD | Card expiry date                                                                                                                                                                                                                                          |
| `card_type`            | String                   | Branding of the card                                                                                                                                                                                                                                      |
| `transaction_id`       | String                   | Identifier for the transaction used to perform the refund                                                                                                                                                                                                 |
| `reference`            | String                   | Identifier for the refund                                                                                                                                                                                                                                 |
| `currency`             | String / ISO 3           | Currency of the purchase                                                                                                                                                                                                                                  |
| `successful`           | Boolean                  | Whether the operation was successful or not                                                                                                                                                                                                               |
| `transaction_date`     | String                   | Date the transaction was created                                                                                                                                                                                                                          |
| `response_code`        | String                   | Response code received from the switch                                                                                                                                                                                                                    |
| `settlement_date`      | String / Date YYYY-MM-DD | Settlement date                                                                                                                                                                                                                                           |
| `metadata`             | Object                   | Metadata for the refund                                                                                                                                                                                                                                   |
| `standalone`           | Boolean                  | Whether the refund was issued without reference to a previous purchase                                                                                                                                                                                    |
| `rrn`                  | String                   | Receipt number of the purchase                                                                                                                                                                                                                            |
| `merchant_advice_code` | String                   | Advice code for how merchants should retry failed transactions. Only present when a transaction is declined. Details on the possible codes are documented [Merchant Advice Codes (Retries)](https://docs.fatzebra.com/docs/merchant-advice-codes-retries) |

---
title: "Chargebacks"
slug: "chargebacks-2"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jul 18 2018 01:01:31 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Sep 07 2018 06:05:48 GMT+0000 (Coordinated Universal Time)"
---
A chargeback process is initiated when a cardholder disputes a card transaction and asks for the charge to be reversed.

## Chargeback

## Response format

| Field                       | Type                     | Description                           |
| :-------------------------- | :----------------------- | :------------------------------------ |
| `id`                        | String                   | ID of the chargeback                  |
| `acquirer_merchant_id`      | String                   | Acquirer ID of the merchant [?]       |
| `reference`                 | String                   |                                       |
| `chargeback_control_number` | String                   |                                       |
| `amount`                    | Integer                  | Amount of the chargeback in cents [?] |
| `reason_code`               |                          |                                       |
| `reason_description`        | String                   |                                       |
| `status`                    | String                   |                                       |
| `merchant_status`           | String                   |                                       |
| `due_date`                  | String / Date YYYY-MM-DD |                                       |
| `metadata`                  | Object                   | Metadata                              |
| `notifications`             | Array                    | Chargeback notifications              |

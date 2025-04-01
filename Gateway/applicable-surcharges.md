---
title: Applicable Surcharges
slug: applicable-surcharges
excerpt: ''
metadata:
  image: []
  robots: index
createdAt: Tue Dec 19 2017 22:26:06 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Sep 07 2018 05:52:30 GMT+0000 (Coordinated Universal Time)
---

# Response object

| Scheme         | Card number         | Purchase response code |
| -------------- | ------------------- | ---------------------- |
| Mastercard     | 5123 4567 8901 2346 | 00 Approved            |
|                | 5313 5810 0012 3430 | 05 Declined            |
| VISA           | 4005 5500 0000 0001 | 00 Approved            |
|                | 4557 0123 4567 8902 | 05 Declined            |
| AMEX           | 3456 789012 34564   | 00 Approved            |
|                | 3714 496353 98431   | 05 Declined            |
| JCB            | 3530 1113 3330 0000 | 00 Approved            |
|                | 3566 0020 2036 0505 | 05 Declined            |
| China UnionPay | 6250946000000016    | 00 Approved            |
|                | 6250947000000014    | 05 Declined            |

| Field                          | Type    | Description                                                       |
| ------------------------------ | ------- | ----------------------------------------------------------------- |
| `card_description`             | string  | Description of the card details provided.                         |
| `surcharge_amount`             | integer | Amount of the applicable surcharge in the smallest currency unit. |
| `surcharge_amount_description` | string  | Description of the surcharge amount.                              |
| `total_amount`                 | integer | Total amount to be charged including surcharging.                 |

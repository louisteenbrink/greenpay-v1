---
title: "Settlement"
slug: "settlement"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Mar 28 2018 06:10:34 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Sep 07 2018 06:28:17 GMT+0000 (Coordinated Universal Time)"
---
In order to reconcile and report on your credit card transactions an settlement endpoint is available to retrieve summary details.

This endpoint details the totals broken down by card type within the specified settlement period.

Note: If the settlement date specified is still current (i.e. the date has not rolled over) the totals will not be complete and may be different for new requests.

# Fields

The response to the endpoint will return the following data structure:

| Name                    | Type              | Description                                                                                                                    |
| :---------------------- | :---------------- | :----------------------------------------------------------------------------------------------------------------------------- |
| date                    | date (yyyy-mm-dd) | The settlement period date                                                                                                     |
| currency                | string            | The ISO 4217 3-letter currency code for the settlement period                                                                  |
| totals                  | Array<Mixed>      | Documented below, an array of settlement total objects                                                                         |
| totals.scheme           | string            | The card scheme for the totals                                                                                                 |
| totals.purchases.amount | integer           | The total amount for the settlement period of all successful purchases, in the smallest unit (e.g. cents, yen etc)             |
| totals.purchases.count  | integer           | The total number of successful purchases for the settlement period.                                                            |
| totals.refunds.amount   | integer           | The total amount for the settlement period of all successful refunds, in the smallest unit (e.g. cents, yen etc)               |
| totals.refunds.amount   | integer           | The total number of successful refunds for the settlement period.                                                              |
| totals.total.amount     | integer           | The total amount for the settlement period of all successful purchases and refunds, in the smallest unit (e.g. cents, yen etc) |
| totals.total.count      | integer           | The total number of successful purchases and refunds for the settlement period.                                                |

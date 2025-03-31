---
title: "Direct Debits"
slug: "direct-debits"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Sun May 13 2018 23:03:11 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Sep 10 2020 03:00:46 GMT+0000 (Coordinated Universal Time)"
---
Direct Debits are used to take funds from a customer's account (the source account) and deposit them into your account (the destination account).

## Direct Debit

## Response object

| Field            | Type                     | Description                                                         |
| :--------------- | :----------------------- | :------------------------------------------------------------------ |
| `id`             | String                   | ID of the direct debit                                              |
| `amount`         | Float                    | Amount of the direct debit in dollars. Minimum 0.01, positive only. |
| `bsb`            | String                   | The source account BSB number                                       |
| `account_number` | String                   | The source account number                                           |
| `account_name`   | String                   | The source account name                                             |
| `description`    | String                   | Description of the direct debit                                     |
| `reference`      | String                   | Unique reference for the direct debit                               |
| `date`           | String / Date YYYY-MM-DD | The direct debit creation date                                      |
| `process_date`   | String / Date YYYY-MM-DD | The direct debit processing date                                    |
| `status`         | String                   | Status of the direct debit                                          |
| `result`         | String                   | Result of the direct debit                                          |
| `metadata`       | Object                   | Metadata for the direct debit                                       |

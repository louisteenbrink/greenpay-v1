---
title: "Direct Credits"
slug: "direct-credits"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Nov 28 2017 05:57:49 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Sep 10 2020 03:00:58 GMT+0000 (Coordinated Universal Time)"
---
Direct Credits are used to send funds from your account (the source account) to a third party (the destination account).

## Direct Credit

## Response format

| Field            | Type                     | Description                                                          |
| :--------------- | :----------------------- | :------------------------------------------------------------------- |
| `id`             | String                   | ID of the direct credit                                              |
| `amount`         | Float                    | Amount of the direct credit in dollars. Minimum 0.01, positive only. |
| `bsb`            | String                   | The destination account BSB number                                   |
| `account_number` | String                   | The destination account number                                       |
| `account_name`   | String                   | The destination account name                                         |
| `description`    | String                   | Description of the direct credit                                     |
| `reference`      | String                   | Unique reference for the direct credit                               |
| `date`           | String / Date YYYY-MM-DD | The direct credit creation date                                      |
| `process_date`   | String / Date YYYY-MM-DD | The direct credit processing date                                    |
| `status`         | String                   | Status of the direct credit                                          |
| `result`         | String                   | Result of the direct credit                                          |
| `metadata`       | String                   | Metadata for the direct credit                                       |

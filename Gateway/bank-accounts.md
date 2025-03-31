---
title: "Bank Accounts"
slug: "bank-accounts"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Dec 04 2017 02:30:51 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jun 05 2019 00:36:51 GMT+0000 (Coordinated Universal Time)"
---
Bank accounts can be stored in the gateway for use with customers and direct entries. Australian and NZ bank accounts can be stored. Please note, bank accounts can not be edited once created.

| Field            | Type    | Description                                                                                                                 |
| :--------------- | :------ | :-------------------------------------------------------------------------------------------------------------------------- |
| `account_name`   | string  | Account name to be used for direct entry.                                                                                   |
| `account_number` | numeric | Bank account number. 6-9 digits for an Australian bank account, or 8-10 digits for a New Zealand bank account               |
| `bsb`            | numeric | BSB number - this will be in the format of ###-### for an Australian bank account, or ###### for a New Zealand bank account |
| `account_type`   | string  | "AU" or "NZ" for Australian or New Zealand bank account.  Defaults to "AU" if not provided.                                 |

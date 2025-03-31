---
title: "Card On File"
slug: "recurring-and-other-transaction-types"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Nov 08 2018 05:08:25 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 14 2022 23:38:13 GMT+0000 (Coordinated Universal Time)"
---
Card on file transactions include:

1. Tokenizing credit card for use later. (See example [here](https://docs.fatzebra.com/docs/tokenized-credit-cards))
2. Recurring and instalment payment. (See example [here](https://docs.fatzebra.com/docs/recurring-instalment-payments))
3. Merchant initiated transactions. (See example [here](https://docs.fatzebra.com/docs/merchant-initiated-transaction))

There are several fields related to these transactions.

## ECM

The ECM (eCommerce Indicator) describes the card transaction type. The field is two digits (mn) with the possible values being:

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

Below is an example on how to set the ECM value.

```json Example: Recurring Payment
{
  "extra": {
    "ecm": 32
  }
}
```

## Stored Credential Indicator

The stored credential indicator is used to indicate if this is the initial recurring / instalment transaction, or the subsequent transaction.

| Description            | Value |
| :--------------------- | :---- |
| Initial Transaction    | I     |
| Subsequent Transaction | S     |

Below is an example on how to use stored credential indicator

```json
{
  "extra": {
    "stored_credential_indicator": "I"
  }
}
```

## Omit Expiry

The omit expiry field set to true can also be sent through for recurring transactions against expired cards. This will allow the transaction to be sent to the banking network without the expiry date field. Typically, this field increases approval rates for recurring transactions against expired cards.

```json Example: Omit Expiry Flag
{
  "extra": {
    "omit_expiry": true,
    "ecm": 32
  }
}
```

## Merchant Initiated Transactions

A merchant initiated transaction is a payment that is agreed with a payer's consent, and is initiated by the merchant collecting the payment.

In order to apply for a merchant initiated transaction, the merchant need to specify why this transaction is initiated using the `auth_reason` field. Below are available reasons.

| Authorization Reason                    | Value            |
| :-------------------------------------- | :--------------- |
| Resubmission Payment                    | resubmission     |
| Delayed Charges Payment                 | delayed_charges  |
| Re-authorization Payment                | reauthorization  |
| No Show                                 | no_show          |
| Account Topup                           | account_topup    |
| Unscheduled Payment                     | unscheduled      |
| Incremental                             | incremental      |
| Instalment                              | instalment       |
| Recurring Transaction - Subscriptions\* | subscription     |
| Partial Shipment                        | partial shipment |

[*] Subscriptions are a recurring payment of fixed value

```json Example: No Show
{
  "extra": {
    "auth_reason": "no_show"
  }
}
```

## Card On File

The card on file flag set to true indicates we are using a credit card that is stored in a vault, eg. card that is tokenized via Fat Zebra gateway. All recurring, instalment payment and merchant initiated transactions are card on file transactions.

Note that you don't need to apply this value for recurring, installment payment and merchant initiated transaction, as the system will apply it automatically.

```json Example: Card On File
{
  "extra": {
    "card_on_file": true
  }
}
```

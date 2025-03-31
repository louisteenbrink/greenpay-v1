---
title: "Recurring & Installment Transactions"
slug: "apple-pay-recurring-installment-transactions"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Oct 26 2020 23:22:59 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Dec 03 2020 05:41:35 GMT+0000 (Coordinated Universal Time)"
---
Merchants can make recurring and installment transactions using Apple Pay cards. This is achieved by using the `card_token` from the initial Apple Pay transaction where the customer authorized the recurring or installment cycle, as well as specifying the `authorization_tracking_id` returned on the initial Apple Pay transaction in all subsequent recurring or installment transactions.

> 📘 Apple have published a set of [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/apple-pay/overview/payment-types/) that detail how Apple Pay transactions should be presented to customers. These guidelines include [recurring and installment payments](https://developer.apple.com/design/human-interface-guidelines/apple-pay/overview/payment-types/) and should be followed by merchants.

This process would look like:

## 1. Process an initial Apple Pay transaction

Merchants must first have the customer authorize an initial Apple Pay transaction. This can be done by following the steps in Fat Zebra's [Apple Pay documentation](doc:apple-pay).

## 2. Store the card_token & authorization_tracking_id for future use

The last step of processing the initial Apple Pay transaction is to make an API call to Fat Zebra to [**create a purchase using a wallet**](https://docs.fatzebra.com/v1.0/reference#create-a-purchase-with-wallet).

In the response of this API call you will receive two values which should be stored for later use:

- `card_token`: this is a token for the card number used in the initial Apple Pay transaction and can be used in subsequent transactions so that the actual card number does not need to be entered
- `metadata.authorization_tracking_id`: this is an ID returned by the card schemes which must be presented on subsequent recurring or installment transactions.

> ❗️ Failure to present the `authorization_tracking_id` may result in the recurring or installment transaction being declined

For reference, here's an example response from the API call used to create the initial Apple Pay transaction:

```json Response from create a purchase with a wallet API call
{
    "successful": true,
    "response": {
        "authorization": "123615",
        "id": "001-P-1DAY0JLF",
        "card_number": "442769XXXXXX5460",
        "card_holder": "ApplePay Card Holder",
        "card_expiry": "2023-12-31",
        "card_token": "zce2sfg5dgryi7a3x4fm",
        "card_type": "VISA",
        "card_category": "Debit",
        "card_subcategory": "Commercial",
        "amount": 1,
        "decimal_amount": 0.01,
        "successful": true,
        "message": "Approved",
        "reference": "9dffa525-d13a-4000-ac01-80a60a39435d",
        "currency": "AUD",
        "transaction_id": "001-P-1DAY0JLF",
        "settlement_date": "2020-10-27",
        "transaction_date": "2020-10-27T09:56:05+11:00",
        "response_code": "00",
        "captured": true,
        "captured_amount": 1,
        "rrn": "812423498214",
        "cvv_match": "U",
        "metadata": {
            "authorization_tracking_id": "VI457139255729342",
            "original_transaction_reference": ""
        },
        "addendum_data": {}
    },
    "errors": [],
    "test": false
}
```

Given the above response, you would store the following values in your system for future use:

- **card_token**: `zce2sfg5dgryi7a3x4fm`
- **authorization_tracking_id**: `VI457139255729342`

## 3. Process recurring or installment Apple Pay transactions

To create a recurring or installment transaction, call the [Create a purchase with a token](ref:create-a-purchase-with-a-token-1) API endpoint and specify a [recurring or installment value in extra.ecm](doc:recurring-and-other-transaction-types).

You will also need to specify the `authorization_tracking_id` value stored in step 2 above in the `extra.authorization_tracking_id` of your request:

```json Create a recurring Apple Pay purchase
curl https://gateway.pmnts-sandbox.io/v1.0/purchases -u TEST:TEST -d' 
    { 
        "amount": 1000, 
        "reference": "oiuwiouwxmnx23", 
        "customer_ip": "111.222.111.123", 
        "currency": "AUD", 
        "card_token": "zce2sfg5dgryi7a3x4fm",
        "extra": {
          "ecm": "32",
          "authorization_tracking_id": "VI457139255729342"
        }
    }'
```

In the above example an ecm of `32` - Internet/Recurring has been specified. This ecm value can be modified depending on your requirements, e.g. if you need a Telephone Order/Installment transaction you would specify an ecm of `13`. Refer to  [the following documentation](doc:recurring-and-other-transaction-types) for more information on ecm values.

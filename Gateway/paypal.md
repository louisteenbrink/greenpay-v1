---
title: "PayPal"
slug: "paypal"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Aug 26 2020 05:42:49 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Nov 15 2023 00:22:33 GMT+0000 (Coordinated Universal Time)"
---
> 📘 PayPal Integration
> 
> You can talk to our support team about integrating PayPal Checkout and activating your account. You can also refer to our integration guideline document for further information:
> 
> <https://docs.fatzebra.com/docs/paypal-overview>

In this document, PayPal endpoints are described including:

- Orders
- Authorizations
- Captures
- Refunds
- Billing Agreements

## Response objects

## Order

| Field                  | Type          | Description                                                          |
| :--------------------- | :------------ | :------------------------------------------------------------------- |
| `id`                   | String        | ID of the order                                                      |
| `amount`               | Integer       | Amount of the order in the smallest unit for the currency e.g. cents |
| `decimal_amount`       | Float         | Amount of the order as a decimal                                     |
| `captured_amount`      | Integer       | Captured amount if the order is captured                             |
| `authorized_amount`    | Integer       | Authorization amount if the order is authorized                      |
| `refunded_amount`      | Integer       | Refunded amount if the order is refunded                             |
| `message`              | String        | `Approved`, `Declined`                                               |
| `transaction_id`       | String        | ID of the refund                                                     |
| `currency`             | String        | Currency of the refund                                               |
| `successful`           | Boolean       | If the operation was successful or not                               |
| `transaction_date`     | String / Date | Date of the refund                                                   |
| `intent`               | String        | `Capture`, `Authorize`                                               |
| `paypal_reference`     | String        | Reference number assigned by PayPal                                  |
| `invoice_id`           | String        | Invoice ID of the order                                              |
| `billing_agreement_id` | String        | ID of the billing agreement if paid by a billing agreement           |
| `status`               | String        | `Created`, `Saved`, `Approved`, `Voided`, `Completed`                |
| `payment_source`       | String        | `BILLING_AGREEMENT`                                                  |
| `authorizations`       | Array         | List of authorizations                                               |
| `captures`             | Array         | List of captures                                                     |
| `refunds`              | Array         | List of refunds                                                      |
| `payer`                | Object        | Buyer's PayPal information                                           |
| `payee`                | Object        | Merchant's PayPal information                                        |

## Authorization

| Field                           | Type          | Description                                                                             |
| :------------------------------ | :------------ | :-------------------------------------------------------------------------------------- |
| `id`                            | String        | ID of the authorization                                                                 |
| `amount`                        | Integer       | Amount of the authorization in the smallest unit for the currency e.g. cents            |
| `decimal_amount`                | Float         | Amount of the authorization as a decimal                                                |
| `captured_amount`               | Integer       | Captured amount if the authorization is captured                                        |
| `refunded_amount`               | Integer       | Refunded amount if the capture is refunded                                              |
| `message`                       | String        | `Approved`, `Declined`                                                                  |
| `transaction_id`                | String        | ID of the refund                                                                        |
| `currency`                      | String        | Currency of the refund                                                                  |
| `successful`                    | Boolean       | If the operation was successful or not                                                  |
| `transaction_date`              | String / Date | Date of the refund                                                                      |
| `status`                        | String        | `Created`, `Requested`, `Voided`, `Captured`, `Partially Captured`, `Expired`, `Denied` |
| `balance_available_for_capture` | Integer       | Available balance for capture                                                           |
| `order`                         | String        | ID of the parent order                                                                  |
| `reference`                     | String        | The order reference                                                                     |

## Capture

| Field                           | Type          | Description                                                            |
| :------------------------------ | :------------ | :--------------------------------------------------------------------- |
| `id`                            | String        | ID of the refund                                                       |
| `amount`                        | Integer       | Amount of the refund in the smallest unit for the currency e.g. cents  |
| `decimal_amount`                | Float         | Amount of the refund as a decimal                                      |
| `captured_amount`               | Integer       | Captured amount                                                        |
| `message`                       | String        | `Approved`, `Declined`                                                 |
| `transaction_id`                | String        | ID of the refund                                                       |
| `currency`                      | String        | Currency of the refund                                                 |
| `successful`                    | Boolean       | If the operation was successful or not                                 |
| `transaction_date`              | String / Date | Date of the refund                                                     |
| `status`                        | String        | `Completed`, `Requested`, `Declined`, `Refunded`, \`Partially Refunded |
| `note_to_payer`                 | String        | Note to the buyer                                                      |
| `invoice_id`                    | String        | Invoice ID of the refund                                               |
| `paypal_fee`                    | Integer       | PayPal fee                                                             |
| `seller_receivable_net_amount`  | Integer       | Seller receivable net amount                                           |
| `balance_available_for_refund`  | Integer       | Available balance for refund                                           |
| `balance_available_for_capture` | Integer       | Available balance for capture                                          |
| `authorization`                 | String        | ID of the parent authorization                                         |
| `order`                         | String        | ID of the parent order                                                 |
| `refunded_amount`               | Integer       | Refunded amount                                                        |
| `is_final_capture`              | Boolean       | If this is the final capture of the order                              |
| `captured`                      | Boolean       | If it is captured, refunded or partially refunded                      |
| `reference`                     | String        | The order reference                                                    |

## Refund

| Field                          | Type          | Description                                                           |
| :----------------------------- | :------------ | :-------------------------------------------------------------------- |
| `id`                           | String        | ID of the refund                                                      |
| `amount`                       | Integer       | Amount of the refund in the smallest unit for the currency e.g. cents |
| `decimal_amount`               | Float         | Amount of the refund as a decimal                                     |
| `refunded`                     | String        | `Approved`, `Declined`                                                |
| `message`                      | String        | `Approved`, `Declined`                                                |
| `transaction_id`               | String        | ID of the refund                                                      |
| `currency`                     | String        | Currency of the refund                                                |
| `successful`                   | Boolean       | If the operation was successful or not                                |
| `transaction_date`             | String / Date | Date of the refund                                                    |
| `status`                       | String        | `Completed`, `Requested`                                              |
| `note_to_payer`                | String        | Note to the buyer                                                     |
| `invoice_id`                   | String        | Invoice ID of the refund                                              |
| `paypal_fee`                   | Integer       | PayPal fee                                                            |
| `seller_payable_net_amount`    | Integer       | Seller payable net amount                                             |
| `balance_available_for_refund` | Float         | Available balance for refund                                          |
| `capture`                      | String        | ID of the parent capture                                              |
| `order`                        | String        | ID of the parent order                                                |

## Billing Agreement

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`id`",
    "0-1": "String",
    "0-2": "ID of the billing agreement",
    "1-0": "`name`",
    "1-1": "String",
    "1-2": "Name of the billing agreement assigned by merchant",
    "2-0": "`description`",
    "2-1": "String",
    "2-2": "Description of the billing agreement assigned by merchant",
    "3-0": "`state`",
    "3-1": "String",
    "3-2": "State of the billing agreement: `Active`, `Inactive`",
    "4-0": "`payer`",
    "4-1": "Object",
    "4-2": "Buyer's information including: `email`, `first_name`, `last_name`",
    "5-0": "`shipping_address`",
    "5-1": "Object",
    "5-2": "Buyer's shipping address",
    "6-0": "`merchant_custom_data`",
    "6-1": "String",
    "6-2": "Merchant generated data  \nRefer to [PayPalPaymentObject](doc:paypal-payment-object)",
    "7-0": "`created_at`",
    "7-1": "String / Date",
    "7-2": "Creation date of the billing agreement"
  },
  "cols": 3,
  "rows": 8,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

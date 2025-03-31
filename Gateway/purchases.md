---
title: "Purchases"
slug: "purchases"
excerpt: ""
hidden: false
createdAt: "Fri Oct 13 2017 01:50:41 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Sep 18 2024 06:08:30 GMT+0000 (Coordinated Universal Time)"
---
A purchase represents a capture, authorization or void against a payment method.

## Purchase

## Response format

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`authorization`",
    "0-1": "String",
    "0-2": "Authorization number",
    "1-0": "`id`",
    "1-1": "String",
    "1-2": "Id of the purchase",
    "2-0": "`card_number`",
    "2-1": "String",
    "2-2": "The obfuscated card number",
    "3-0": "`card_holder`",
    "3-1": "String",
    "3-2": "The name of the card holder",
    "4-0": "`card_expiry`",
    "4-1": "String / Date YYYY-MM-DD",
    "4-2": "The expiry date of the card",
    "5-0": "`card_token`",
    "5-1": "String",
    "5-2": "A token representing the saved credit card",
    "6-0": "`card_type`",
    "6-1": "String",
    "6-2": "Scheme of the card",
    "7-0": "`card_category`",
    "7-1": "String",
    "7-2": "Type of the card: credit or debit",
    "8-0": "`card_subcategory`",
    "8-1": "String",
    "8-2": "The subcategory of the card",
    "9-0": "`amount`",
    "9-1": "Integer",
    "9-2": "Amount of the purchase in the smallest unit for the currency e.g. cents",
    "10-0": "`decimal_amount`",
    "10-1": "Float",
    "10-2": "Amount of the purchase as a decimal",
    "11-0": "`successful`",
    "11-1": "Boolean",
    "11-2": "If the operation was successful or not",
    "12-0": "`message`",
    "12-1": "String",
    "12-2": "A message giving context to the outcome of the request",
    "13-0": "`reference`",
    "13-1": "String",
    "13-2": "A unique reference from the switch",
    "14-0": "`currency`",
    "14-1": "String / ISO 4217",
    "14-2": "The currency of the purchase",
    "15-0": "`transaction_id`",
    "15-1": "String",
    "15-2": "A unique reference for each action against a purchase",
    "16-0": "`settlement_date`",
    "16-1": "String / Date YYYY-MM-DD",
    "16-2": "The date of settlement",
    "17-0": "`transaction_date`",
    "17-1": "String / Date ISO 8601",
    "17-2": "The date the transaction was created",
    "18-0": "`response_code`",
    "18-1": "String",
    "18-2": "The response code received from the switch",
    "19-0": "`captured`",
    "19-1": "Boolean",
    "19-2": "Whether the purchase was partly or fully captured",
    "20-0": "`captured_amount`",
    "20-1": "Integer",
    "20-2": "Amount captured in the smallest unit for the currency e.g. cents",
    "21-0": "`rrn`",
    "21-1": "String",
    "21-2": "The receipt number of the purchase",
    "22-0": "`cvv_match`",
    "22-1": "String",
    "22-2": "Whether the CVV match status from the issuer. Possible values are:  \n  \n_ M - Matched  \n_ Y - Matched  \n_ N - Not Matched  \n_ P - Not Processed  \n_ S - Suspicious  \n_ U - Unknown (response from network unclear)  \n  \nMerchants should use this to determine whether they are comfortable processing risky transactions.",
    "23-0": "`avs_result_code`",
    "23-1": "Integer",
    "23-2": "Indicates the result of the AVS check if AVS fields were provided.  \n  \nRefer to the [documentation on AVS](https://docs.fatzebra.com/docs/avs) for more details.",
    "24-0": "`metadata`",
    "24-1": "Object",
    "24-2": "Metadata of the purchase",
    "25-0": "`addendum_data`",
    "25-1": "Object",
    "25-2": "Addendum data of the purchase. Described below.",
    "26-0": "`merchant_advice_code`",
    "26-1": "String",
    "26-2": "Advice code for how merchants should retry failed transactions. Only present when a transaction is declined. Details on the possible codes are documented [Merchant Advice Codes (Retries)](https://docs.fatzebra.com/docs/merchant-advice-codes-retries)"
  },
  "cols": 3,
  "rows": 27,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


## Metadata

Some switching paths and acquirers will return additional data that can be found in the `metadata` field of a purchase response. This includes:

[block:parameters]
{
  "data": {
    "h-0": "Metadata Field",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`authorization_tracking_id`",
    "0-1": "String",
    "0-2": "An ID returned by the card scheme that is required to be presented on subsequent recurring or instalment transactions.  \n  \nNote that if this is not provided in any wallet transactions, the transaction will be rejected. For example [Apple Pay recurring or installment transactions](doc:recurring-installment-transactions).",
    "1-0": "`card_sequence_number`",
    "1-1": "String",
    "1-2": "A number indicating the sequence number of the card presented in the transaction",
    "2-0": "`least_cost_routed`",
    "2-1": "Boolean",
    "2-2": "Indicates if the transaction was least cost routed via the Debit network.  \n  \nOnly applicable to transactions using a dual branded card and routed via specific switches.  \n  \nPlease note that this field may return one of three values:  \n  \n- `true`: the transaction was least cost routed  \n- `false`: the switch used supports least cost routing, but the transaction was not eligible for least cost routing  \n- Key not present: the switch used does not support least cost routing"
  },
  "cols": 3,
  "rows": 3,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


## Addendum Data

For some switching paths and acquirers it may be possible to include addendum data which is passed onto the card issuer - this is primarily used for corporate purchasing cards, American Express cards etc.

To include this data with your transactions the field `addendum_data` should be added to the request payload with the appropriate data payload for the transaction type included - these different payload types are detailed below.

If addendum data was presented with the original transaction (such as for a pre-auth) the data will be merged, with the most recent data overwriting the older data.

### Corporate Purchasing Level 2 Data

Level 2 data for corporate purchase cards may be included which can detail the order reference, purchase order numbers, line item details etc.

| Field                             | Type                                                 | Description                                                                                                          |
| :-------------------------------- | :--------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------- |
| `cardmember_reference`            | String. Max length: 20. Alphanumeric and Spaces only | The card member's reference number, such as a store order number or customer PO Number                               |
| `description_1` - `description_4` | String. Max length: 40. Alphanumeric and Spaces only | The description for up to four line items. These should be descriptive and avoid generic terms such as 'Merchandise' |
| `quantity_1` - `quantity_4`       | Unsigned integer. Maximum value: 999.                | The quantity of items for the line items                                                                             |
| `total_1` - `total_4`             | Unsigned integer. Maximum value: 99999.              | The total for the line item as a whole number in the smallest unit (e.g. $155.60 will be 15560)                      |
| `shipping_postcode`               | String. Max length: 15. Alphanumeric and Spaces only | The post code for the shipping address                                                                               |

#### Example

```json
{
    "corp_l2": {
        "cardmember_reference": "ORD 123456 PO 08789",
        "description_1": "Box of paper",
        "quantity_1": 5,
        "total_1": 5000,
        "description_2": "Pencils",
        "quantity_2": 10,
        "total_2": 1000,         
        "description_3": "Pens",
        "quantity_3": 10,
        "total_3": 1500,
        "description_4": "White Out",
        "quantity_4": 1,
        "total_4": 500,
        "shipping_postcode": "EC1A 1AA"
      }
}
```

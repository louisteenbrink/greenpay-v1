---
title: "Chargebacks"
slug: "chargebacks"
excerpt: "You can subscribe to webhooks for chargeback notifications.  Each time our system receives a notification, a webhook will be sent containing information on the current and previous notifications related to the chargeback, newest notification first."
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Jul 17 2018 05:51:48 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Aug 10 2018 06:01:17 GMT+0000 (Coordinated Universal Time)"
---
## Sample Webhook Body

```json JSON
{
  "event": "chargeback:notification",
  "hook_id": "071-WH-JJKU6RSP",
  "id": "071-CB-MIP4SIHH",
  "payload": {
    "acquirer_merchant_id": "ABCDE12345",
    "id": "071-CB-MIP4SIHH",
    "reference": "C2BB3D60",
    "received_at": "2018-07-01T09:30:00.000Z",   
    "amount": 100,
    "currency": "AUD",    
    "reason_code": "865",
    "reason_description": "Service cancelled on 05/04/2018, credit not processed",
    "matched": true,
    "due_date": "2018-07-07",
    "metadata": {
      "transaction_date": "02-Feb-2018",
      "transaction_time": "14:13:00"
    },
    "purchase": {
      "id": "071-P-PAGTKK4W",
      "reference": "9wsa323e",
      "currency": "AUD",
      "amount": 100,
      "card_number": "411111XXXXXX1111",
      "card_holder": "Card Holder",
      "card_expiry": "2022-12-31",
      "card_token": "fke83tk1",
      "card_type": "VISA",
      "card_category": "Credit",
      "card_subcategory": "Credit",     
      "response_code": "00",
      "message": "Approved",
      "successful": true,
      "settlement_date": "2018-02-02",     
      "transaction_date": "2018-02-02T14:13:46+10:00",
      "rrn": "071PPAGTKK4W",
      "authorization": "693734",     
      "captured": true,
      "captured_amount": 100,
      "metadata": {},
      "addendum_data": {}
    },    
    "notifications": [
      {
        "id": "071-CN-6CNWTPAK",
        "received_at": "2018-07-15T00:00:00.000Z",
        "metadata": {
          "chargebackId": "749309",
          "chargebackDebitRef": "c2bb3d60-d04b-4c1c-8fd1-9d7a440a6d8b",
          "respondByDate": "22-Jul-18",
          "reasonForChargeback": "Service cancelled on 05/04/2018, credit not processed"
        }
      },
            {
        "id": "071-CN-79HDJKSL",
        "received_at": "2018-07-08T00:00:00.000Z",
        "metadata": {
          "chargebackId": "748480",
          "RetrievalRef": "c2bb3d60-d04b-4c1c-8fd1-9d7a440a6d8b",
          "respondByDate": "15-Jul-18",
          "reasonForChargeback": "Service cancelled on 05/04/2018, credit not processed"
        }
      },
      {
        "id": "071-CN-QS0V0OJS",
        "received_at": "2018-07-01T09:30:00.000Z",
        "metadata": {
          "chargebackId": "748392",
          "respondByDate": "7-Jul-18",
          "chargebackRef": "c2bb3d60-d04b-4c1c-8fd1-9d7a440a6d8b",
          "reasonForChargeback": "Service cancelled on 05/04/2018 ,credit not processed"
        }
      }
    ]    
  },
}
```

## Webhook Body Fields

| Field     | Type   | Description                                        |
| :-------- | :----- | :------------------------------------------------- |
| `event`   | string | Webhook event name, e.g. "chargeback:notification" |
| `hook_id` | string | Unique identifier for this webhook                 |
| `id`      | string | Unique identifier for this chargeback              |
| `payload` | hash   | Details of the chargeback event                    |

## Payload Fields

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`acquirer_merchant_id`",
    "0-1": "string",
    "0-2": "Acquirer's merchant ID",
    "1-0": "`id`",
    "1-1": "string",
    "1-2": "Unique ID for the chargeback",
    "2-0": "`reference`",
    "2-1": "string",
    "2-2": "Reference for the chargeback",
    "3-0": "`created_at`",
    "3-1": "string",
    "3-2": "Date and time when chargeback record was created",
    "4-0": "`amount`",
    "4-1": "integer",
    "4-2": "A positive integer representing the amount of the chargeback, in the smallest currency unit (e.g. 100 can mean $1.00 or ¥100 depending on the currency).",
    "5-0": "`reason_code`",
    "5-1": "string",
    "5-2": "Reason code for the chargeback (See <https://pmnts.readme.io/v1.0/docs/chargeback-reason-codes>)",
    "6-0": "`reason_description`",
    "6-1": "string",
    "6-2": "Description of the reason for the chargeback",
    "7-0": "`status`",
    "7-1": "string",
    "7-2": "Status of the chargeback, e.g. Matched, Unmatched",
    "8-0": "`merchant_status`",
    "8-1": "string",
    "8-2": "Merchant's status for the chargeback, e.g. New, In progress",
    "9-0": "`due_date`",
    "9-1": "string",
    "9-2": "Date when response must be completed by",
    "10-0": "`metadata`",
    "10-1": "hash",
    "10-2": "Additional info",
    "11-0": "`purchase`",
    "11-1": "hash",
    "11-2": "Details of the original purchase  \n  \nPurchase Hash | | |  \n------------ \\| ------------- \\| ------------  \n`id` | string | Unique ID for the notification  \n`reference` | string | Reference for the purchase  \n`currency` | string | Currency of the purchase  \n`amount` | integer | Amount of the purchase  \n`card_number` | string | Masked credit card number  \n`card_holder` | string | Credit card holder's name  \n`card_expiry` | string | Credit card expiry  \n`card_token` | string | Credit card token  \n`card_type` | string | Credit card type  \n`card_category` | string | Credit card category  \n`card_subcategory` | string | Credit card subcategory  \n`response_code` | string | Response code  \n`message` | string | Response message  \n`successful` | boolean | Whether or not the purchase was successful  \n`settlement_date` | string | Settlement date  \n`rrn` | string | RRN  \n`authorization` | string | Authorization code  \n`captured` | boolean | Whether or not the authorization was captured  \n`captured_amount` | integer | Captured amount  \n`metadata` | hash | Additional info  \n`addendum_data` | hash | Addendum data",
    "12-0": "`notifications`",
    "12-1": "array",
    "12-2": "Array of notifications for this chargeback in descending order by received date  \n  \nNotification Hash | | |  \n------------ \\| ------------- \\| ------------  \n`id` | string | Unique ID for the notification  \n`received_at` | string | Date notification was received  \n`merchant_status` | string | Merchant's status for the notification, e.g. Unread, Read  \n`metadata` | hash | Additional info"
  },
  "cols": 3,
  "rows": 13,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

---
title: "Chargeback Notifications"
slug: "chargeback-notifications"
excerpt: "Receiving a Chargeback"
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jul 18 2018 04:30:35 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 19:39:45 GMT+0000 (Coordinated Universal Time)"
---
When a chargeback occurs, Fat Zebra receives a notification of the chargeback and sends you an automated email about it. 

You can subscribe to webhooks for chargeback notifications. Each time our system receives a notification or update, a webhook will be sent containing information on the current and previous notifications related to the chargeback, newest notification first.

```json Webhook Sample
{  
   "acquirer_merchant_id": "ABCDE12345",
   "id": "071-CB-MIP4SIHH",
   "reference": "C2BB3D60",
   "created_at": "2018-07-01T09:30:00.000Z",   
   "amount": 100,
   "reason_code": "865",
   "reason_description": "Service cancelled on 05/04/2018, credit not processed",
   "status": "Matched",
   "merchant_status": "In Progress",
   "due_date": "2018-07-01",
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
     "settlement_date": "2018-02-27",     
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
       "received_at": "2018-07-08T00:00:00.000Z",
       "merchant_status": "Unread",
       "metadata": {
         "chargebackId": "1",
         "chargebackDebitRef": "c2bb3d60-d04b-4c1c-8fd1-9d7a440a6d8b",
         "respondByDate": "15-Jul-18",
         "reasonForChargeback": "Service cancelled on 05/04/2018 ,credit not processed"
       }
     },
     {
       "id": "071-CN-QS0V0OJS",
       "received_at": "2018-07-01T00:00:00.000Z",
       "merchant_status": "Read",
       "metadata": {
         "chargebackId": "2",
         "respondByDate": "7-Jul-18",
         "chargebackRef": "c2bb3d60-d04b-4c1c-8fd1-9d7a440a6d8b",
         "reasonForChargeback": "Service cancelled on 05/04/2018 ,credit not processed"
       }
     }
   ]
}
```

Chargeback webhooks contain the following Fields:

|                               |                                                                                                                                                                        |
| :---------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| acquirer_merchant_id          | Acquirer's merchant ID                                                                                                                                                 |
| id                            | Unique ID for the chargeback                                                                                                                                           |
| reference                     | Reference for the chargeback                                                                                                                                           |
| created_at                    | Date and time when chargeback record was created                                                                                                                       |
| amount                        | A positive integer representing the amount of the chargeback, in the smallest currency unit (eg., 100 to charge $1.00, or 100 to Charge ¥100, a zero decimal currency) |
| reason_code                   | Reason code for the chargeback (See table ...)                                                                                                                         |
| reason_description            | Description of the reason for the chargeback                                                                                                                           |
| status                        | Status of the chargeback, e.g. Matched, Unmatched                                                                                                                      |
| merchant_status               | Merchant's status for the chargeback eg., New, In progress                                                                                                             |
| due_date                      | Date when response must be completed by                                                                                                                                |
| metadata                      | Additional info                                                                                                                                                        |
| purchase                      | Details of the original purchase                                                                                                                                       |
| notifications                 | Array of notifications for this chargeback in descending order by received date                                                                                        |
| notifications.id              | Unique ID for the purchase                                                                                                                                             |
| notifications.received_at     | Date notification was received                                                                                                                                         |
| notifications.merchant_status | Merchant's status for the notification, e.g. Unread                                                                                                                    |
| notifications.metadata        | Additional info                                                                                                                                                        |

---
title: "Merchant Advice Codes (Retries)"
slug: "merchant-advice-codes-retries"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Nov 08 2021 23:43:40 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Oct 05 2022 01:38:31 GMT+0000 (Coordinated Universal Time)"
---
For declined transactions there is a field returned advising the merchant how they should process a retry. The possible values and explanations is listed below:

| Code            | Description/Action to take                                                                                                                       |
| :-------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| update_required | The merchant should contact the customer to obtain updated payment method details. This may be for a new expiry date, CVV or similar.            |
| retry_later     | The merchant should retry the transaction after the timestamp provided in `merchant_advice_retry_after`.                                         |
| do_not_retry    | Do not retry the payment. Contact the customer to obtain an alternative payment method for this transaction.                                     |
| not_supported   | The payment token used is not supported for this transaction. Contact the customer to obtain an alternative payment method for this transaction. |
| cancelled       | The recurring agreement has been cancelled by the customer - Do Not Retry. Contact the customer if necessary to establish a new agreement.       |
| none            | No advice code has been provided. Retry processing up to the merchant to determine.                                                              |

## Retry Later

If a `retry_later` code is received, the merchant should retry after the timestamp provided in the `merchant_advice_retry_after` field. If the field is absent, assume 72 hours.

```json
{
   // ...
   "merchant_advice_code": "retry_later",
   "merchant_advice_retry_after": "2022-10-04T15:39:55+11:00"
}
```

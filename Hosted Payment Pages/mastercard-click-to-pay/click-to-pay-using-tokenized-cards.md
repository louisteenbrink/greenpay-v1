---
title: "Click to Pay - Using tokenized cards"
slug: "click-to-pay-using-tokenized-cards"
excerpt: ""
hidden: false
createdAt: "Thu Nov 09 2023 01:06:39 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Nov 21 2023 03:58:12 GMT+0000 (Coordinated Universal Time)"
---
When you use Click to Pay, you may wish to tokenize a card and then issue a purchase against that card at a later time. You may wish to do this if you're altering the cost of a purchase, such as when you're applying a surcharge or a discount during the checkout flow. Or, if you wish to use this card for recurring purchases.

You can opt-in to this process by using the `tokenize_only` parameter during the checkout flow. Consult either the iframe or SDK pages for how to subscribe to these relevant tokenization events.

In both cases, you'll get back an `'fz.click_to_pay.tokenization.success'` event. This event will contain data in this shape:

```json json
{
  "message": "Card tokenization success.",
  "data": {
    "gatewayResponse": {
      "r": 1,
      "successful": true,
      "token": "d846bgx28s97l3u2ke3k",
      "tokenizeOnly": true,
      "cardHolder": "MasterCard Click To Pay User",
      "cardNumber": "518600XXXXXX8785",
      "cardExpiry": "07/2027",
      "cardType": "MasterCard",
      "cardCategory": "Credit",
      "cardSubcategory": "Standard",
      "clickToPay": {
        "correlationId": "34f4a04b.fa6ba445-8530-458d-856b-6867fce06b46",
        "transactionId": "0a4e0d3.34f4a04b.296f80511b492eda82f4d20017d35c0f12693bfd",
        "flowId": "34f4a04b.fa6ba445-8530-458d-856b-6867fce06b46.1699227515"
      },
      "v": "f4249fe67d0dc3ca86e57353b69d914f"
    },
    "clickToPayResponse": {
      "srcDigitalCardId": "4b20076b-c13b-4a66-a8e1-015caab73d7a",
      "panBin": "518600",
      "panLastFour": "8785",
      "digitalCardData": {
        "descriptorName": "Mastercard",
        "artUri": "https://sbx.assets.mastercard.com/card-art/combined-image-asset/HIGH-MASK-3x.png",
        "isCoBranded": false,
        "status": "ACTIVE"
      },
      "digitalCardFeatures": [],
      "panExpirationMonth": "07",
      "panExpirationYear": "2027",
      "paymentCardDescriptor": "mastercard",
      "paymentCardType": "PREPAID",
      "maskedBillingAddress": {},
      "cardholderFirstName": "R***",
      "cardholderLastName": "B***",
      "cardholderFullName": "R*** B***"
    }
  }
}
```

**Note:** when applying a surcharge, use the first 6 digits of the `gatewayResponse.cardNumber` field. This value is always populated, where as `clickToPayResponse.panBIN` will only be populated in certain situations. Do not rely on `clickToPayResponse.panBIN` being present for surcharge calculation.

We return both the Gateway and Click to Pay response here to give you the most information you need to potentially display the chosen card's information back to the consumer.

The `token` here will be consistent for the selected card, and future purchases through the Click to Pay flow will be tied to this token. We encourage you to continue to route the user through the Click to Pay flow, for security reasons.

### Verifying postmessages

The `v` value returned in `gatewayResponse` is a hash of the token and your account's shared secret. Using the above details of `r=1` and `token=d846bgx28s97l3u2ke3k`, and a shared secret value of `52ccce5a5c5` in a HMAC-MD5 calculation, we combine them like this:

```javascript
HmacMD5("<r value>:<token value>", "<shared secret>").toString();
```

With the above values we get:

```javascript
HmacMD5("1:d846bgx28s97l3u2ke3k", "52ccce5a5c5").toString();
```

And then this results in a verification value of: 

```
7a84eef23efedecb693575315f0c6abb
```

### Submitting purchases after tokenization

When making a purchase request, you should pass your intended amount through (in cents) and token (from `gatewayResponse.token`) through in the request. **If this purchase was initiated from the Click to Pay flow, you should also include the Click to Pay metadata in the transaction.** If this purchase was initiated outside of the Click to Pay flow, such as for a recurring subscription charge, you do not need to include this information.

Here's an example using our Ruby gem, showing how the Click to Pay metadata is included:

```ruby Ruby
FatZebra::Purchase.create(
  amount: 104,
  reference: "ABCD1234"
  token: token,
  customer_ip: customer_ip,
  metadata: {
    click_to_pay_correlation_id: click_to_pay_correlation_id,
    click_to_pay_flow_id: click_to_pay_flow_id,
    click_to_pay_transaction_id: click_to_pay_transaction_id,
  }
 )
```

This metadata is for tracking purposes only, and we can use it to correlate events between users opting-in to the the Click to Pay checkout, and fulfilling a transactional flow.

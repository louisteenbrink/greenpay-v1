---
title: "Masterpass Express"
slug: "masterpass-express"
excerpt: "Masterpass Express gives your customers a faster, easier way to checkout online and gives you a way to increase sales without significantly changing the way you process payments now. Customers can pair their wallet with your website, allowing you to present their shipping address and masked cards at checkout without invoking Masterpass to streamline the experience."
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Mar 13 2019 21:51:21 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Jun 14 2019 05:35:14 GMT+0000 (Coordinated Universal Time)"
---
# Pairing the customer's wallet

Pairing of a Masterpass wallet can be completed two different ways - either through a separate, stand alone pairing request, or as part of a checkout experience.

Documentation on the pairing workflows can be found on the [Mastercard Developer Website](https://developer.mastercard.com/documentation/masterpass-merchant-integration-v7/7#express-checkout2)

Please note: The pairing process returns a pairing ID which is unique for the customer's wallet and the merchant. This pairing ID must be securely stored, and is used to retrieve the customer pre-checkout details. For each request using the pairing ID a new pairing ID is returned, which should replace the pairing ID stored for that customer. Failure to store this new ID with each request will result in the pairing link becoming broken and the pairing will need to be recreated before a customer can use Masterpass Express again.

# Using Masterpass Express on your Website

Once a customer is paired with your website it is possible to retrieve and present their preferred shipping and payment options (this step is called pre-checkout). The customer then selects their card and shipping address, then the merchant executes the Express Checkout with Masterpass via the Masterpass API from the merchant's server. Documentation on the Server-side API can be found on the [Mastercard Developer website](https://developer.mastercard.com/documentation/masterpass-merchant-integration-v7/7#express-checkout2).

Upon successful completion of the Masterpass Express Checkout the credit card transaction can be processed with the Gateway. 

The Purchase request to the gateway requires the core parameters, such as the amount, merchant reference, etc, however instead of card details a wallet field is provided, with the wallet type (MASTERPASSEXPRESSV7), and the transaction ID used in Pre-checkout. For example:

```json
POST /v1.0/purchases HTTP/1.1
Content-type: application/json

{
	"reference": "ORD-12129",
  "amount": 382490,
  "customer_ip": "203.202.112.98",
  "wallet": {
    "type": "MASTERPASSEXPRESSV7",
    "token": {
      "pre_checkout_transaction_id": "e956e80d-b00c-4ba6-bb48-8eab7e64e746"
    }
  }
}
```

For previous versions of the Masterpass integrations the Gateway response for the transaction would include wallet details, such as the customer's billing address, shipping address etc, however the majority of this information is now provided to the merchant from the Masterpass libraries, in the response the merchant receives from the Masterpass Express Checkout create method.

An example of the wallet data returned with Masterpass Express is as follow:

```json
"wallet": {
  "card_source_reference": "02495831-ee5c-49d1-83bd-4e0ae5927d91",
  "address": {
    "line_1": "Testing",
    "line_2": null,
    "city": "Test",
    "state": "AU-NSW",
    "postcode": "1111"
  }
}
```

---
title: "Amex Express Checkout"
slug: "amex-express-checkout"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jul 18 2018 02:22:23 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 20:15:55 GMT+0000 (Coordinated Universal Time)"
---
To add Amex Express Checkout to your ecommerce website or application:

1. Add the Amex Express Checkout iframe and Javascript Integration to your website or application.
2. Submit the **auth_code**, **wallet_id**, **transaction_id** and card_type from the request to fat Zebra via our **Credit Card Tokenization API** or our [Purchases API](ref:purchases).

> 📘 The Fat Zebra WooCommerce plugin has been updated to include Amex Express Checkout out of the box. For setup simply ensure you have the latest version of the plugin and then enable Amex Express Checkout from within WooCommerce Settings → Checkout → Amex Express Checkout.

# Setting up your Amex Express Checkout Profile

There is nothing to do here - your merchant account is already setup with Amex Express Checkout when your Amex Internet Merchant Facility is setup in the Gateway.

# Add the Amex Express Checkout Button

To display the Amex Express Checkout button within your website add the following HTML to embed the button within a transparent iframe:

```html
<iframe src="https://paynow-sandbox.pmnts.io/v2/amexeco/[username]/[nonce]/[currency]/[amount]/x?tokenize_only=true&amp;postmessage=true"
  frameborder="0"
  height="38"
  width="155"
  seamless="seamless"
  allowtransparency="true"
  scrolling="no"
  style="position:relative; margin-top: -20px; top: 15px;">
</iframe>
```

Within the iframe `src` attribute, replace the following values:

| Placeholder | Description                                          |
| :---------- | :--------------------------------------------------- |
| username    | Your Fat Zebra gateway username                      |
| nonce       | A unique ID or reference for the checkout or session |
| currency    | The 3-letter currency code for the transaction       |
| amount      | The total amount for the transaction                 |

# Add the Javascript

Once a customer completes the Amex Express Checkout process a message will be returned to the webpage hosting the iframe with the parameters required by the Gateway to complete the transaction. The following Javascript will receive this message and inject the values into a form to be submitted to your website:

```javascript
jQuery(function() {
  jQuery(window).on('message onmessage', function(e) {
    var payment = e.originalEvent.data;
    var form = jQuery('#checkout-form');
    // Display 'loading' indicator here
    for(var key in payment) {
      form.append("<input type='hidden' name='" + key + "' value='" + payment[key] + "' />");
    }

    form.submit();
  });
});
```

# Submit the `auth_code`, `wallet_id`, `transaction_id` and `card_type` to Fat Zebra for Tokenization of Purchase Transactions

Once you have received a successful Amex Express Checkout from the Javascript Integration there are two methods of making use of the Payment Details:

- Tokenize the card details for checkout workflows such as requiring confirmation or calculation of shipping costs based on the address details returned from Amex Express Checkout
- Perform a purchase with the credentials for workflows which do no need the shipping details before determining the final value of the transaction (e.g. digital products without shipping, access to online services etc)

Both options use the standard Fat Zebra **Gateway API** for **Purchases** and **Credit Cards**, however instead of providing card details (card holder, card number, expiry date, security code) a `wallet` payload is included in the request as seen below (credit card request):

```json
{
  "wallet": {
    "type": "AMEX",
    "auth_code": "08d9cba9-5b51-4b60-8139-af1117a4be8d",
    "transaction_id": "746af2a72d31e5f6cc8f14c68452b8c3",
    "wallet_id": "01",
    "card_type": "AMEX"
  }
}
```

For both a Credit Card and Purchase request a `wallet` payload will be included in the response which includes:

- email address
- first and last name
- address
  - line 1
  - line 2
  - city
  - state
  - postcode
  - phone number
- card source reference (the Amex Express Checkout `transaction_id`)

An example response from tokenizing a credit card with a Amex Express Checkout credentials can be seen below:

```json
{
  "successful": true,
  "response": {
    "token": "95p4npi2",
    "card_holder": "John Smith",
    "card_number": "376070XXXXX1008",
    "card_expiry": "2018-12-31T23:59:59+11:00",
    "card_type": "AMEX",
    "card_category": "Credit",
    "card_subcategory": "Credit",
    "authorized": true,
    "transaction_count": 0,
    "alias": null,
    "wallet": {
      "name": {
        "first": "John",
        "last": "Smith"
      },
      "address": {
        "line_1": "50 Martin Place",
        "line_2": "2nd Floor",
        "city": "Sydney",
        "state": "NSW",
        "postcode": "2000",
        "country": "AU",
        "phone": "61282231111"
      },
      "email": "john.smith@gmail.com",
      "card_source_reference": "746af2a72d31e5f6cc8f14c68452b8c3"
    }
  },
  "errors": [],
  "test": true
}
```

For more details on creating purchases using the Amex Express Checkout credentials please see the [Create a purchase, with a wallet](ref:create-a-purchase) document. If the merchant needs to retrieve the customers details prior to performing a transaction a tokenization request can be made in stead of a purchase request. For more details please see **Tokenization with Wallet**.

# Further Help

If you require any further assistance with your Amex Express Checkout integration please contact [Fat Zebra Support](mailto:support@fatzebra.com?subject=Visa+Checkout+Enquiry) with your questions and we will be more than happy to assist or provide guidance where possible.

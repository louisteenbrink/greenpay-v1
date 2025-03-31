---
title: "Click to Pay"
slug: "click-to-pay"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jul 18 2018 02:22:14 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Sep 07 2023 23:57:13 GMT+0000 (Coordinated Universal Time)"
---
[block:html]
{
  "html": "<div>\nPay with confidence with the same payment brands you use today. For an easy and smart checkout, simply click to pay wherever you see the Click to Pay icon <img src=\"https://files.readme.io/0938bb0-acc_40x30_blu01.png\"/>and your card is accepted. Click to Pay is built on industry security standards for online transactions.\n</div>\n\n<style></style>"
}
[/block]


# Click to Pay Customer Workflow

- Create an account once and speed through checkout without having to re-enter payment or shipping information wherever you see Click to Pay.
- Checkout with a single username and password across the sites you love to shop.
- Visa secures access to your account with advanced security tools, so you can shop online with confidence.
- Consistent, simple experience across desktop, mobile web and apps. Easy to activate with any major credit or debit card.
- Earn the same great rewards with the card you already use.
- Seamless web and mobile checkout without ever leaving merchant site.

# Using Click to Pay on your website

> 📘 Fat Zebra currently has pre-built support for Click to Pay in WooCommerce with [version 1.5.0 of our plugin](https://wordpress.org/plugins/woocommerce-fat-zebra-gateway/). We are also building plugins and extensions for other supported carts however we do not yet have an expected release date.

In order to add Click to Pay to your eCommerce website or application:

1. Review and accept the Click to Pay Merchant Services agreement to create your Click to Pay profile.
2. Add the Click to Pay JavaScript Integration or Mobile Application SDK to your website or application.
3. Submit the `callid` from the request to Fat Zebra via our Credit Card Tokenization API or our Purchases API.

# Setting up your Click to Pay Profile

In order to setup the Click to Pay profile you must first review and accept the Click to Pay Merchant Service Agreement (MSA). To do this:

1. Log into the Merchant Dashboard.
2. Click on the My Account link on the left hand side and then click the Click to Pay link.
3. Review and accept the Click to Pay MSA.
4. Once the MSA has been accepted you will be provided with your Click to Pay API Key.

To view your Click to Pay API Key at a later date you can visit the same **My Account** → **Click to Pay page**.

# Integrating Click to Pay

## JavaScript SDK

The Click to Pay JavaScript Integration consists of the following steps:

### 1. Add the anti-click jacking protection

One of the fundamental steps for protecting the customer from click-jacking is to include anti-click jacking protections into any website pages where the Click to Pay lightbox is included. These protections include both the X-Frame-Options header and the anti-clickjacking code to be included in the head section of the page.

_X-Frame-Options_

Most newer browsers now understand and support the [X-Frame-Options](https://developer.mozilla.org/en-US/docs/Web/HTTP/X-Frame-Options) header. For your website you should ensure that the response header for the checkout page, or any page where the Click to Pay widget is included, includes the following header:

`X-Frame-Options: Deny`

or

`X-Frame-Options: SAMEORIGIN`

or

`X-Frame-Options: ALLOW-FROM uri`

_Anti-Click Jacking Markup_  
The following markup should be included in the head section of any page hosting the Click to Pay lightbox:

```html
<head>
  <style id="antiClickjack">body{display:none;}</style>
  <script type="text/javascript">
    if (self === top) {
      var antiClickjack = document.getElementById("antiClickjack");
      antiClickjack.parentNode.removeChild(antiClickjack);
    } else {
      top.location = self.location;
    }
  </script>
</head>
```

More information on anti-click jacking techniques can be found on the [OWASP Clickjacking Defence Cheat Sheet](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet)

### 2. Add the `onVmeReady()` function to the checkout page

The following code should be added to the head section of the checkout page:

```html
<script>
  function onVmeReady() {
    V.init({
      apikey: "API_KEY_FROM_DASHBOARD",
      // Any further initalization options can be added here
    });
  }
</script>
```

In the `V.init` method call it is possible to customise the checkout experience including:

- Adding your logo and name
- Customising the text displayed in the confirmation page
- Choosing whether to display a Continue or Pay button
- Indicate if the shipping details should be selected
- Indicate the card types to be accepted

For full details on the options for the `V.init` method call please see the [Click to Pay Javascript Integration Guide (section 2-1 to 2-10)](https://developer.visa.com/vme/merchant/documents/Visa_Checkout_JavaScript_Integration_Guide/Integration_Overview.html).

### 3. Add the payment request details to the `V.init` call

In addition to the API Key you will need to include the payment request details as seen below:

```html
<script>
  function onVmeReady() {
    V.init({
      apikey: "API_KEY_FROM_DASHBOARD",
      paymentRequest: {
        currency: "AUD",
        total: 150.51
      }
    });
  }
</script>
```

### 4. Add the event handlers for the Click to Pay lightbox events

```html
<script>
  function onVmeReady() {
    V.init({
      apikey: "API_KEY_FROM_DASHBOARD",
      paymentRequest: {
        currency: "AUD",
        total: 150.51
      }
    });

    V.on("payment.success", function(payment) {
      alert("Checkout successful. Call ID (to be sent to Fat Zebra): " + payment.callid);
    });
    V.on("payment.cancelled", function(payment) {
      alert("Click to Pay payment cancelled. Please retry or try another payment method.");
    });
    V.on("payment.error", function(payment, error) {
      alert("Click to Pay payment failed. Error details: " + JSON.stringify(error));
    });
  }
</script>
```

More details on the `V.on` events can be found in the [Click to Pay Javascript Integration Guide](https://developer.visa.com/vme/merchant/documents/Visa_Checkout_JavaScript_Integration_Guide/Integration_Overview.html), section 2-12 to 2-14.

### 5. Add the Click to Pay Button

Finally add the following code in your web page where you would like the Click to Pay button to be displayed (note: the CSS for the Click to Pay button can be included in an external CSS file provided it is included in any pages the Click to Pay button is rendered):

```html
<style type="text/css">
  #custom-visa-checkout-outer-container{
    position:relative;
  }
 
  #custom-visa-checkout-learn-more{
    width:210px;
    text-align:right;
  }
  #custom-visa-checkout-learn-more-text{
    font:bold 8.5pt arial;
    text-decoration: none;
    color: #0044AA;
  }
</style>
 
<div id="custom-visa-checkout-outer-container">
  <img alt="Button" class="v-button" data-2x-image="https://secure.checkout.visa.com/wallet-services-web/xo/button.png?locale=en_AU&amp;card_brands=VISA,MasterCard&amp;style=color&amp;size=425" height="47" id="v-checkout-button" role="button" src="https://secure.checkout.visa.com/wallet-services-web/xo/button.png?locale=en_AU&amp;card_brands=VISA,MasterCard&amp;style=color&amp;size=213" width="213" style="cursor: pointer; width: 213px;">
  <div id="custom-visa-checkout-learn-more">
    <a href="javascript:void(0)" id="custom-visa-checkout-learn-more-text" onclick="document.getElementById('custom-visa-checkout').style.display='block'" >Learn More</a>
  </div>
  <img id="custom-visa-checkout" src="https://assets.secure.checkout.visa.com/VmeCardArts/partner/Cart_LearnMore_Pop-Up_left.png" style="display:none;z-index:9999;position:absolute; top: -170px; left: 220px;" onclick="document.getElementById('custom-visa-checkout').style.display='none';" />
</div>
```

It is highly recommended that the Click to Pay button markup is not modified in any way, especially with regards to the "Learn More" link. It is permitted to modify the stylesheets for the "Learn More" images or positioning to ensure it works properly in your website provided it adheres to the [Visa Branding Requirements](https://developer.visa.com/vme/merchant/documents/Getting_Started_With_Visa_Checkout/Branding_Requirements.html).

## Mobile SDK

For information on the Click to Pay Mobile SDK please see the guides provided at the [Click to Pay Documentation website](https://developer.visa.com/vme/merchant/documents/Mobile_SDKs/ios/Getting_Started_With_the_Visa_Checkout_SDK.html).

### Submit the `callid` to Fat Zebra for Tokenization of Purchase Transactions

Once you have received a successful Click to Pay `callid` from the Javascript Integration or Mobile SDK there are two methods of making use of the Payment Details:

1. Tokenize the card details for checkout workflows such as requiring confirmation or calculation of shipping costs based on the address details returned from Click to Pay.
2. Perform a purchase with the `callid` for workflows which do not need the shipping details before determining the final value of the transaction (e.g. digital products without shipping, access to online services etc).

Both options use the standard Fat Zebra **Gateway API** for **Purchases** and **Credit Cards**, however instead of providing card details (card holder, card number, expiry date, security code) a `wallet` payload is included in the request as seen below (credit card request):

```json
{
  "wallet": {
    "type": "VISA",
    "callid": "123456789901233456789" // The payment.callid value from the Javascript integration, or the Mobile SDK result callid.
  }
}
```

For both a Credit Card and Purchase request a wallet payload will be included in the response which includes:

- email address
- first and last name
- address
  - line 1
  - line 2
  - city
  - state
  - postcode
  - phone number
- card source reference (the Click to Pay `callid`)

An example response from tokenizing a credit card with a Click to Pay callid can be seen below:

```json
{
  "successful": true,
  "response": {
    "token": "kkmz2w9k",
    "card_holder": "Test",
    "card_number": "555544XXXXXX2226",
    "card_expiry": "2020-10-31T23:59:59+11:00",
    "authorized": true,
    "transaction_count": 0,
    "wallet": {
      "name": {
        "first": "Matthew",
        "last": "Savage"
      },
      "address": {
        "line_1": "1 Smith Road",
        "line_2": null,
        "city": "Test",
        "state": "NSW",
        "postcode": "2625",
        "phone": "0421858913"
      },
      "email": "matt@amasses.net",
      "card_source_reference": "4259122687658622628"
    }
  },
  "errors": [
  ],
  "test": true
}
```

**Note:** it is important to remember that an address will not be available in the response if `collectShipping` is not set to `true` in the `V.init` options.

For more details on creating purchases using the Click to Pay `callid`, please see [Create a purchase using a wallet](ref:create-a-purchase-with-wallet). If the merchant needs to retrieve the customers details prior to performing a transaction, a tokenization request can be made instead of a purchase request. For more details, please see [Tokenize a card with wallet credentials](ref:tokenize-a-card-with-wallet-credentials).

## Further Help

If you require any further assistance with your Click to Pay integration please contact [Fat Zebra Support](mailto:support@fatzebra.com) with your questions and we will be more then happy to assist or provide guidance where possible.

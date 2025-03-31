---
title: "Click to Pay"
slug: "mastercard-click-to-pay"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Sep 12 2023 05:06:41 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sun Nov 12 2023 22:08:10 GMT+0000 (Coordinated Universal Time)"
---
[Click to Pay](https://www.mastercard.com.au/en-au/personal/ways-to-pay/click-to-pay.html) is a simple, secure, and consistent way to checkout.

It is built on Industry standards on [EMV](https://www.emvco.com) specifications and smart security powered by Mastercard and is supported by major card schemes, such as Mastercard, Visa, and others.

With millions of customers already enrolled in Click to Pay, leverage this capability to provide your customers a faster, secure, and best in class payment experience.

We integrate to Click to Pay for all participating networks (including Mastercard and Visa) via Mastercard SRCi system providing an embedded checkout experience and currently support three methods of integration:

- [Hosted Page ](https://docs.fatzebra.com/reference/click-to-pay-hosted-payment-page)(i.e. redirection from the merchants website to the payment page) -- we host the whole checkout flow for you and redirect back to your site (when the `return_path` option is provided).
- IFrame embed -- you embed the Click to Pay iframe within your own checkout flow, and we send events from the frame back to the parent page. 
- [JavaScript SDK](https://docs.fatzebra.com/reference/click-to-pay-javascript-sdk) -- this embeds the iframe in a page for you and provides features to hook into those events.

Both methods support Mastercard and Visa payment methods.

## Testing

### Sandbox Testing

First, enroll with Mastercard's Sandbox by entering your details here: <https://sandbox.src.mastercard.com/profile/enroll>. Once you have a Click to Pay account you can then start using it.

### Approved Credit Card Numbers

The credit card numbers are different from the Fat Zebra test card numbers, as these are Mastercard or Visa specific test card numbers.

These numbers will all result in an "Approved" purchase when used with Click to Pay:

- 5186001700008785
- 5186001700009726
- 5186001700009908
- 5186001700008876
- 4622943127011022
- 4622943127011030
- 4622943127011048
- 4622943127011055
- 4622943127011063

You can find out more information about these cards here: <https://developer.mastercard.com/unified-checkout-solutions/documentation/testing/test_cases/click_to_pay_case/#test-cards>

### Variable response credit card numbers

To test "variable response" card numbers, use the cents value of a purchase's price to specify which[ Response Code](https://docs.fatzebra.com/docs/response-codes) you would like. For example, a purchase with a price of $123.05 and any of the following cards would result in an 05 - Declined response.

PAN Data cards:

- 5120350100064545
- 5120350100064552
- 5186001700008876
- 5120350100064578
- 5186001700001434

Token Data cards:

- 5120350100064537
- 5120350100064545
- 5120350100064552
- 5120350100064560
- 5120350100064578

### Mastercard Click-To-Pay Action Sheet

Installation: 

CDN:

| Environment | URL                                                |
| :---------- | :------------------------------------------------- |
| Staging     | <https://cdn.pmnts-staging.io/sdk/v1/fatzebra.css> |
| Sandbox     | <https://cdn.pmnts-sandbox.io/sdk/v1/fatzebra.css> |
| Production  | <https://cdn.pmnts.io/sdk/v1/fatzebra.css>         |

These are the classes and id's required to display MasterCard's recommended action sheet for click-to-pay.

```
    <main class="main-container" id="mainContent">
      <div class="checkout-button-wrapper">
        <button type="button" id="checkoutButton">checkout</button>
      </div>
      <div class="iframe-container slide-in" id="iframeContainer">
        <div class="iframe-foreground">
          <iframe class="iframe-checkout" id="checkoutIframe" name="checkout-iframe"></iframe>
        </div>
        <div class="iframe-background" id="iframeBackground" />
      </div>
    </main>
```

This will render: 

on Desktop an animated side bar: 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/509475b-Screenshot_2023-11-10_at_11.33.31_am.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


on Mobile an animated action sheet:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e71d195-Screenshot_2023-11-10_at_11.33.16_am.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


For further reference:

<https://github.com/Mastercard/action-sheet-reference-app>

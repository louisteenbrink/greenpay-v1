---
title: "Overview"
slug: "javascript-sdk-overview"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jul 23 2020 05:11:12 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Nov 10 2023 01:38:53 GMT+0000 (Coordinated Universal Time)"
---
## Introduction

Fat Zebra provides a Javascript SDK named **fatzebra.js** that enables merchants to access features including:

- [3DS2](3ds2-overview)
- iFraming Hosted Payments Page via Javascript
- PayPal checkout flow

### Authentication

Each feature accessible via fatzebra.js requires OAuth authentication whereby merchants obtain an OAuth access token for each payment session required. Refer to [Obtain an OAuth token](doc:obtain-oauth-token) for more details.

### SDK source

| Environment | URL                                               |
| :---------- | :------------------------------------------------ |
| Staging     | <https://cdn.pmnts-staging.io/sdk/v1/fatzebra.js> |
| Sandbox     | <https://cdn.pmnts-sandbox.io/sdk/v1/fatzebra.js> |
| Production  | <https://cdn.pmnts.io/sdk/v1/fatzebra.js>         |

### Mastercard Click-To-Pay Action Sheet

Installation: 

CDN:

| Environment | URL                                                |
| :---------- | :------------------------------------------------- |
| Staging     | <https://cdn.pmnts-staging.io/sdk/v1/fatzebra.css> |
| Sandbox     | <https://cdn.pmnts-sandbox.io/sdk/v1/fatzebra.css> |
| Production  | <https://cdn.pmnts.io/sdk/v1/fatzebra.css>         |

NPM

```
npm i @fat-zebra/sdk
```

then import the stylesheet

```
@import '@fat-zebra/sdk/dist/fatzebra.css';
```

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

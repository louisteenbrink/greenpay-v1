---
title: "Hosted Payments Page Integration"
slug: "hosted-payments-page-integration"
excerpt: "Instructions detailing how to integrate Google Pay™ into your Website using the Fat Zebra Hosted Payments Page"
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri May 24 2019 05:08:09 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 20:33:14 GMT+0000 (Coordinated Universal Time)"
---
# Pre-requisites

- Read the [Google Pay Web Brand Guidelines](https://developers.google.com/pay/api/web/guides/brand-guidelines)
- Read the [Google Pay APIs Acceptable Use Policy](https://payments.developers.google.com/terms/aup). You must adhere to this policy when integrating the Fat Zebra Hosted Payments Page.
- Prior to implementing Google Pay, contact the [Fat Zebra support team](mailto:support@fatzebra.com) to have Google Pay enabled on your account. You will be required to agree to the Google Pay Terms of Services in the [Merchant Dashboard](https://dashboard.pmnts.io). The Fat Zebra support representative will provide instructions on how to do this.

# Implementation Steps

Follow the instructions in the Fat Zebra [Hosted Payments Page documentation](ref:hosted-payment-pages). A Google Pay button will be displayed by default on the Hosted Payments Page once Google Pay has been enabled on your account.

If you chose to integrate the Hosted Payments Page via an iframe you will need to specify  **allowpaymentrequest** on the **<iframe>** tag:

```html iframe with allowpaymentrequest attribute
<iframe
  allowpaymentrequest
  height='800'
  src='https://paynow.pmnts.io/xxxx/invoices?iframe=1&nonce=7705a1dd&ts=1511737426&v=8f14f3f99769ce96b2488dc4a1350ff8'
  width='600'>
</iframe>
```

If your **<iframe>** element uses the [**sandbox attribute**](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#attr-sandbox), an **allow-popups** token should be set to allow display of the Google Pay payment sheet in a new window:

```html iframe with sandbox attribute
<iframe
  allowpaymentrequest
  sandbox="allow-popups"
  height='800'
  src='https://paynow.pmnts.io/xxxx/invoices?iframe=1&nonce=7705a1dd&ts=1511737426&v=8f14f3f99769ce96b2488dc4a1350ff8'
  width='600'>
</iframe>
```

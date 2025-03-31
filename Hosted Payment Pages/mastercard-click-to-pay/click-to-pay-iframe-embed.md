---
title: "Click to Pay - iFrame Embed"
slug: "click-to-pay-iframe-embed"
excerpt: ""
hidden: false
createdAt: "Tue Nov 07 2023 23:27:53 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Nov 05 2024 23:35:50 GMT+0000 (Coordinated Universal Time)"
---
When using the iframe embed option, generate a URL as per the steps outlined in the [Configuration documentation](https://docs.fatzebra.com/reference/click-to-pay-configuration).

## Cross-frame communication (with `tokenizeOnly`)

When the `tokenize_only` parameter is set to `true`, and the `postmessage` parameter to `true`, then your parent frame will receive an event, which you can subscribe with this code:

```
<script>
  window.paymentHost = "https://paynow.pmnts-sandbox.io";

var messageListener = function(event) {
  if (event.origin !== window.paymentHost) {
    return;
  }

  if ('data' in event === false) {
    return
  }

  switch (event.data.subject) {
    case "fz.click_to_pay.tokenization.success":
      // Handle successful tokenization.
    case "fz.click_to_pay.tokenization.error":
      // Handle tokenization error.
  }
};

window.addEventListener("message", messageListener)
</script>

```

The shape of the data is documented on the ["Using tokenized cards" page](https://docs.fatzebra.com/reference/click-to-pay-using-tokenized-cards).

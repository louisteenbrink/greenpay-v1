---
title: "Click to Pay - iFrame Embed with events"
slug: "click-to-pay-iframe-embed-events"
excerpt: ""
hidden: true
createdAt: "Tue Nov 05 2024 23:29:56 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Nov 06 2024 00:20:15 GMT+0000 (Coordinated Universal Time)"
---
When using the iframe embed option, generate a URL as per the steps outlined in the [Configuration documentation](https://docs.fatzebra.com/reference/click-to-pay-configuration).

## Event subscription

When the `postmessage` parameter is set to `true`, you can subscribe to the events listed below with the following code:

```
<script>
window.paymentHost = "https://paynow.pmnts-sandbox.io";

const messageListener = function(event) {
  if (event.origin !== window.paymentHost) {
    return;
  }

  if ('data' in event === false) {
    return
  }

  switch (event.data.subject) {
    case "fz.click_to_pay.tokenization.success":
      // Handle successful tokenization.
      const eventData = event.data.data
    ...
  }
};

window.addEventListener("message", messageListener)
</script>

```

## Events

The following events may be subscribed to during the Click to Pay flow:

- `fz.click_to_pay.dcf` - emitted when the Digital Checkout Flow (DCF) is loaded. The card scheme hosting the flow is indicated in the event data.

```
{
  channel: 'click_to_pay',
  subject: 'fz.click_to_pay.dcf',
  data: {  
    cardScheme: <'visa'|'mastercard'|'amex'>  
  },
}
```

- `fz.click_to_pay.initial_mrt_req` - emitted on initialisation of the Click to Pay flow. 

```
{
  channel: 'click_to_pay',
  subject: 'fz.click_to_pay.initial_mrt_req',
  data: {}
}
```

When this event is received and there is a recognition token persisted in the user's browser cookies, it needs to be fetched and sent back to the PayNow iframe via postmessage:

```
// fetch the recognition token
const mrt = <recognition token value>

const message = {
  channel: 'click_to_pay',
  subject: 'fz.click_to_pay.initial_mrt_res',
    data: {
      mrt
    },
};

// get a reference to the PayNow iframe element (here it is nested within a containing div with id="fz-paynow")
const paynowIframe = document.querySelector('#fz-paynow iframe')

// send the recognition token to the PayNow iframe via postmessage
paynowIframe.contentWindow.postMessage(message, window.paymentHost)
```

- `fz.click_to_pay.mrt` - emitted if a user elects to be remembered in the browser in a new user checkout/OTP flow AND a recognition token is returned during the Click to Pay checkout. The recognition token value is provided in the event data.
  - When a non-null token value is emitted, it should be persisted as a first-class cookie.
  - When a null token value is emitted (signifying user sign-out), any associated cookie should be removed. 
  - On the call to `renderClickToPay()`, the cookie value should be fetched and passed in via the `mrt`option. This value will then be used to initialise the Click to Pay checkout. 

```
{
  channel: 'click_to_pay',
  subject: 'fz.click_to_pay.mrt',
  data: {
    mrt: <token value> 
  }
}
```

- `fz.click_to_pay.resize` - emitted when the Click to Pay container is resized. The new container height (in pixels) is provided in the event data. Note that this event will not be emitted when the DCF flow is entered as this content is controlled by the card schemes. We provide the `fz.click_to_pay.dcf`event to notify when this flow is launched, together with the hosting card scheme, to assist with appropriately sizing the container.  

```
{
  channel: 'click_to_pay',
  subject: 'fz.click_to_pay.resize',
  data: { 
    heightPx: <number> 
  }
}
```

- `fz.click_to_pay.tokenization.success` - emitted on tokenization success when the `tokenize_only` parameter is set to `true`. This event's body and how to use it is explained further in the ["Using Tokenized Cards"](https://docs.fatzebra.com/reference/click-to-pay-using-tokenized-cards)  page.

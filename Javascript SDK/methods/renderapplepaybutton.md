---
title: "renderApplePayButton"
slug: "renderapplepaybutton"
excerpt: ""
hidden: true
createdAt: "Mon Aug 12 2024 02:09:38 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Aug 28 2024 04:11:06 GMT+0000 (Coordinated Universal Time)"
---
# renderApplePayButton(ApplePaySetupParams)

Renders the Fat Zebra Hosted Apple Pay Web button within the specified div element (see `containerId` in the example below).

The below example includes rendering of the payment form as well as the apple pay button.

```Text javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JS SDK</title>
    <style>
        .title {
            font-size: 2rem;
            font-weight: bold;
        }

        .flex {
            display: flex;
        }

        .mb-8 {
            margin-bottom: 2rem;
        }

        .mr-6 {
            margin-right: 1.5rem;
        }

        .ml-6 {
            margin-left: 1.5rem;
        }

        .mt-4 {
            margin-top: 1rem;
        }

        .gap-4 {
            gap: 1rem;
        }

        #fz-payment-form iframe {
            height: 350px;
        }
    </style>
    <script type="text/javascript" src="https://cdn.pmnts.io/sdk/v1/fatzebra.js"></script>
</head>
<body>

<h2 class="title is-2">JS SDK</h2>

<div class="flex mb-8" style="height: 450px; width: 300px;">
    <div class="flex flex-col mt-4 gap-4">
        <div id="fz-payment-form" class="hpp-button-show mr-6"></div>
        <div>Pay with Apple Pay</div>
        <div id="fz-apple-pay-button" style="width: 300px; height: 30px;" class="hpp-button-show mr-6"></div>
    </div>
    <div class="flex flex-col">
        <div id="messages" class="ml-6"></div>
    </div>
</div>
<script type="text/javascript">
  localStorage.setItem('fz-access-token', oauth_token);
  const username = "TEST"
  const version = 3
  const amount = 100
  const currency = "AUD"
  const reference = "REF1234"
  const verification = <hash_of_ref_amount_currency>
    const environment = "production"
    const options = {
    allowed_card_networks: ['visa'],
    allowed_card_types: ['supportsCredit']
  }

    const fz = new FatZebra({username});


    // See event section on handling events
    fz.on('fz.form_validation.error', function(event) {
    notify(event.type, event.detail.message, 'is-danger');
    console.log(`event type: ${event.type}, message: ${event.detail.message}`)
  });

    # Render payment form
  fz.renderPaymentsPage({
    containerId: 'fz-payment-form',
    version,
    paymentIntent: {
    payment: {
    amount,
    currency,
    reference
  },
    verification
  },
    options: {
    ...options,
    css: "<https hosted css>",
    css_signature: <hash_of_url_hosted_css>
  }
      });
    # Render apple pay button
  fz.renderApplePayButton({
    containerId: 'fz-apple-pay-button',
    environment,
    paymentIntent: {
      payment: {
        amount,
        currency,
        reference
    },
      verification
    },
    options
  });
</script>

</body>
</html>

```

Options

[block:parameters]
{
  "data": {
    "h-0": "Option",
    "h-1": "Supported Params",
    "h-2": "Default",
    "0-0": "allowed_card_networks",
    "0-1": "amex, chinaUnionPay, discover, jcb, maestro, masterCard, visa",
    "0-2": "visa, masterCard",
    "1-0": "allowed_card_types",
    "1-1": "supportsCredit, supportsDebit, supportsEMV (for chinaUnionPay)",
    "1-2": "supports3DS, supportsCredit,  \nsupportsCredit"
  },
  "cols": 3,
  "rows": 2,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

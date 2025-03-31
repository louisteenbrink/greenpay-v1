---
title: "Validation"
slug: "validation"
excerpt: "Error messages can be produced when incorrect data is passed to JS SDK methods"
hidden: false
createdAt: "Fri Jul 24 2020 00:54:22 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jan 22 2025 04:49:34 GMT+0000 (Coordinated Universal Time)"
---
| Event                 | Description                                                               | Applicable Methods                                                                                   |
| :-------------------- | :------------------------------------------------------------------------ | :--------------------------------------------------------------------------------------------------- |
| `fz.validation.error` | Client-side validation errors occurred while calling fatzebra.js methods. | [verifyCard](doc:verifycard), [renderPaymentsPage](doc:renderpaymentspage), [checkout](doc:purchase) |

Examples of validation errors include:

### Required fields

Calling `fz.renderPaymentsPage` without specifying an amount like this:

```
fz.renderPaymentsPage({
  containerId: 'fz-paynow',
  version: 3,
  paymentIntent: {
    payment: {
      currency: "AUD",
      reference: "ABCD1234",
    }
  },
  verification: 'verification-hash-goes-here'
});
```

 Will give you a validation error:

```json fz.validation.error data payload - required field
{
  errors: [
    "/paymentIntent/payment/amount is required",
    ...
  ],
  data: null
}
```

### Data type invalid

Similarly, providing an invalid value for fields:

```
fz.renderPaymentsPage({
  containerId: 'fz-paynow',
  version: 3,
  paymentIntent: {
    payment: {
      amount: "100 dollarydoos",
      currency: "AUD",
      reference: "ABCD1234",
    }
  },
  verification: 'verification-hash-goes-here'
});
```

Will also produce a validation message:

```json fz.validation.error data payload - data type invalid
{
  errors: [
    "/paymentIntent/payment/amount should be an integer",
    ...
  ],
  data: null
}
```

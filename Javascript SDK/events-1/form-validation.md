---
title: "Form Validation (V2)"
slug: "form-validation"
excerpt: "Error messages that can be used to indicate which payment form fields have invalid data."
hidden: false
createdAt: "Tue Aug 10 2021 02:51:06 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jan 22 2025 04:51:12 GMT+0000 (Coordinated Universal Time)"
---
> 🚧 Hosted Payments Page form validation errors are propagated to the parent frame (merchant website) via fz.form_validation.error event. This is distinct from the `fz.validation.error`, which is used to indicate errors to do with calls to functions such as `renderPaymentsPage`

| Event                      | Description                            | Applicable Methods                           |
| :------------------------- | :------------------------------------- | :------------------------------------------- |
| `fz.form_validation.error` | Hosted Payments Form validation errors | [renderPaymentsPage](doc:renderpaymentspage) |

## fz.form_validation.error Data Payload

Example

```json
{
  "message": "Form was not valid",
  "errors": [
    "Expiry Date is required",
    "Security Code (CVV) is required"
  ],
  "data": {
    "payment_request_expiry_date": [
      {
        "errorCode": "hpp_10401",
        "message": "Expiry Date is required"
      }
    ],
    "payment_request_security_code": [
      {
        "errorCode": "hpp_10301",
        "message": "Security Code (CVV) is required"
      }
    ]
  }
}
```

- _errors_ contains an array of messages associated with the form validation errors.
- _data_ provides details around the affected fields and the associated errors, along with error codes. Developers can take advantage of the error code in order to customise the user experience.

## Validation Rules

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Rule",
    "h-2": "Error Code",
    "0-0": "payment_request_card_holder",
    "0-1": "required",
    "0-2": "hpp_10101",
    "1-0": "payment_request_card_holder",
    "1-1": "max length  \n  \n- 50 characters",
    "1-2": "hpp_10102",
    "2-0": "payment_request_card_holder",
    "2-1": "pattern  \n  \n- alphanumeric only",
    "2-2": "hpp_10103",
    "3-0": "payment_request_card_number",
    "3-1": "required",
    "3-2": "hpp_10201",
    "4-0": "payment_request_card_number",
    "4-1": "min length  \n  \n- 13 characters",
    "4-2": "hpp_10202",
    "5-0": "payment_request_card_number",
    "5-1": "max length  \n  \n- 19 characters",
    "5-2": "hpp_10203",
    "6-0": "payment_request_card_number",
    "6-1": "pattern  \n  \n- valid credit card number pattern",
    "6-2": "hpp_10204",
    "7-0": "payment_request_card_number",
    "7-1": "supported card types  \n  \n- **applicable only when `options.cards` is provided**.See [HppSetupParams](doc:hppsetupparams) for details",
    "7-2": "hpp_10205",
    "8-0": "payment_request_security_code",
    "8-1": "required",
    "8-2": "hpp_10301",
    "9-0": "payment_request_security_code",
    "9-1": "min length  \n  \n- 3 characters",
    "9-2": "hpp_10302",
    "10-0": "payment_request_security_code",
    "10-1": "max length  \n_ 4 characters for AMEX & JCB  \n_ 3 characters for everything else. ",
    "10-2": "hpp_10303",
    "11-0": "payment_request_security_code",
    "11-1": "pattern  \n  \n- numeric only",
    "11-2": "hpp_10304",
    "12-0": "payment_request_expiry_date",
    "12-1": "required",
    "12-2": "hpp_10401",
    "13-0": "payment_request_expiry_date",
    "13-1": "valid expiry date  \n  \n- greater than today",
    "13-2": "hpp_10402",
    "14-0": "payment_request_email",
    "14-1": "required  \n  \n- **applicable only when `options.showEmail` is provided**.See [HppSetupParams](doc:hppsetupparams) for details",
    "14-2": "hpp_10501",
    "15-0": "payment_request_email",
    "15-1": "pattern  \n  \n- valid email format",
    "15-2": "hpp_10502",
    "16-0": "payment_request_email",
    "16-1": "max length  \n  \n- 100 characters",
    "16-2": "hpp_10503"
  },
  "cols": 3,
  "rows": 17,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

---
title: "Google Pay™"
slug: "google-pay"
excerpt: "A faster, safer way to pay. Google Pay™ allows your customers to securely and quickly check out in apps and on the web."
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu May 23 2019 06:47:45 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Jun 30 2023 02:45:58 GMT+0000 (Coordinated Universal Time)"
---
# Google Pay Checkout Workflow

- A customer adds a credit, debit, or other payment method into Google Pay. This occurs when the customer adds payment method details into the Google Pay Android or Web app, or when the customer uses a payment method to buy a Google product or service (like an app or movie on Google Play, or storage space for Google Drive).
- The customer chooses to Buy with Google Pay on the merchant's website or Android app and only needs to then select their card and shipping address.
- The merchant receives an encrypted Google Pay token and sends this to Fat Zebra. Your systems are not exposed to the PCI Scope for this data.

# Implementation Methods

There are three methods that merchants can choose from to implement Google Pay with Fat Zebra:

1. **[Android App](android-app-integration)**: integrate Google Pay into an Android application.
2. **[Web Integration](web-integration):** integrate Google Pay into your website using the Google Pay API Javascript client library.
3. **[Via Fat Zebra Hosted Payments Page](hosted-payments-page-integration)**: integrate Google Pay into your website by iframing or redirecting to the Fat Zebra Hosted Payments Page. The Fat Zebra Hosted Payments Page will then handle the Google Pay checkout flow for you.

For instructions on each implementation method, click on the relevant link above.

# Testing

To test Google Pay you must log in to a real Google account - to gain access to the Test Card Numbers provided by Google you must visit the following group and add yourself as a member: <https://groups.google.com/g/googlepay-test-mode-stub-data>

The Google Pay API will not return live, chargeable payment information in Google's test environments. The test environment can be configured on both Android App and Web Integrations - refer to Google's [About the test environment](https://developers.google.com/pay/api/web/guides/test-and-deploy/integration-checklist#about-the-test-environment) documentation for more information.

The [Fat Zebra Sandbox environment](doc:endpoint-base-urls) will accept the non-chargeable payment information returned by the Google Pay API test environment.

All Google Pay transactions sent to the Fat Zebra API Sandbox environment will return cent-based responses, whereby the response code returned will be dependent on the amount specified in the request. E.g. for a request of $1.00, the Fat Zebra API will return a response code of "00" based on the cents of the amount. Similarly a request for $1.05 will return a response code of "05" declined. This allows you to test your integration against various response codes.

| Fat Zebra Environment | Google Pay Environment   |
| :-------------------- | :----------------------- |
| Sandbox               | `ENVIRONMENT_TEST`       |
| Production            | `ENVIRONMENT_PRODUCTION` |

# Additional Information

## Supported Authorization Methods

| Authorization Method |
| :------------------- |
| `PAN_ONLY`           |
| `CRYPTOGRAM_3DS`     |

## Supported Card Networks

| Card Network |
| :----------- |
| `AMEX`       |
| `JCB`        |
| `MASTERCARD` |
| `VISA`       |

## Billing Address Requirements

The Fat Zebra API does not require any billing address details to be sent. This is subject to change in the future.

# Limitations

> 🚧 Limited Acquirer Support For Recurring Transactions
> 
> Processing recurring transactions via Google Pay is not supported by all Australian acquirers. If these methods are used where support is not yet available the transactions may be declined or return errors.

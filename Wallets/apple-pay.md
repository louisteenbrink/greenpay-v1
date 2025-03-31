---
title: "Apple Pay"
slug: "apple-pay"
excerpt: "Accepting Apple Pay is faster than accepting traditional credit and debit cards and other payment methods. Customers no longer need to spend time searching for their wallet and finding the right card. Within apps or websites when using Safari, your customers can check out with a single touch."
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jul 18 2018 02:23:15 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Aug 10 2020 07:11:42 GMT+0000 (Coordinated Universal Time)"
---
# Apple Pay Checkout Workflow

- A customer adds a credit, debit, or prepaid card into their Apple Wallet app on their iPhone, iPad, Apple Watch or Mac.
- The customer chooses to Buy with Apple Pay on the merchants website or iOS app and only needs to then select their card and shipping address.
- The customer's card details are retrieved securely by Fat Zebra and your systems are not exposed to the PCI Scope for this data.

# Pre-requisites

## Apple Guidelines

Before starting your Apple Pay integration, please review Apple's documentation on how to prepare your app and/or website to support Apple Pay:

- [Planning For Apple Pay](https://developer.apple.com/apple-pay/planning/)
- [Apple Pay Acceptable Use Guidelines For Websites](https://developer.apple.com/apple-pay/acceptable-use-guidelines-for-websites/)
- [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/apple-pay/overview/introduction/)
- [Apple Sandbox Testing](https://developer.apple.com/apple-pay/sandbox-testing)

## Setup your Apple Merchant ID

An Apple Merchant ID is an identifier you register with Apple that uniquely identifies your business as a merchant able to accept payments.  
Follow the instructions in [Setup your Apple Merchant ID](setup-your-apple-merchant-id) for instructions to create this ID.

# Implementing Apple Pay in Apps

Apple provide a [sample Xcode app](https://developer.apple.com/library/archive/samplecode/Emporium/Introduction/Intro.html#//apple_ref/doc/uid/TP40016175-Intro) that implements Apple Pay that can be used for reference.

Please follow the [**official documentation from Apple for implementing Apple Pay in Apps**](https://developer.apple.com/documentation/passkit/apple_pay).

In summary, you will need to implement the following to support Apple Pay in your app, with some steps requiring configuration specific to Fat Zebra:

- [Enable Apple Pay in Xcode](https://help.apple.com/xcode/mac/9.3/#/deva43983eb7?sub=dev44ce8ef13)
- Determine if the device supports Apple Pay and whether the user has added payment cards using `PKPaymentAuthorizationController ` and `PKPaymentAuthorizationViewController `
- Provide a button that is used either to trigger payments through Apple Pay or to prompt the user to set up a card with `PKPaymentButton`
- Display a request for payment, including information about payment processing capabilities, the payment amount, and shipping information using `PKPaymentRequest`
- Handling the callback in `PKPaymentAuthorizationControllerDelegate` that is made when the user has authorized the payment, and calling the Fat Zebra API to [**create a purchase using a wallet**](https://docs.fatzebra.com/v1.0/reference#create-a-purchase-with-wallet)

# Implementing Apple Pay on the Web

Please follow the [**official documentation from Apple for implementing Apple Pay on the Web**](https://developer.apple.com/documentation/apple_pay_on_the_web).

Your implementation must meet the following pre-requisites as prescribed by Apple:

- Your website must comply with [Apple Pay on the Web: Acceptable Use Guidelines](https://developer.apple.com/apple-pay/acceptable-use-guidelines-for-websites/)
- All pages that include Apple Pay [must be served over HTTPS](https://developer.apple.com/documentation/apple_pay_on_the_web/setting_up_your_server)
- Your Apple Merchant ID must have a **Merchant Identity Certificate** (which you will request from Fat Zebra) upload to it in the Apple Developer Dashboard, see [Setup your Apple Merchant ID](https://docs.fatzebra.com/v1.0/docs/setup-your-apple-merchant-id) for instructions
- Any domains that will be used for Apple Pay transaction must be [registered and verified in the Apple Developer Dashboard](https://help.apple.com/developer-account/#/dev1731126fb)

Implementing the following to support Apple Pay on you website will require the following steps, with some steps requiring configuration specific to Fat Zebra:

- [Choose an API for Implementing Apple Pay on Your Website](https://developer.apple.com/documentation/apple_pay_on_the_web/choosing_an_api_for_implementing_apple_pay_on_your_website), as you have the option of using the [Apple Pay JS API](https://developer.apple.com/documentation/apple_pay_on_the_web/apple_pay_js_api) or the [W3C Payment Request API](https://developer.apple.com/documentation/apple_pay_on_the_web/payment_request_api)
- Determine if the device supports Apple Pay using [`window.ApplePaySession`](https://developer.apple.com/documentation/apple_pay_on_the_web/apple_pay_js_api/checking_for_apple_pay_availability)
- [Display an Apple Pay Button](https://developer.apple.com/documentation/apple_pay_on_the_web#2930449) on your website using CSS templates provided by Apple
- Create an [Apple Pay Session & provide it a payment request](https://developer.apple.com/documentation/apple_pay_on_the_web/apple_pay_js_api/creating_an_apple_pay_session)
- [Create an Apple Pay Session](https://developer.apple.com/documentation/apple_pay_on_the_web/apple_pay_js_api/creating_an_apple_pay_session) for your payment request
- Handle the [`onvalidatemerchant` event](https://developer.apple.com/documentation/apple_pay_on_the_web/apple_pay_js_api/providing_merchant_validation) and call your server passing it the URL from the event’s `validationURL` property. Your server will then need to call the Fat Zebra [Get Apple Pay Session](doc:get-apple-pay-session) endpoint. Your server will then receive an **opaque Apple Pay session object** from the Fat Zebra endpoint. This object needs to be passed onto your client side to call the Apple Pay Javascript SDK's `completeMerchantValidation` method.
- Once the user authorizes the payment, the `onpaymentauthorized` handler will be called on the `ApplePaySession`. This handler will contain a payment token encrypted by Apple using **Payment Processing Certificate**. In this event handler you can then call Fat Zebra API to [**create a purchase using a wallet**](https://docs.fatzebra.com/v1.0/reference#create-a-purchase-with-wallet), providing the payment token in the request payload

# Testing in the Fat Zebra Sandbox Environment

Apple provides a Sandbox environment which allows you to test your implementation of Apple Pay with test credit and debit cards. Documentation on setting up a Apple Sandbox tester account [https://developer.apple.com/apple-pay/sandbox-testing/]\(can be found here).

The Fat Zebra API Sandbox environment will accept these Apple test credit and debit cards. For more information on the URL's of the Fat Zebra API Sandbox environment, refer to [Endpoint Base URLs](doc:endpoint-base-urls).

All Apple Pay transactions sent to the Fat Zebra API Sandbox environment will return cent-based responses, whereby the response code returned will be dependent on the amount specified in the request. E.g. for a request of $1.00, the Fat Zebra API will return a response code of "00" based on the cents of the amount. Similarly a request for $1.05 will return a response code of "05" declined. This allows you to test your integration against various response codes.

# Limitations

> 🚧 Limited Acquirer Support For Recurring Transactions
> 
> Processing recurring transactions via Apple Pay is not supported by all Australian acquirers. If these methods are used where support is not yet available the transactions may be declined or return errors.

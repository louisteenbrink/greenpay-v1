---
title: "Setup your Apple Merchant ID"
slug: "setup-your-apple-merchant-id"
excerpt: ""
hidden: true
createdAt: "Mon Apr 01 2019 04:49:57 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 04 2024 01:23:20 GMT+0000 (Coordinated Universal Time)"
---
> 🚧 Note:
> 
> You can now onboard for Apple Pay (app and web) via your Merchant Dashboard - see [this page](https://docs.fatzebra.com/docs/apple-pay-onboarding-via-merchant-dashboard) for further details.

This article provides instructions detailing how to setup an Apple Merchant ID for Apple Pay.

An Apple Merchant ID is an identifier you register with Apple that uniquely identifies your business as a merchant able to accept payments. This ID never expires, and can be used in multiple websites and iOS apps and in multiple environments (testing and production).

# Request Merchant Identifier and Certificates from Fat Zebra

Contact your Fat Zebra account representative to get onboarded onto our Apple Pay integration. We will provide you with the following:

- A **Merchant Identifier** that you will need to setup your Apple Merchant ID
- A **Payment Processing Certificate** which you will need to add to the Apple Merchant ID you setup in the previous step. Apple will use this certificate to encrypt transaction data. This file will have a name ending with _-applepay.csr_.
- (_Apple Pay on the Web merchants only_) A **Merchant Identity Certificate** which you will need to upload to Apple when setting up your Apple Merchant IDs. Apple will use this certificate to authenticate your web sessions with the Apple Pay servers when using Apple Pay on the Web. This file will have a name ending with _-applepay-web.csr_.

# Create an Apple Merchant ID

1. Sign in to the [Apple Developer Dashboard](https://developer.apple.com/account/).
2. In _Certificates, Identifiers & Profiles_, choose **iOS, tvOS, watchOS** from the pop-up menu on the left.
3. Under _Identifiers_, select **Merchant IDs**, then in the upper-right corner, click the Add button (+).
4. Enter the merchant description and identifier name provided to you by your Fat Zebra Representative.
5. Review the settings, then click **Register**.
6. Click **Done**.

# Upload Your Payment Processing Certificate

1. Sign in to the [Apple Developer Dashboard](https://developer.apple.com/account/).
2. In _Certificates, Identifiers & Profiles_, choose **iOS, tvOS, watchOS** from the pop-up menu on the left.
3. Under _Identifiers_, select **Merchant IDs**, click on the Merchant ID that was setup in previous steps and then click **Edit**.
4. Under _Payment Processing Certificate_ click on **Create Certificate**.
5. Choose **No** for the question about processing in China, then click **Continue**.
6. Click **Continue**, then **Choose File**, and select the Payment Processing CSR file provided to you by Fat Zebra (ending in _-applepay.csr_), then click **Continue**.
7. On the _Your Certificate is Ready_ screen, click **Download** to save the generated certificate.
8. Send the generated certificate to your Fat Zebra account representative. Fat Zebra will load this certificate into our system, enabling your Apple Pay integration.

# Upload Your Merchant Identity Certificate

You will need to upload your Merchant Identity Certificate only if you plan to support Apple Pay on the Web.

1. Sign in to the [Apple Developer Dashboard](https://developer.apple.com/account/).
2. In _Certificates, Identifiers & Profiles_, choose **iOS, tvOS, watchOS** from the pop-up menu on the left.
3. Under _Identifiers_, select **Merchant IDs**, click on the Merchant ID that was setup in previous steps and then click **Edit**.
4. Scroll down to the **Apple Pay on the Web** section and click **Create Certificate** under the **Merchant Identity Certificate** section.
5. Click **Continue**, then **Choose File**, and select the Merchant Identity CSR file provided to you by Fat Zebra (ending in _-applepay-web.csr_), then click **Continue**.
6. On the **Your Certificate is Ready** screen, click **Download** to save the generated certificate.
7. Send the generated certificate to your Fat Zebra account representative. Fat Zebra will load this certificate into our system, enabling your Apple Pay integration.

# Verify Your Merchant Domain

You will need to verify your Merchant Domain with Apple only if you plan to support Apple Pay on the Web. You will need to verify domains for any website that you plan to implement Apple Pay on.

1. Sign in to the [Apple Developer Dashboard](https://developer.apple.com/account/).
2. In _Certificates, Identifiers & Profiles_, choose **iOS, tvOS, watchOS** from the pop-up menu on the left.
3. Under _Identifiers_, select **Merchant IDs**, click on the Merchant ID that was setup in previous steps and then click **Edit**.
4. Scroll down to the **Apple Pay on the Web** section and click **Add Domain** under the **Merchant Domains** section.
5. Enter the domain name. Please note that the domain must have a valid TLS certificate in place - an error will be returned if Apple cannot verify the certificate.
6. Click **Continue**.
7. Once the domain is registered you will be provided a link to download a verification file. Download this file make it accessible at the URL specified on the screen.
8. Depending on the domain specified you may need to Verify the domain, and retry this until the domain is successfully verified. Once verification is complete the file should not be deleted, as Apple periodically checks this.

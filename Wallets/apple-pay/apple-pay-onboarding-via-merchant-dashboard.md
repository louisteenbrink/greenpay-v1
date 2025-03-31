---
title: "Apple Pay Onboarding via Merchant Dashboard"
slug: "apple-pay-onboarding-via-merchant-dashboard"
excerpt: ""
hidden: false
createdAt: "Tue Apr 23 2024 02:02:26 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Nov 04 2024 01:23:10 GMT+0000 (Coordinated Universal Time)"
---
This article provides instructions detailing how to onboard for Apple Pay (app) and Apple Pay (web).

# Apple Pay (app)

1. Sign in to the Merchant Dashboard. In the sidebar, select Settings > Payment Methods.
2. Click 'Activate' for the Apple Pay wallet.
3. Agree to the terms of service.
4. The following will be generated for you:

- A **Merchant Identifier** that you will need to setup your Apple Merchant ID. An Apple Merchant ID is an identifier you register with Apple that uniquely identifies your business as a merchant able to accept payments. This ID never expires, and can be used in multiple websites and iOS apps and in multiple environments (testing and production).
- A **Payment Processing Certificate signing request** which you will use to generate a payment processing certificate. Apple will use this certificate to encrypt transaction data. This file will have a name ending with _-applepay.csr_.

5. Follow the steps in the section **Create an Apple Merchant ID ** below to register your merchant identifier in the Apple Developer Dashboard.
6. Follow the steps in the section **Generate your Payment Processing Certificate** below to generate your payment processing certificate (_apple_pay.cer_).
7. Upload your payment processing certificate (_apple_pay.cer_) in the Apple Pay wallet onboarding dialog.
8. On successful submission, the certificate will be loaded into our system enabling your Apple Pay integration.

# Apple Pay (web)

You will need to verify your merchant domain(s) with Apple if you plan to support Apple Pay on the Web. You will need to add domains for any website that you plan to implement Apple Pay on.

1. Sign in to the Merchant Dashboard. In the sidebar, select Settings > Payment Methods.
2. Click 'Activate' for the Apple Pay (web) wallet.
3. Follow the directions in the dialog to add your domain. Our system will record that domain in the database, and then send a request to Apple to register and verify it. Apple will try to retrieve the domain verification file from the domain that was provided, and verify the value in the file matches the value they set against our Gateway identity. 
4. After the first domain has been successfully added, your Apple Pay (web) wallet should be activated. You can add more domains by clicking on 'Add Domain'.

# Appendix

## Create an Apple Merchant ID

1. Sign in to the [Apple Developer Dashboard](https://developer.apple.com/account/).
2. In _Certificates, Identifiers & Profiles_, choose **iOS, tvOS, watchOS** from the pop-up menu on the left.
3. Under _Identifiers_, select **Merchant IDs**, then in the upper-right corner, click the Add button (+).
4. Enter the merchant description and identifier name provided to you by your Fat Zebra Representative.
5. Review the settings, then click **Register**.
6. Click **Done**.

## Generate your Payment Processing Certificate

1. Sign in to the [Apple Developer Dashboard](https://developer.apple.com/account/).
2. In _Certificates, Identifiers & Profiles_, choose **iOS, tvOS, watchOS** from the pop-up menu on the left.
3. Under _Identifiers_, select **Merchant IDs**, click on the Merchant ID that was setup in previous steps and then click **Edit**.
4. Under _Payment Processing Certificate_ click on **Create Certificate**.
5. Choose **No** for the question about processing in China, then click **Continue**.
6. Click **Continue**, then **Choose File**, and select the Payment Processing CSR file provided to you by Fat Zebra (ending in _-applepay.csr_), then click **Continue**.
7. On the _Your Certificate is Ready_ screen, click **Download** to save the generated certificate.

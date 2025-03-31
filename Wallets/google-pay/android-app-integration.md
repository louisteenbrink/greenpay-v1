---
title: "Android App Integration"
slug: "android-app-integration"
excerpt: "Instructions detailing how to integrate Google Pay™ into an Android App using Fat Zebra as your gateway"
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri May 24 2019 03:27:16 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 20:30:53 GMT+0000 (Coordinated Universal Time)"
---
# Pre-requisites

1. Read the [Google Pay Android Brand Guidelines](https://developers.google.com/pay/api/android/guides/brand-guidelines)
2. Follow Google Pay's [Deploy production environment guidelines](https://developers.google.com/pay/api/web/guides/test-and-deploy/deploy-production-environment). In this step you will obtain a **merchantID**. By integrating Google Pay, you agree to Google's [terms of service](https://payments.developers.google.com/terms/sellertos).
3. Contact the [Fat Zebra support team](mailto:support@fatzebra.com) to have Google Pay enabled on your account. You will be supplied a **gatewayMerchantID**. 

# Implementation Steps

Follow the instructions in the following Google guides to implement a Google Pay button in your app:

- [Google Pay Android developer documentation](https://developers.google.com/pay/api/android/)
- [Google Pay Android integration checklist](https://developers.google.com/pay/api/android/guides/test-and-deploy/integration-checklist)

When setting up the _tokenizationSpecification_ object, specify the following values for the **gateway** and **gatewayMerchantId** values:

```java
private static JSONObject getTokenizationSpecification() {
  JSONObject tokenizationSpecification = new JSONObject();
  tokenizationSpecification.put("type", "PAYMENT_GATEWAY");
  tokenizationSpecification.put(
      "parameters",
      new JSONObject()
          .put("gateway", "fatzebra")
          .put("gatewayMerchantId", "<provided to you by Fat Zebra>"));

  return tokenizationSpecification;
}
```

The Google Pay button will generate an encrypted token that you must then include in a request to the Fat Zebra API to:

- Create a purchase using the card in the Google Pay payload
- Or tokenize the card details in the Google Pay payload

The following documentation outlines the format of the two API calls:

- [Create a purchase using a wallet](ref:create-a-purchase-with-wallet)
- [Tokenize a card with wallet credentials](ref:tokenize-a-card-with-wallet-credentials)

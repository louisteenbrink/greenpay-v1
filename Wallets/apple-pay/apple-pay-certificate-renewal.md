---
title: "Apple Pay (app) Certificate Renewal"
slug: "apple-pay-certificate-renewal"
excerpt: ""
hidden: false
createdAt: "Sat Dec 28 2024 02:12:31 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Feb 04 2025 00:37:18 GMT+0000 (Coordinated Universal Time)"
---
This article provides instructions detailing how to renew your Apple Pay (app) certificate.

## Loading your new certificate

1. In your **Merchant Dashboard**, select _Settings_ > _Payment Methods_. In the _Apple Pay_ section, your certificate should be marked as "Expiring" or "Expired" and you should see an option to "Generate New Certificate".

   ![](https://files.readme.io/a7c37988fdbe68c375c6c2dc6766a891abc142e5c2f94b13b68cf5c243c0c702-image.png)

   1. Click "Generate New Certificate" and download the .csr file from the dialog. Note the merchant identifier shown in the dialog.  
      ![](https://files.readme.io/cccac847dfeac12785b785f6c907fe405d96707ae0b096f3af1b6df8c2cd34de-image.png)

2. In your **Apple Developer Dashboard**, view the details for the merchant identifier displayed in step 2. 

   1. In the _Apple Pay Payment Processing Certificate_ section for this identifier, select "Create Certificate", then follow the steps to create a new certificate uploading the .csr file downloaded in step 2 when asked. 
   2. Download the apple_pay.cer file for the newly created certificate.  
      ![](https://files.readme.io/8fe9f4dbb92783c514ffd490199658faeb2f840d6d983bc4516d9df8e475ad87-image.png)

3. Back in your **Merchant Dashboard**, upload the apple_pay.cer file generated from step 2.  
   ![](https://files.readme.io/79d1d894c6d9024df953f9f7a525d20ccc63859bfed6446f7046f3fe317c9a38-image.png)

4. Your certificate should now be loaded in the system but will not yet be active. Apple Pay (app) transaction processing will continue against the expiring/expired certificate.

   ![](https://files.readme.io/03c2c4e52c7d521c38eef1f730a552d51ca3b961f4bbe38e5d4503524978d006-image.png)

<br />

## Activating your new certificate

Complete the following steps when you are ready to activate your new certificate.

1. In your **Apple Developer Dashboard**, activate the new certificate.

   ![](https://files.readme.io/28e16474ae5d52d8c84ad68f29f6a002a7f8f73f2614d16403a51af226b1c427-image.png)

2. In your **Merchant Dashboard**, click the small "Play" button next to the new certificate on the Payment Methods page.  
     ![](https://files.readme.io/e700b7b2966030eab5f2dc5dc73df03e75fa2b32b2ba0247f15ad7a468eee01e-image.png)

   1. Click "Activate" in the next dialog.  
      ![](https://files.readme.io/bf233b6c00665f12f2d0191b69fe969375bea7c183d1713894bdc4e4c06d1ec6-image.png)

   2. The new certificate should now display as Active and will be used for Apple Pay (app) transaction processing.  
      ![](https://files.readme.io/8911b422e8f91b91a8b9dff6685fb79ceae251f0c7112cab78283bcf9f83f230-image.png)

3. Attempt a handful of Apple Pay transactions within your mobile app to test the new certificate immediately after activation and again in a couple of hours.

---
title: "Overview"
slug: "3ds2-overview"
excerpt: "3DS2 allows you to authenticate your transactions to reduce fraud and shift liability"
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Sep 07 2020 01:03:05 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Sep 30 2020 04:18:33 GMT+0000 (Coordinated Universal Time)"
---
3DS2 is a payments industry standard that promotes secure, frictionless consumer authentication for online payments. 3DS2 allows you to reduce fraud by providing methods to verify the authenticity of online payments.

The steps required to implement 3DS2 using Fat Zebra will depend on:

1. If you have already have an MPI (Merchant Plug-in) or require Fat Zebra to act as your MPI
2. Your PCI level
3. Your preferred integration method

# MPI

### I already have an MPI

If you have an existing MPI integration you will need to follow your MPI's instructions in order to authenticate a payment transaction. After authentication your MPI will provide you with 3DS data which may include:

- Cryptogram, CAV, CAVV or AAV
- Ecommerce Indicator (ECI) or Security Level Indicator (SLI)
- PARes
- VERes

You will then need to set the [3D Secure fields](doc:3d-secure) on your Fat Zebra Purchase or Refund API calls in order to complete a 3DS2 transaction.

### I don't have an MPI

Fat Zebra can act as your MPI. Please contact your Fat Zebra representative for more information on how to add Fat Zebra's 3DS2 MPI to your account.

Using Fat Zebra's MPI, there are various integration methods to choose from depending on your PCI level:

[block:parameters]
{
  "data": {
    "h-0": "Integration Method",
    "h-1": "Description",
    "h-2": "3DS Integration Guide",
    "0-0": "Hosted Payments Page",
    "0-1": "**PCI SAQ A required**  \n  \nYour website uses Fat Zebra’s payment form through the Fat Zebra Hosted Payments Page iframe.  \n  \nPayment processing is entirely outsourced to FatZebra, meaning you do not need to handle any raw card data.",
    "0-2": "[Using Hosted Payments Page](doc:using-hosted-payments-page)",
    "1-0": "Direct Post",
    "1-1": "**PCI A-EP required**  \n  \nYour website hosts the payment form and you are responsible for collecting card details on front end code you host.  \n  \nCard data exchange with Fat Zebra will take place via an AJAX call from your frontend directly to Fat Zebra.",
    "1-2": "[Using Custom Payments Form](doc:using-custom-payments-form)",
    "2-0": "API",
    "2-1": "**PCI SAQ D required**  \n  \nYour website hosts the payment form and you are responsible for collecting card details in both your backend and frontend.  \n  \nCard data exchange with Fat Zebra will take place via API calls from your backend system to Fat Zebra.",
    "2-2": "[Using Custom Payments Form](doc:using-custom-payments-form)"
  },
  "cols": 3,
  "rows": 3,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

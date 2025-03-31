---
title: "SCA"
slug: "sca"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Jul 24 2020 01:50:49 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Jul 13 2023 09:04:28 GMT+0000 (Coordinated Universal Time)"
---
[block:parameters]
{
  "data": {
    "h-0": "Event",
    "h-1": "Description",
    "h-2": "Applicable Methods",
    "0-0": "`fz.sca.success`",
    "0-1": "Emitted when 3DS validation completes successfully.  \n  \nThe liability shifts from merchant to the card issuer.  \n  \nPlease note: The edge case is when the enrolled field (ver) comes back as 'N' (3DS success - Not Enrolled), which means \"No, Bank is not participating in 3-D Secure protocol\". If the Enrolled value is equal to N, then the Consumer is NOT eligible for Authentication (No liability shift).  \n  \nMost merchants choose to continue with these transactions, because otherwise in many cases it would be stopping customers from making legitimate transactions.",
    "0-2": "[renderPaymentsPage](doc:renderpaymentspage)  \n[verifyCard](https://docs.fatzebra.com/docs/verifycard)",
    "1-0": "`fz.sca.error`",
    "1-1": "Emitted when 3DS enrolment or validation failed.  \n  \nThe payment attempt is deemed risky and merchant shall not proceed with the payment.",
    "1-2": "[renderPaymentsPage](doc:renderpaymentspage)  \n[verifyCard](https://docs.fatzebra.com/docs/verifycard)"
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


## fz.sca.success Data Payload

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`aav`",
    "0-1": "string",
    "0-2": "Account Authentication Value. Unique 32-character transaction token for a 3D Secure transaction. For Mastercard Identity Check, the AAV is named the UCAF. For Visa Secure, the AAV is named the CAVV.",
    "1-0": "`cavv`",
    "1-1": "string",
    "1-2": "Cardholder Authentication Verification Value. A Base64-encoded string sent back with Visa Secure-enrolled cards that specifically identifies the transaction with the issuing bank and Visa. Standard for collecting and sending AAV data for Visa Secure transactions.",
    "2-0": "`par`",
    "2-1": "string",
    "2-2": "Payer Authentication Response. Compressed, Base64-encoded response from the card-issuing bank",
    "3-0": "`sli`",
    "3-1": "string",
    "3-2": "The Security Level Indicator for 3DS transactions",
    "4-0": "`xid`",
    "4-1": "string",
    "4-2": "String used by both Visa and Mastercard which identifies a specific transaction on the Directory Servers. This string value should remain consistent throughout a transaction’s history.",
    "5-0": "`ucaf`",
    "5-1": "string",
    "5-2": "Universal Cardholder Authentication Field.  \n  \nMastercard only.",
    "6-0": "`ver`",
    "6-1": "string",
    "6-2": "3DS enrolment status.",
    "7-0": "`directoryServerTxnId`",
    "7-1": "string",
    "7-2": "Directory server transaction Id",
    "8-0": "`threedsVersion`",
    "8-1": "string",
    "8-2": "3DS version used for verifying the intended payment."
  },
  "cols": 3,
  "rows": 9,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


```json fz.sca.success data payload
{
  message: "xxx",
  data: {
    aav: "xxx",
    cavv: "xxx",
    par: "xxx",
    sli: "xxx",
    xid: "xxx",
    ucaf: "xxx",
    ver: "xxx",
    directoryServerTxnId: "xxx",
    threedsVersion: "xxx",
  }
}
```

## fz.sca.error Data Payload

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`errorCode`",
    "0-1": "string",
    "0-2": "Error code for specific 3DS/SCA failure scenario.  \n  \nerrorCode will be not be present in the event of request timeout or server error  \n  \nSee below for error code mapping."
  },
  "cols": 3,
  "rows": 1,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


```json fz.sca.error data payload
// Request timeout, server error, etc. Prompt user to retry.
{
  errors: ["xxx"],
  data: null
}

// 3DS2 authentication failed. The card is deemed risky by issuer.
{
  errors: ["xxx"],
  data: {
    errorCode: "xxx"
  }
}
```

## 3DS/SCA Error Code Mapping

[block:parameters]
{
  "data": {
    "h-0": "Error Code",
    "h-1": "Description",
    "0-0": "`001`",
    "0-1": "**Bypassed authentication**  \nThis is related to a feature that is **currently not available**. We will look at providing merchants the ability to configure rules to determine whether authentication is required for a transaction.  \n--  \nNo liability shift",
    "1-0": "`002`",
    "1-1": "**Authentication not available on lookup**  \nUnable to verify 3DS enrolment status with the issuer.  \n--  \nNo liability shift",
    "2-0": "`003`",
    "2-1": "**Unavailable frictionless authentication**  \n3DS authentication is unavailable with the issuer.  \n--  \nNo liability shift",
    "3-0": "`004`",
    "3-1": "**Unsuccessful frictionless authentication**  \nThe issuer deems the transaction as risky  \n--  \nNo liability shift",
    "4-0": "`005`",
    "4-1": "**Rejected frictionless authentication**  \n  \n--  \nNo liability shift",
    "5-0": "`006`",
    "5-1": "**Unsuccessful step-up authentication**  \nUnsuccessful authentication due to  failed OTP (one time password) challenge.  \n--  \nNo liability shift",
    "6-0": "`007`",
    "6-1": "**Unavailable step-up authentication**  \nThe card holder is enrolled for 3DS, but authentication is not available with that issuer.  \n--  \nNo liability shift"
  },
  "cols": 2,
  "rows": 7,
  "align": [
    "left",
    "left"
  ]
}
[/block]

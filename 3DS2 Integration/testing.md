---
title: "Testing"
slug: "testing"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Sun Sep 06 2020 23:06:49 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Aug 28 2023 02:17:31 GMT+0000 (Coordinated Universal Time)"
---
A 3DS check may end up with one of the following outcomes.

- 3DS check successful  
  `fz.sca.success` event is triggered by fatzebra.js.  If you own your own payments form and use the `verifyCard` method of fatzebra.js to perform 3DS checks, 3DS result data will be provided in the `fz.sca.success` event payload. Using this 3DS result data in your Purchase or Refund API call will qualify that transaction for liability shift.

- Please note: The edge case is when the enrolled field (ver) comes back as 'N' (3DS success - Not Enrolled), which means "No, Bank is not participating in 3-D Secure protocol". If the Enrolled value is equal to N, then the Consumer is NOT eligible for Authentication (No liability shift).

- 3DS check unsuccessful  
  `fz.sca.error` event is triggered by fatzebra.js.  An [error code](doc:sca#3dssca-error-code-mapping) will be returned in the event payload indicating the reason for the error. This could be due to the card issuer not support 3DS2 or if the cardholder was unable to verify their card when prompted with a 3DS challenge flow (e.g. they entered the wrong one-time pin that was sent to their mobile device). 

- Server Error or timeout.  
  `fz.sca.error` event is triggered by fatzebra.js. No error code will be returned in the event payload. In this event we recommend that you prompt your users to retry the 3DS check/payment.

# Test cards

FatZebra provides a number of test cards to simulate various 3DS scenarios in the Sandbox environment. Each of the following card numbers will simulate a predetermined outcome:

## Successful 3DS2 check

[block:parameters]
{
  "data": {
    "h-0": "Scenario",
    "h-1": "Cards",
    "0-0": "**Successful frictionless authentication**  \nCardholder being authenticated by their Card Issuer  \n--  \nLiability shift",
    "0-1": "Visa: 4000000000001000  \nMastercard: 5200000000001005  \nAmex: 340000000001007",
    "1-0": "**Attempts processing frictionless authentication**  \nCardholder is enrolled in 3DS however the Issuer is not supporting the program, resulting in a stand-in authentication experience  \n--  \nLiability shift",
    "1-1": "Visa: 4000000000001026  \nMastercard: 5200000000001021  \nAmex: 340000000001023",
    "2-0": "**Successful step-up authentication**  \nSuccessful OTP challenge  \n--  \nLiability shift",
    "2-1": "Visa: 4000000000001091  \nMastercard: 5200000000001096  \nAmex: 340000000001098"
  },
  "cols": 2,
  "rows": 3,
  "align": [
    "left",
    "left"
  ]
}
[/block]


**fz.sca.success** sample payload

```json
{
  "message": "FatZebra.3DS: 3DS success - Successful Frictionless Authentication",
  "data": {
    "cavv": "xxx",
    "par": "xxx",
    "sli": "xxx",
    "xid": "xxx",
    "ver": "xxx",
    "directoryServerTxnId": "xxx",
    "threedsVersion": "xxx" 
  }
}
```

## Unsuccessful 3DS check

[block:parameters]
{
  "data": {
    "h-0": "Scenario",
    "h-1": "Card",
    "h-2": "Error code",
    "0-0": "**Unsuccessful enrolment check**  \nEnrolment failed by card issuer  \n--  \nNo liability shift",
    "0-1": "Visa:  \n4000000000002446  \nMastercard:  \n5200000000002037  \nAmex:  \n340000000002732",
    "0-2": "002",
    "1-0": "**Unsuccessful frictionless authentication**  \nAuthentication failed by card issuer without challenge  \n--  \nNo liability shift",
    "1-1": "Visa: 4000000000001018  \nMastercard: 5200000000001013  \nAmex: 340000000001015",
    "1-2": "004",
    "2-0": "**Unavailable frictionless authentication**  \nAuthentication is unavailable from the issuer at the current time.  \n--  \nNo liability shift",
    "2-1": "Visa: 4000000000001034  \nMastercard: 5200000000001039  \nAmex: 340000000001031",
    "2-2": "003",
    "3-0": "**Rejected frictionless authentication**  \nAuthentication rejected by the issuer.  \n--  \nNo liability shift",
    "3-1": "Visa: 4000000000001042  \nMastercard: 5200000000001047  \nAmex: 340000000001049",
    "3-2": "005",
    "4-0": "**Authentication not available on lookup**  \nUnable to verify 3DS enrolment status with the issuer due to system error.  \n--  \nNo liability shift",
    "4-1": "Visa: 4000000000001059  \nMastercard: 5200000000001054  \nAmex: 340000000001056",
    "4-2": "002",
    "5-0": "**Server Error**  \n--  \nNo liability shift",
    "5-1": "Visa: 4000000000001067  \nMastercard: 5200000000001062  \nAmex: 340000000001064",
    "5-2": "-",
    "6-0": "**Timeout**  \n--  \nNo liability shift",
    "6-1": "Visa: 4000000000001075  \nMastercard: 5200000000001070  \nAmex: 340000000001072",
    "6-2": "-",
    "7-0": "**Bypassed authentication**  \nThis is related to a feature that is **currently not available**. We will look at providing merchants the ability to configure rules to determine whether authentication is required for a transaction.  \n--  \nNo liability shift",
    "7-1": "Visa: 4000000000001083  \nMastercard: 5200000000001088  \nAmex: 340000000001080",
    "7-2": "001",
    "8-0": "**Unsuccessful step-up authentication**  \nUnsuccessful authentication due to  failed OTP (one time password) challenge.  \n--  \nNo liability shift",
    "8-1": "Visa: 4000000000001109  \nMastercard: 5200000000001104  \nAmex: 340000000001106",
    "8-2": "006",
    "9-0": "**Unavailable step-up authentication**  \nThe card holder is enrolled for 3DS, but authentication is not available with that issuer.  \n--  \nNo liability shift",
    "9-1": "Visa: 4000000000001117  \nMastercard: 5200000000001112  \nAmex: 340000000001114",
    "9-2": "007"
  },
  "cols": 3,
  "rows": 10,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


**fz.sca.error** sample payload

```json fz.sca.error
{
  "errors": [
    "FatZebra.3DS: 3DS error - Rejected Frictionless Authentication"
  ],
  "data": {
    "errorCode": "005" 
  }
}
```

---
title: "Create a purchase using a wallet"
slug: "create-a-purchase-with-wallet"
excerpt: ""
hidden: false
createdAt: "Fri Sep 07 2018 02:14:08 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Jul 16 2024 02:05:56 GMT+0000 (Coordinated Universal Time)"
---
## The wallet request object

The credentials required to make payments with a particular wallet provider vary according to the provider used. The `type` field in the wallet object determines which provider syntax is used. Currently supported wallets are:

- Apple Pay
- Google Pay

### Apple Pay

| Field               | Type                                                                                              | Description                                                                                                                                                                                                         |
| :------------------ | :------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `type`              | String. For Apple Pay, the value will be `APPLE`, or `APPLEPAYWEB` if using Apple Pay on the Web. | Wallet provider identifier                                                                                                                                                                                          |
| `token`             | Object                                                                                            |                                                                                                                                                                                                                     |
| `token.paymentData` | Object                                                                                            | Data format is specified by the latest [Apple Pay documentation](https://developer.apple.com/library/archive/documentation/PassKit/Reference/PaymentTokenJSON/PaymentTokenJSON.html#//apple_ref/doc/uid/TP40014929) |

## Google Pay

| Field   | Type                                               | Description                                                                                                                                                                           |
| :------ | :------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `type`  | String. For Google Pay, the value will be `GOOGLE` | Wallet provider identifier                                                                                                                                                            |
| `token` | Object                                             | Set this field to the object provided by the Google Pay API. This object will contains fields including `intermediateSigningKey`, `protocolVersion`, `signature`, and `signedMessage` |

---
title: "Create a purchase using a wallet passthrough"
slug: "create-a-purchase-using-wallet-passthrough"
excerpt: ""
hidden: true
createdAt: "Wed Jan 22 2025 22:20:56 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jan 22 2025 23:51:00 GMT+0000 (Coordinated Universal Time)"
---
## The wallet passthrough object

This payload allows a vaulted wallet credential to be decryped and passed to FatZebra to be used for transactions. Currently supported passthrough wallets are ApplePay and GooglePay.

The wallet object should be supplied, including the wallet type and cryptogram, to ensure the correct switch settings are applied. The card and transactions details should be applied using the decrypted wallet details.

The wallet object for a passthrough transaction **must** contain:

- type, currently supported values:
  - `passthrough_apple_pay` for ApplePay wallets
  - `passthrough_google_pay` for GooglePay wallets
- Cryptogram - decrypted from the wallet

Other fields may be applied as per standard purchase field.

<br />

> 🚧 BIN blocking based on county of origin will not be performed when using network token passthrough.
> 
> As the underlying instrument is not provided, and the network token submitted may have been generated with a BIN that corresponds to a foreign institution, BIN blocking can not be applied to transactions using network token passthrough.

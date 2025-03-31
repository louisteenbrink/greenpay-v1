---
title: "Create a purchase using a network token passthrough"
slug: "create-a-purchase-using-token-passthough"
excerpt: ""
hidden: false
createdAt: "Mon Apr 22 2024 23:52:51 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Aug 23 2024 01:06:00 GMT+0000 (Coordinated Universal Time)"
---
## The cryptogram object

Using a scheme token to transact a cryptogram must be provided for the first transaction.

Subsequent transactions may provide the cryptogram if required.

Fatzebra will save the the scheme token as a standard credit card record with a Fatzebra token, with a wallet type of 'Passthrough token'. Using the returned Fatzebra token, the cryptogram may be passed in.

> 🚧 BIN blocking based on county of origin will not be performed when using network token passthrough.
> 
> As the underlying instrument is not provided, and the network token submitted may have been generated with a BIN that corresponds to a foreign institution, BIN blocking can not be applied to transactions using network token passthrough.

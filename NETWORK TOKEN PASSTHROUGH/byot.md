---
title: "Bring Your Own Network Token"
slug: "byot"
excerpt: "FatZebra allows the use of network tokens for Mastercard or Visa through the MDES and VTS program."
hidden: false
createdAt: "Fri May 10 2024 06:01:25 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Aug 23 2024 01:08:13 GMT+0000 (Coordinated Universal Time)"
---
Merchants may wish to perform network tokenisation of their own cards to manage lifecycle events of these cards. FatZebra allows the presentment of network tokens with the cryptogram, passing these through to the switch.

By supplying a network token as the card number, the token expiry as the card expiry and the network provided cryptogram in the cryptogram field, FatZebra will mark the card as being a provided network token.

All other fields are applicable as for a regular purchase.

```Text json
{
  "card_number": "55555555555555555",
  "card_holder": "Valued Cardholder",
  "card_expiry": "02/2027",
  "customer_ip": "127.0.0.1",
  "amount": 110,
  "currency": "AUD"
  "cryptogram": "Aaaaaa111112222223333344444=="
}
```

All subsequent transactions, either using the network token as the card number or the returned FatZebra token card will be treated as a network token transaction.

The cryptogram should be fetched as per rules for the network token - through either VTS or MDES.

On subsequent transactions, if the cryptogram is not present, it will be omitted. This is **not** recommended; some transactions are eligible to have the cryptogram omitted - for instance merchant initiated transactions that are recurring - however they may be declined by the issuer.

---
title: "Card Account events"
slug: "card-account-events"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jul 06 2023 00:59:26 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Jul 06 2023 04:27:25 GMT+0000 (Coordinated Universal Time)"
---
For merchants taking advantage of network tokens, this webhook will fire when:

- a change has occurred to a card-on-file. For example, when a card's expiry date has been updated, merchants will receive an update event with the new expiry date;
- the scheme token status is updated.

The network token status will be one of the following values:

[block:parameters]
{
  "data": {
    "h-0": "Status",
    "h-1": "Description",
    "0-0": "pending",
    "0-1": "This card has been enrolled for network tokenisation but has not yet had its token activated.  \n  \nAny transactions attempted with a card in this state will fall back to the original PAN.",
    "1-0": "active",
    "1-1": "This card has an active network token. When transacting with a card in this state, a digital PAN and corresponding cryptographic signature will be fetched and used for the transaction.  \n  \nIf there are errors when fetching the payment instrument (for instance due to service interruptions), the transaction will fall back to the original PAN.",
    "2-0": "suspended",
    "2-1": "This card has a network token, however the token has been suspended by either the network or issuing bank. A card that is suspended may return to the active state, or it may be deleted.  \n  \nAny transactions attempted with a card in this state will fall back to the original PAN.",
    "3-0": "deleted",
    "3-1": "This card has had its network token deleted, possibly due to account closure or some other reason. Merchants should attempt to contact the card holder for an updated payment method.  \n  \nAny transactions attempted with a card in this state will fall back to the original PAN."
  },
  "cols": 2,
  "rows": 4,
  "align": [
    "left",
    "left"
  ]
}
[/block]


```json card_account:update
{  
  "event": "card_account:update",
  "payload": {
    "token": "abcd1234abcd",
    "card_number": "555555XXXXXX1243",
    "card_expiry": "2021-09-30",
    "card_type": "MasterCard",
    "card_category": "Credit",
    "card_updater_status": "active"
  }
}
```

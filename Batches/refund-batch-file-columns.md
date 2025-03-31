---
title: "Refund Batch File Columns"
slug: "refund-batch-file-columns"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Mar 01 2019 01:21:51 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Mar 01 2019 01:32:27 GMT+0000 (Coordinated Universal Time)"
---
[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Example Value",
    "h-2": "Description",
    "0-0": "Amount",
    "0-1": "10050  \nInteger  \nRequired",
    "0-2": "The amount of the transaction to be processed.  \nThis is an integer in the smallest units for the currency (i.e. $100.50 will be 10050).",
    "1-0": "Currency",
    "1-1": "AUD  \nString (3 characters)  \nRequired",
    "1-2": "The ISO Currency code for the transaction.",
    "2-0": "Reference",
    "2-1": "INV-1234  \nString (100 characters)  \nRequired",
    "2-2": "The merchant reference for the transaction. This must be unique.  \nIt is recommended that this is alphanumeric only with the exception of hyphen (-) and underscore (\\_).",
    "3-0": "Card Holder",
    "3-1": "Max Smith  \nString (50 characters)  \nRequired unless Token or Purchase ID is present",
    "3-2": "The card holder's name.",
    "4-0": "Card Number",
    "4-1": "4444333322221111  \nString (19 characters)  \nRequired unless Token or Purchase ID is present",
    "4-2": "The card number.",
    "5-0": "Card Expiry",
    "5-1": "09/2023  \nDate (mm/yyyy)  \nRequired unless Token or Purchase ID is present",
    "5-2": "The card expiry date in mm/yyyy format.",
    "6-0": "Token",
    "6-1": "a348jki  \nString (20 characters)  \nRequired unless Purchase ID is present or unless Card Holder, Card Number and Card Expiry are present.",
    "6-2": "The card token to be used in place of Card Holder, Card Number and Card Expiry.  \nThis column takes priority over the other card detail columns.",
    "7-0": "Description",
    "7-1": "Invoice for EOFY accounts  \nString (255 characters)  \nOptional",
    "7-2": "The description for the transaction.",
    "8-0": "Purchase ID",
    "8-1": "071-P-ABCD1234  \nString (15 characters)  \nRequired unless Token is present or unless Card Holder, Card Number and Card Expiry are present.",
    "8-2": "If refunding a previous purchase, this is the ID of the purchase that should be refunded."
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

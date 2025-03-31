---
title: "Purchase Batch File Columns"
slug: "purchase-batch-specification"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon May 14 2018 00:51:06 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sat Sep 29 2018 09:12:11 GMT+0000 (Coordinated Universal Time)"
---
[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Example Value",
    "h-2": "Description",
    "0-0": "Amount",
    "0-1": "10050  \n  \nInteger  \nRequired",
    "0-2": "The amount of the transaction to be processed.  \nThis is an integer in the smallest units for the currency (i.e. $100.50 will be 10050)",
    "1-0": "Currency",
    "1-1": "AUD  \n  \nString (3 characters)  \nRequired",
    "1-2": "The ISO Currency code for the transaction.",
    "2-0": "Reference",
    "2-1": "INV-1234  \n  \nString (100 characters)  \nRequired",
    "2-2": "The merchant reference for the transaction. This must be unique.  \nIt is recommended that this is alphanumeric only with the exception of hyphen (-) and underscore (\\_)",
    "3-0": "Card Holder",
    "3-1": "Max Smith  \n  \nString (50 characters)  \nRequired unless Token is present",
    "3-2": "The card holder's name.",
    "4-0": "Card Number",
    "4-1": "4444333322221111  \n  \nString (19 characters)  \nRequired unless Token is present",
    "4-2": "The card number.",
    "5-0": "Card Expiry",
    "5-1": "09/2023  \n  \nDate (mm/yyyy)  \nRequired unless Token is present",
    "5-2": "The card expiry date in mm/yyyy format.",
    "6-0": "Token",
    "6-1": "a348jki  \n  \nString (20 characters)  \nRequired unless Card Holder, Card Number and Card Expiry are present.",
    "6-2": "The card token to be used in place of Card Holder, Card Number and Card Expiry.  \nThis column takes priority over the other card detail columns.",
    "7-0": "Description",
    "7-1": "Invoice for EOFY accounts  \n  \nString (255 characters)  \nOptional",
    "7-2": "The description for the transaction."
  },
  "cols": 3,
  "rows": 8,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

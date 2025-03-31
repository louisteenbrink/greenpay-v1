---
title: "Result Files"
slug: "result-files"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon May 14 2018 01:59:01 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Mar 01 2019 01:21:20 GMT+0000 (Coordinated Universal Time)"
---
## Result File Contents

Upon completion of a batch the result file can be retrieved to be ingested into other systems.

## Result file contents for PURCHASE/REFUND batches

[block:parameters]
{
  "data": {
    "h-0": "Column Name",
    "h-1": "Example Value",
    "h-2": "Description",
    "0-0": "Reference",
    "0-1": "INV-1234  \n  \nString (100 characters)",
    "0-2": "The merchant reference for the transaction.",
    "1-0": "Transaction ID",
    "1-1": "071-P-ABCD1234A  \n  \nString",
    "1-2": "The gateway transaction ID.",
    "2-0": "Result",
    "2-1": "Approved  \n  \nString",
    "2-2": "Whether the transaction was Approved or Declined.",
    "3-0": "Response Code",
    "3-1": "08  \n  \nString (2 digits)",
    "3-2": "The bank response code.",
    "4-0": "Message",
    "4-1": "Approved  \n  \nString",
    "4-2": "The message for the bank response code.",
    "5-0": "Authorization ID",
    "5-1": "983423  \n  \nString (6 digits)",
    "5-2": "The transaction authorisation ID.",
    "6-0": "RRN",
    "6-1": "348723409134  \n  \nString (12 digits)",
    "6-2": "The transaction reference retrieval number (RRN, also known as receipt number).",
    "7-0": "Amount",
    "7-1": "10050  \n  \nNumeric",
    "7-2": "The transaction amount.",
    "8-0": "Currency",
    "8-1": "AUD  \n  \nString (3 characters)",
    "8-2": "The ISO Currency code for the transaction.",
    "9-0": "Card Holder",
    "9-1": "Max Smith  \n  \nString (18 characters)",
    "9-2": "The card holder's name.",
    "10-0": "Card Number",
    "10-1": "444433XXXXXX1111  \n  \nString (19 characters)",
    "10-2": "The masked card number for the transaction.",
    "11-0": "Card Expiry",
    "11-1": "09/2023  \n  \nDate (mm/yyyy)",
    "11-2": "The card expiry date in mm/yyyy format.",
    "12-0": "Token",
    "12-1": "jksh328h  \n  \nString (20 characters)",
    "12-2": "The card token to be used in place of Card Holder, Card Number and Card Expiry.",
    "13-0": "Description",
    "13-1": "Invoice INV-1234  \n  \nString (32 characters)",
    "13-2": "The description for the transaction."
  },
  "cols": 3,
  "rows": 14,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


## Result file contents for DIRECTDEBIT batch

[block:parameters]
{
  "data": {
    "h-0": "Column Name",
    "h-1": "Example Value",
    "h-2": "Description",
    "0-0": "Reference",
    "0-1": "INV-1234  \n  \nString (100 characters)",
    "0-2": "The merchant reference for the transaction.",
    "1-0": "Transaction ID",
    "1-1": "071-DD-ABCD1234A  \n  \nString",
    "1-2": "The gateway direct debit ID.",
    "2-0": "Result",
    "2-1": "Approved  \n  \nString",
    "2-2": "Whether the transaction was Approved or Declined.",
    "3-0": "Message",
    "3-1": "Approved  \n  \nString",
    "3-2": "The message for the bank response code.",
    "4-0": "Amount",
    "4-1": "10050  \n  \nNumeric",
    "4-2": "The amount of the transaction to be processed.  \nThis is an integer in the smallest units for the currency (i.e. $100.50 will be 10050)",
    "5-0": "Currency",
    "5-1": "AUD  \n  \nString (3 characters)",
    "5-2": "ISO Currency code for the transaction. Currently only AUD is supported for Direct Debit.",
    "6-0": "Reference",
    "6-1": "INV-1234  \n  \nString (100 characters)",
    "6-2": "The merchant reference for the transaction. This must be unique.  \nIt is recommended that this is alphanumeric only with the exception of hyphen (-) and underscore (\\_)",
    "7-0": "Account Name",
    "7-1": "Max Smith  \n  \nString (18 characters)",
    "7-2": "The bank account holders name.",
    "8-0": "BSB",
    "8-1": "633-000  \n  \nString (7 characters)",
    "8-2": "The bank BSB in the ###-### format.",
    "9-0": "Account Number",
    "9-1": "112498233  \n  \nString (9 characters, numerical)",
    "9-2": "The bank account number, maximum 9 digits.",
    "10-0": "Bank Account ID",
    "10-1": "071-BA-AZ7JK98L  \n  \nString (20 characters)",
    "10-2": "The Bank Account ID to be used for the transaction instead of the bank account details.  \nThis column takes priority over the other bank account columns.",
    "11-0": "Description",
    "11-1": "Invoice INV-1234  \n  \nString (18 characters)",
    "11-2": "The description for the transaction. This will appear on the customers bank statement."
  },
  "cols": 3,
  "rows": 12,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

---
title: "Direct Debit Batch File Columns"
slug: "direct-debit-batches"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon May 14 2018 01:13:12 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Oct 04 2018 01:11:00 GMT+0000 (Coordinated Universal Time)"
---
[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Example Value",
    "h-2": "Description",
    "0-0": "Amount",
    "0-1": "10050  \n  \nInteger  \n  \nRequired",
    "0-2": "The amount of the transaction to be processed.  \nThis is an integer in the smallest units for the currency (i.e. $100.50 will be 10050).",
    "1-0": "Currency",
    "1-1": "AUD  \n  \nString (3 characters)  \n  \nRequired",
    "1-2": "The ISO Currency code for the transaction. Currently only AUD is supported for Direct Debit.",
    "2-0": "Reference",
    "2-1": "INV-1234  \n  \nString (64 characters)  \n  \nRequired",
    "2-2": "The merchant reference for the transaction. This must be unique.  \nIt is recommended that this is alphanumeric only with the exception of hyphen (-) and underscore (\\_).",
    "3-0": "Account Name",
    "3-1": "Max Smith  \n  \nString (32 characters)  \n  \nRequired unless Bank Account ID is present",
    "3-2": "The bank account holder's name.",
    "4-0": "BSB",
    "4-1": "633-000  \n  \nString (7 characters)  \n  \nRequired unless Bank Account ID is present",
    "4-2": "The bank BSB in the ###-### format.",
    "5-0": "Account Number",
    "5-1": "112498233  \n  \nString (9 characters, numeric)  \n  \nRequired unless Bank Account ID is present",
    "5-2": "The bank account number, maximum 9 digits.",
    "6-0": "Bank Account ID",
    "6-1": "071-BA-AZ7JK98L  \n  \nString (20 characters)  \n  \nRequired unless Account Name, BSB and Account Number are present.",
    "6-2": "The Bank Account ID to be used for the transaction instead of the bank account details.  \nThis column takes priority over the other bank account columns.",
    "7-0": "Description",
    "7-1": "Invoice INV-1234  \n  \nString (18 characters)  \n  \nRequired",
    "7-2": "The description for the transaction. This will appear on the customer's bank statement and must be unique."
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

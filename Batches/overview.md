---
title: "Overview"
slug: "overview"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon May 14 2018 01:54:53 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Jun 06 2023 01:16:09 GMT+0000 (Coordinated Universal Time)"
---
Card purchases and bank account direct debits can be processed in bulk by uploading a batch file.

> 📘 File Name
> 
> The file name must use the following format:  `[Prefix]-[Version]-[Type]-[Merchant Username]-[Date]-[Suffix].csv`  
> For example: `BATCH-v1-PURCHASE-acmeinc-20180131-1516337063.csv`

| Filename Component | Example Value | Description                                                                                                                                                                     |
| :----------------- | :------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Prefix             | BATCH         | This value must always be "BATCH".  It indicates that this is a batch processing file.                                                                                          |
| Version            | v1            | The version of the batch file. This should currently be set to "v1".                                                                                                            |
| Type               | PURCHASE      | This indicates the type of records in the file. Use "PURCHASE", "REFUND" or "DIRECTDEBIT"                                                                                       |
| Merchant Username  | acmeinc       | Your merchant username.                                                                                                                                                         |
| Date               | 20180131      | The desired processing date for the batch.  If the date provided is current or past, the batch will be queued for immediate processing.                                         |
| Suffix             | 1516337063    | Choose your own suffix for distinguishing between batches scheduled on the same date (e.g. file created timestamp in epoch time).  This should be no longer than 15 characters. |

> 🚧 File Format Requirements
> 
> The batch file must be in CSV format and use ASCII as the character set. 
> 
> Each line must end in Carriage Return and Linefeed (CRLF).
> 
> The file must not contain any header or footer rows.
> 
> The data in the file must be text-types; i.e. if creating rows in Excel, ensure all cell types are set to Text to ensure numbers are not converted to scientific etc.

## Validation

When a batch file is received for processing it will be validated and then enqueued to be processed on the batch date (or immediately if the date is the same as the upload date or a past date).

## Processing & Completion

For batches which need to be processed as soon as they are received, the date in the filename should be set to the current date. If a batch is for a future date then this date should be used in the filename.

Batches which are for immediate processing will be started as soon as they are properly validated, however they may be queued behind other batches. For future dated batches, processing will commence at midnight, UTC+10 (or UTC+11 during AEDT) (14:00 UTC).

A results file can be downloaded which details the outcome of each transaction.

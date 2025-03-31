---
title: "Create a batch"
slug: "create-a-batch"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Jan 19 2018 04:35:31 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Feb 28 2019 03:54:42 GMT+0000 (Coordinated Universal Time)"
---
> 📘 Batch File Format
> 
> The [Batch File Format](doc:overview) is detailed in the Overview section of the Batches Reference. There are three formats - Purchases, Refunds, Direct Debits.

> 🚧 Filename Convention
> 
> The Batch filename must fit a specific convention in order to be accepted. When uploading your batch please ensure that the filename uses the following pattern:
> 
> `BATCH-[version]-[type]-[username]-[date]-[reference].csv`
> 
> Where:
> 
> - `version` is the file format version (currently v1)
> - `type` is the batch file type (PURCHASE, REFUND or DIRECTDEBIT)
> - `username` is your merchant username
> - `date` is the date in YYYYMMDD format when the batch should be processed
> - `reference` is your reference for the batch file

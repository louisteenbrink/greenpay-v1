---
title: "Batches"
slug: "batches"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Dec 04 2017 02:28:40 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Mar 19 2019 05:22:30 GMT+0000 (Coordinated Universal Time)"
---
# Fields

| Field            | Type              | Description                                                                    |
| :--------------- | :---------------- | :----------------------------------------------------------------------------- |
| `id`             | string            | Unique identifier for this batch.                                              |
| `filename`       | string            | The name of the uploaded batch file                                            |
| `type`           | string            | The batch type - PURCHASE, REFUND or DIRECTDEBIT                               |
| `reference`      | string            | The batch file reference                                                       |
| `status`         | string            | The batch file status - possible values are Completed, Pending, Deleted, Error |
| `process_date`   | date (yyyy-mm-dd) | The date the batch is scheduled for or was processed                           |
| `start_date`     | date (yyyy-mm-dd) | The date the batch was started                                                 |
| `completed_date` | date (yyyy-mm-dd) | The date the batch was completed                                               |
| `created_at`     | date (yyyy-mm-dd) | The date the batch file record was created                                     |

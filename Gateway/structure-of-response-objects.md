---
title: "Structure of response objects"
slug: "structure-of-response-objects"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Sep 07 2018 00:00:40 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 20:35:41 GMT+0000 (Coordinated Universal Time)"
---
All Fat Zebra API responses share the same top level syntax. This lays out the response object, whether the operation was successful or if any errors were received.

| Field        | Type             | Description                                                                            |
| :----------- | :--------------- | :------------------------------------------------------------------------------------- |
| `successful` | Boolean          | Defines whether the request was valid                                                  |
| `response`   | Object/Array     | The scalar or vector serialization of records, depending on the context of the request |
| `errors`     | Array of strings | List of errors encountered when processing the request                                 |
| `test`       | Boolean          | Indicates whether or not the request was made in test mode                             |

Additionally, endpoints that list entities add the following fields to facilitate the paging of results.

| Field           | Type   | Description                                 |
| :-------------- | :----- | :------------------------------------------ |
| `records`       | Number | The sum of records returned                 |
| `total_records` | Number | Total number of records to iterate through  |
| `page`          | Number | The current page rendered in the result set |
| `total_pages`   | Number | Total number of pages to iterate through    |

Each of the sections describing API methods will assume this format and describes the body of the `response` field.

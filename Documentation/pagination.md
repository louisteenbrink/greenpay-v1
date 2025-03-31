---
title: "Pagination"
slug: "pagination"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Jul 17 2018 07:35:58 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Feb 24 2022 00:30:37 GMT+0000 (Coordinated Universal Time)"
---
In order to keep responses quick and small, multi-value results will be paginated.

By default a request will return up to 10 records per page, however this can be specified to return up to 50 per request.

To page through the records, each request will need to provide the following values in the query string:

| Name     | Type    | Description                                                              |
| :------- | :------ | :----------------------------------------------------------------------- |
| `limit`  | integer | The number of records to return per request. Defaults to 10, maximum 50. |
| `offset` | integer | The offset (i.e. page number) to return. Defaults to 1.                  |

For example, if your limit is set to 10, and you wish to retrieve records 101 to 110 you would specify the following parameters in your request:

```
limit=10&offset=11
```

The API will return a maximum of 50 records even if a limit greater than 50 is requested.

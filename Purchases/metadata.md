---
title: "Metadata"
slug: "metadata"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Nov 08 2018 05:40:42 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Nov 08 2018 05:49:38 GMT+0000 (Coordinated Universal Time)"
---
When creating purchases, it's possible to store additional keys and values against each purchase. These values will be returned when querying the purchase in future, and are also visible via the Merchant Dashboard. Attaching metadata is done using the `metadata` key, as demonstrated below.

```json Metadata Example
{
  "metadata": {
    "your_reference": "abcd1234",
    "something_else": 42
  }
}
```

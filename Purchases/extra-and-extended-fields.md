---
title: "Extra and Extended Fields"
slug: "extra-and-extended-fields"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Jul 17 2018 13:48:42 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Nov 08 2018 05:52:21 GMT+0000 (Coordinated Universal Time)"
---
Fat Zebra enables extended fields for merchants to allow advanced integrations where the need arises. These fields include [3D Secure values (XID, CAVV, PARes, VERes, SLI)](doc:3d-secure), [ECM](doc:recurring-and-other-transaction-types) and [Dynamic Descriptors](doc:dynamic-descriptors). If you require this functionality for your integration please contact Fat Zebra support and detail your requirements so we can determine the best option for your needs.

All relevant fields will only be accepted for merchants which are explicitly configured to support extra fields.

All fields should be included under the extra key in the request payload:

```json Example
{
    "extra": {
        "sli": "09"
    }
}
```

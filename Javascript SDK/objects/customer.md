---
title: "Customer"
slug: "customer"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jul 23 2020 06:24:06 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Apr 29 2021 01:17:54 GMT+0000 (Coordinated Universal Time)"
---
The **Customer** object holds details about a customer and is used in the following methods:

- [renderPaymentsPage](doc:renderpaymentspage) 
- [verifyCard](doc:verifycard) 

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Required",
    "h-3": "Description",
    "0-0": "`firstName`",
    "0-1": "string",
    "0-2": "Y",
    "0-3": "Customer first name",
    "1-0": "`lastName`",
    "1-1": "string",
    "1-2": "Y",
    "1-3": "Customer surname",
    "2-0": "`email`",
    "2-1": "string",
    "2-2": "Y",
    "2-3": "Customer email address",
    "3-0": "`address`",
    "3-1": "string",
    "3-2": "Y",
    "3-3": "Customer address  \n  \ne.g. `315/123, Success Blvd`",
    "4-0": "`city`",
    "4-1": "string",
    "4-2": "Y",
    "4-3": "Customer suburb/city",
    "5-0": "`postcode`",
    "5-1": "string",
    "5-2": "Y",
    "5-3": "Customer postcode",
    "6-0": "`state`",
    "6-1": "string",
    "6-2": "Y",
    "6-3": "Customer state",
    "7-0": "`country`",
    "7-1": "string",
    "7-2": "Y",
    "7-3": "Customer country.  \n  \nISO Alpha 2 country codes. e.g. AU, GB, NZ"
  },
  "cols": 4,
  "rows": 8,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


```json
{
    firstName: 'Captain',
    lastName: 'America',
    email: 'hello.world@fatzebra.com.au',
    address: '123 Australia Blvd.',
    city: 'Sydney',
    postcode: '2000',
    state: 'NSW',
    country: 'AU'
  }
```

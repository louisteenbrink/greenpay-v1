---
title: "constructor"
slug: "constructor"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jul 23 2020 05:46:22 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Sep 30 2020 04:38:37 GMT+0000 (Coordinated Universal Time)"
---
## Constructor(params)

### params

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Mandatory",
    "h-3": "Description",
    "0-0": "`username`",
    "0-1": "string",
    "0-2": "Y",
    "0-3": "Merchant username",
    "1-0": "`test`",
    "1-1": "string",
    "1-2": "N",
    "1-3": "Required to be `true` in the Sandbox environment.  \n  \nDefaults to `false`."
  },
  "cols": 4,
  "rows": 2,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


### usage

```json
const fz = new FatZebra({
  username: "MerchantXYZ",
  test: true
});
```

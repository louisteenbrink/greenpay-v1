---
title: "3D Secure Card Payments"
slug: "3d-secure"
excerpt: ""
hidden: false
createdAt: "Thu Nov 08 2018 05:10:42 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 17 2024 00:12:44 GMT+0000 (Coordinated Universal Time)"
---
3D Secure card payment data can be added to authorizations, purchases, and refunds. All fields should be included under the extra key in the request payload.

The values for `sli`, `xid`, `cavv`, `par` and `ver` should be supplied by the 3D Secure MPI being used for transaction authentication.

If you do not have an MPI, Fat Zebra can provide an MPI. Refer to the [3DS2 Integration](doc:3ds2-overview) documentation for more information.

[block:parameters]
{
  "data": {
    "h-0": "Field name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "`sli`",
    "0-1": "String (2-digits)",
    "0-2": "The Security Level Indicator (SLI) indicates the type of card holder authentication used for the transaction. Accepted values are described in the table bellow.",
    "1-0": "`xid`",
    "1-1": "String",
    "1-2": "The XID is the transaction ID from the 3D Secure provider. This is Base64 encoded data.",
    "2-0": "`cavv`",
    "2-1": "String",
    "2-2": "The CAVV is the card authentication verification value, provided by the 3D Secure Provider. This is Base64 encoded data.",
    "3-0": "`par`",
    "3-1": "String",
    "3-2": "This is the `PARes` value from 3D Secure",
    "4-0": "`ver`",
    "4-1": "String",
    "4-2": "This is the `VERes` value from 3D Secure",
    "5-0": "`threeds_version`",
    "5-1": "String",
    "5-2": "3DS version used for authenticating the card. The version may include the major, minor, and build numbers, e.g. `2`, `2.1`, or `2.1.0` are all accepted values.  \nIf omitted, this field will default to a value of `1`.",
    "6-0": "`directory_server_txn_id`",
    "6-1": "String",
    "6-2": "Directory Server Transaction ID from the 3D Secure provider. This is commonly a string in UUID format."
  },
  "cols": 3,
  "rows": 7,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


| Visa & eftpos SLI | Mastercard SLI (MPI compatibility) | Description                                                                                  |
| :---------------- | :--------------------------------- | :------------------------------------------------------------------------------------------- |
| `"05"`            | `"02"`                             | Secure, Authenticated transaction with XID and CAVV present                                  |
| `"06"`            | `"01"`                             | Secure, Non-authenticated transaction (XID present, CAVV not present)                        |
| `"07"`            | `"00"`                             | Secure, Non-authenticated transaction (XID and CAVV not present). This is the default value. |

Note: All fields should be included under the extra key in the request payload.

```json Example: 3DS payment data
{
    "extra": {
        "sli": "05",
        "cavv": "MzM2OGI2ZjkwYjYwY2FjODQ3ZWU=",
        "xid": "ZGUzNzgwYzQxM2ZlMWM0MzVkMjc=",
        "par": "Y",
        "ver": "Y",
        "directory_server_txn_id": "5ddb4c13-2e30-4901-9854-5f0305097a25",
        "threeds_version": "2.1.0"
    }
}
```

---
title: "Dynamic Descriptors"
slug: "dynamic-descriptors"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Nov 08 2018 05:22:51 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Sep 22 2022 22:25:10 GMT+0000 (Coordinated Universal Time)"
---
Specifies the card acceptor descriptor details to show up on the cardholder's statement. This is currently only supported for a handful of banks, and must be enabled before use.

Dynamic Descriptors are specified by the field **descriptor** of type **Hash**.  
Required "descriptor" fields are **name** and **location** and they are both of type **String**. Alternatively you can provide the **raw** descriptor field in lieu of **name** and **location**.

Note: If the length of the values exceeds the maximum you will receive a validation error. It is also important to note that the values may be truncated or reflected differently based on how card issuers display these values to their customers.

| Field        | Type   | Description                                                                                                   |
| :----------- | :----- | :------------------------------------------------------------------------------------------------------------ |
| **name**     | String | The card descriptor name to show on the customers statement. Maximum 20 characters                            |
| **location** | String | The card descriptor location to show on the customers statement. Maximum 13 characters                        |
| **raw**      | String | A raw descriptor value which can be presented instead of the name and location values. Maximum 35 characters. |

```json Example: Dynamic Descriptors
{
  "extra": {
    "descriptor": {
      "name": "Biz Name Pty",
      "location": "Surry Hills"
    }
  }
}
```
```json Example: Raw Descriptor
{
  "extra": {
    "descriptor": {
      "raw": "Biz Name Pty Surry Hills NSW AU"
    }
  }
}
```

## Notes for Bill Payment Service Providers/Consumer Bill Payment Services

Merchants who process transactions for bill payments on behalf of other companies, known as Bill Payment Service Providers or Consumer Bill Payment Services, are required to format their descriptor according to scheme requirements, as follows:

`BPSP NAME*MERCHANT  NAME`

In order to do this the `raw` descriptor field must be used, as per the following example:

```text
{
  "extra": {
    "descriptor": {
      "raw": "PAYCORP*Clean Co"
    }
  }
}
```

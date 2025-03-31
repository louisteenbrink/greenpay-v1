---
title: "AVS"
slug: "avs"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Jan 31 2020 01:09:27 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 19:40:44 GMT+0000 (Coordinated Universal Time)"
---
> 📘 Limited Acquirer Support
> 
> AVS checks are currently only supported by a limited number of acquirers. If the AVS fields are used where support is not yet available, the transactions will process as normal and return an `avs_result_code` of `101` which indicates that AVS is not supported.

AVS (Address Verirfication System) is a service that combats fraudulent activity by verifying a cardholder's address information against the card issuer's records.

AVS is currently supported by Fat Zebra on Purchases via the `billing_address` field. If this field is specified, the Fat Zebra API will return an `avs_result_code` field indicating the result of the AVS check.

The following `avs_result_code` values may be returned:

| avs_result_code | Meaning                                                      |
| :-------------- | :----------------------------------------------------------- |
| `0`             | Both address and postcode match                              |
| `1`             | Both address and postcode do not match                       |
| `2`             | Address matches, postcode does not match                     |
| `3`             | Address matches, postcode not verified                       |
| `4`             | Postcode matches, address noes not match                     |
| `5`             | Postcode matches, address not verified                       |
| `6`             | Both address and postcode not verified                       |
| `7`             | Postcode matches                                             |
| `8`             | Cardholder name, address, and postcode match                 |
| `9`             | Cardholder name, address, and postcode does not match        |
| `10`            | Both cardholder name and address match                       |
| `11`            | Both cardholder name and postcode match                      |
| `12`            | Cardholer name matches                                       |
| `13`            | Address and postcode matches, cardholder name does not match |
| `14`            | Address matches, cardhodler name does not match              |
| `15`            | Postcode matches, cardholder name does not match             |
| `100`           | AVS unavailable                                              |
| `101`           | AVS not supported                                            |
| `102`           | Address information is unavailable                           |

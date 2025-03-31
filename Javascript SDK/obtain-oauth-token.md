---
title: "Obtain an OAuth token"
slug: "obtain-oauth-token"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jul 23 2020 05:17:22 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Nov 15 2023 00:27:15 GMT+0000 (Coordinated Universal Time)"
---
An OAuth access token is required to access most fatzebra.js features. To obtain an OAuth access token:

## OAuth Client

1. Log into the [Fat Zebra Merchant Dashboard](https://dashboard.fatzebra.com.au).

2. Navigate to **Tools** > **OAuth Clients** > **Create new OAuth Client**.

3. Download your OAuth Client credentials, access key and access secret. Make sure you save them securely. For security purposes, downloading these credentials is a one-off process and you will not be able to retrieve them again.

## OAuth Access Token

An OAuth access token is a signed JWT that grants fatzebra.js access to the Fat Zebra platform. It contains basic info about the merchant and a list of access grants that determine what the features the OAuth token has access to.

The token needs to be stored in browser’s local storage with key space `fz-access-token` prior to initialising fatzebra.js.

If the access token is either missing or invalid, fatzebra.js will not be permitted to proceed the intended action (e.g. initiate a 3DS2 check).

For security purposes, the OAuth access token is only valid for 15 mins. It is recommended that a unique access token is created for each payment session you require.

### Obtaining an access token

To obtain an OAuth access token, make a **POST** call to the OAuth endpoints listed below using your `access_key` and `access_secret` that you downloaded from the Fat Zebra Merchant Dashboard.

| Environment | Endpoint                                          |
| :---------- | :------------------------------------------------ |
| Staging     | `POST` <https://api.pmnts-staging.io/oauth/token> |
| Sandbox     | `POST` <https://api.pmnts-sandbox.io/oauth/token> |
| Production  | `POST` <https://api.pmnts.io/oauth/token>         |

#### Request

```json Request Body
{
    "access_key": 'xxx',
    "access_secret": 'xxx'
}
```

#### Response

```json Successful Response
{
    "message": "created",
    "data": {
        "token": "xxx"
    }
{
```

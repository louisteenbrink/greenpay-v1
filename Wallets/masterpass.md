---
title: "Masterpass"
slug: "masterpass"
excerpt: "Masterpass gives your customers a faster, easier way to checkout online and gives you a way to increase sales without significantly changing the way you process payments now."
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jul 18 2018 02:22:04 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Feb 15 2022 21:56:35 GMT+0000 (Coordinated Universal Time)"
---
# Masterpass Customer Checkout Workflow

- A customer creates their account once, or a wallet is made available through the customer's bank.
- The customer chooses to Buy with Masterpass on the merchants website and only needs to login and then select their card and shipping address.
- The customers credit card details are retrieved securely by Fat Zebra and your systems are not exposed to the PCI Scope for this data.
- The new Masterpass lightbox allows the customer to stay on your website and offers a streamlined checkout process.

# Using Masterpass on your Website

> 📘 Fat Zebra has pre-built support for Masterpass in WooCommerce with version 1.5.1 of our plugin. We are also building plugins and extensions for other supported carts, however we do not yet have an expected release date for these other carts.

In order to add Masterpass to your ecommerce website or application:

1. Review the Masterpass agreement - upon acceptance Fat Zebra will provision your Masterpass Merchant account.
2. Fat Zebra will notify you once your account is provisioned.
3. Fetch a request token from Fat Zebra's PayNow service - in this step you may also optionally include shopping cart details to be displayed within the Masterpass light box.
4. Handle the callback from the light box and submit the details (checkout resource URL, OAuth token and OAuth verifier) to Fat Zebra along with your Tokenization or Purchase request.

# Setting up your Masterpass Merchant Account

In order to setup the Masterpass Merchant Account you must first review and accept the Masterpass Terms of Use. To do this:

1. Log into the Merchant Dashboard.
2. Click on the My Account link on the left hand side and then click the Masterpass link.
3. Review and accept the Masterpass Terms of Use.
4. Once the Terms of Use has been accepted your account will be provisioned. You will receive an email notification once this is done.

# Fetch the Request Token

In order to run the Masterpass lightbox, a request token is used along with the Checkout ID. As part of this request, Fat Zebra will setup the shopping cart details for the consumer. Merchants are advised to provide shopping cart items if available, however this is optional.  
To fetch a request token a POST request needs to be sent to the Fat Zebra PayNow service:

```json
POST /v2/YOUR_USERNAME/INVOICE-123/AUD/10.00/abcd1234/masterpass_token?origin_url=https://your_website_base_url&callback_path=/your_cart_page HTTP/1.1
Server: paynow.sandbox.fatzebra.com.au
Content-Type: application/json
 
{
  "cart_items": [
    "description": "Man sized tissues",
    "quantity": 1,
    "cost": 1000,
    "image": "https://www.mansizedtissues.com/images/tissue-box.png"
  ]
}
```

The URL for the Masterpass token request contains a few items relative to the transaction, followed by a hash used to verify the data. The URL parameters are:

[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Description",
    "0-0": "username",
    "0-1": "your Fat Zebra username",
    "1-0": "invoice_number",
    "1-1": "The invoice number or transaction reference",
    "2-0": "currency",
    "2-1": "The currency for the transaction",
    "3-0": "amount",
    "3-1": "The transaction total",
    "4-0": "hash",
    "4-1": "A hash of the invoice details to ensure no parameter tampering, generated like so:  \n  \n`` params_string = [username, invoice_number, currency, amount].join(':')\n`HMAC::MD5(shared_secret, params_string)` ``  \n  \nFor example, with the username 'mantissues', invoice number ABC123, currency of AUD and amount of 10.00 the `params_string` would be: `'mantissues:ABC123:AUD:10.00'`",
    "5-0": "masterpass_token",
    "5-1": "On the end of the URL",
    "6-0": "origin_url",
    "6-1": "Your website's base URL e.g. <https://www.mansizedtissues.com>",
    "7-0": "callback_path",
    "7-1": "The path to the page where the Masterpass button is displayed (e.g. /cart for the cart page)"
  },
  "cols": 2,
  "rows": 8,
  "align": [
    "left",
    "left"
  ]
}
[/block]


The resulting request URL would be:  
`https://paynow.pmnts-sandbox.io/v2/mantissues/ABC123/AUD/10.00/abcdef1234567890/masterpass_token?origin_url=http://www.mantissues.com.au&callback_path=/cart`

For more details on calculating this value please see the [Hosted Payment Pages](ref:hosted-payment-pages) documentation.

The cart items request data should include an array of objects with the following fields:

| Parameter   | Type         | Description                                                                            |
| :---------- | :----------- | :------------------------------------------------------------------------------------- |
| description | String       | The line-item description                                                              |
| quantity    | Integer      | The number of items in the cart for this line item                                     |
| cost        | Integer      | The value of the minimum quantity of the items in the lowest denomination (e.g. cents) |
| image       | String (URL) | The URL of the item image. This URL should be a secure (HTTPS) URL.                    |

A successful response will look like:

```http
HTTP 200 OK
Content-Type: application/json

{
  "successful": true,
  "token": "abc123",
  "checkout_id": "abc123"
}
```

Or, if there was an error requesting the Masterpass token:

```http
HTTP 200 OK
Content-Type: application/json

{
  "successful": false,
  "errors": ["An error occurred. Please contact support."]
}
```

| Response field | Type           | Description                                                                                       |
| :------------- | :------------- | :------------------------------------------------------------------------------------------------ |
| successful     | Boolean        | Indicates if the token request was successful                                                     |
| token          | String         | The Masterpass request token                                                                      |
| checkout_id    | String         | The Masterpass checkout ID                                                                        |
| errors         | Array (String) | Any error messages associated with the request. This will only be present if successful is false. |

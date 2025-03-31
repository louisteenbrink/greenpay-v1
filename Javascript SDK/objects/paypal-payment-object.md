---
title: "PayPalPaymentObject"
slug: "paypal-payment-object"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Aug 27 2020 07:40:42 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Nov 15 2023 00:24:49 GMT+0000 (Coordinated Universal Time)"
---
The [setupPayPal](doc:setup-paypal) method can be used to either:

- Create a PayPal Order (**capture** or **authorization**)
- Create a PayPal Billing Agreement (subscription)

## Create a PayPal Order

| Attribute     | Type                                                                                          | Description | Required/Optional |
| :------------ | :-------------------------------------------------------------------------------------------- | :---------- | :---------------- |
| paymentIntent | [PaymentIntent](doc:paymentintent)                                                            |             | required          |
| paymentMethod | [OrderPaymentMethod](https://docs.fatzebra.com/docs/paypal-payment-object#orderpaymentmethod) |             | required          |

### OrderPaymentMethod

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Required/Optional",
    "0-0": "type",
    "0-1": "String",
    "0-2": "value: **paypal_order**",
    "0-3": "required",
    "1-0": "data.intent",
    "1-1": "String",
    "1-2": "Possible values: **capture**, **authorize**",
    "1-3": "required",
    "2-0": "data.options",
    "2-1": "[OrderOptions](https://docs.fatzebra.com/docs/paypal-payment-object#orderoptions)",
    "2-2": "Merchant specific options",
    "2-3": "",
    "3-0": "data.purchases",
    "3-1": "Array\\[[OrderPurchase](https://docs.fatzebra.com/docs/paypal-payment-object#orderpurchase)]",
    "3-2": "Purchase items & amounts  \n  \n**Note: Currently, only 1 `purchase` is acceptable**",
    "3-3": "required"
  },
  "cols": 4,
  "rows": 4,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


### OrderOptions

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Required/Optional",
    "0-0": "brandName",
    "0-1": "String",
    "0-2": "The name of the brand",
    "0-3": "",
    "1-0": "payeePreferredPayment",
    "1-1": "String",
    "1-2": "Possible values:  \n**UNRESTRICTED**, **IMMEDIATE_PAYMENT_REQUIRED**",
    "1-3": "",
    "2-0": "locale",
    "2-1": "String",
    "2-2": "**en_US**, **ko_KR**",
    "2-3": "",
    "3-0": "landingPage",
    "3-1": "String",
    "3-2": "Possible values:  \n**LOGIN, BILLING**, **NO_PREFERENCE**",
    "3-3": "",
    "4-0": "shippingPreference",
    "4-1": "String",
    "4-2": "Possible values:  \n**NO_SHIPPING**,  \n**SET_PROVIDED_ADDRESS**  \n**GET_FROM_FILE**",
    "4-3": ""
  },
  "cols": 4,
  "rows": 5,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


### OrderPurchase

| Attribute               | Type                                                                                      | Description                                                                                                                 | Required/Optional                                         |
| :---------------------- | :---------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------- |
| description             | String                                                                                    | The purchase description                                                                                                    |                                                           |
| softDescriptor          | String                                                                                    | The soft descriptor is the dynamic text used to construct the statement descriptor that appears on a payer's card statement |                                                           |
| amount                  | [PurchaseAmount](https://docs.fatzebra.com/docs/paypal-payment-object#purchaseamount)     |                                                                                                                             | required                                                  |
| items                   | Array\[[PurchaseItem](https://docs.fatzebra.com/docs/paypal-payment-object#purchaseitem)] |                                                                                                                             |                                                           |
| shippingAddress         |                                                                                           |                                                                                                                             | **required if shippingPreference != SET_PROVIDED_ADDRES** |
| shippingAddress.method  | String                                                                                    | A name for the shipping method                                                                                              |                                                           |
| shippingAddress.address | [ShippingAddress](https://docs.fatzebra.com/docs/paypal-payment-object#shippingaddress)   | Shipping address provide by the merchant                                                                                    | required                                                  |

### PurchaseAmount

**Note: All amount values should be in the smallest currency unit (eg., 100 to charge $1.00, or 100 to Charge ¥100, a zero decimal currency).**

| Attribute        | Type    | Description                         | Required/Optional                                        |
| :--------------- | :------ | :---------------------------------- | :------------------------------------------------------- |
| itemTotal        | Integer | The total purchase amount           | **required** if request includes **items\[].unitAmount** |
| taxTotal         | Integer | The total tax for all items         | **required** if request includes **items\[].tax**        |
| shipping         | Integer | The shipping fee for all items      |                                                          |
| handling         | Integer | The handling fee for all items      |                                                          |
| insurance        | Integer | The insurance fee for all item      |                                                          |
| discount         | Integer | The discount for all item           |                                                          |
| shippingDiscount | Integer | The shipping discount for all items |                                                          |

### PurchaseItem

[block:parameters]
{
  "data": {
    "h-0": "Attribute",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Required/Optional",
    "0-0": "name",
    "0-1": "String",
    "0-2": "The item name",
    "0-3": "required",
    "1-0": "qty",
    "1-1": "Integer",
    "1-2": "The item quantity",
    "1-3": "required",
    "2-0": "unitAmount",
    "2-1": "Integer",
    "2-2": "The item price, in the smallest currency unit (eg., 100 to charge $1.00, or 100 to Charge ¥100, a zero decimal currency)",
    "2-3": "required",
    "3-0": "tax",
    "3-1": "Integer",
    "3-2": "The item tax",
    "3-3": "",
    "4-0": "category",
    "4-1": "String",
    "4-2": "The item category type  \nPossible values: **DIGITAL_GOODS**, **PHYSICAL_GOODS**",
    "4-3": "",
    "5-0": "sku",
    "5-1": "String",
    "5-2": "The stock keeping unit (SKU) for the item",
    "5-3": "",
    "6-0": "description",
    "6-1": "String",
    "6-2": "The item description",
    "6-3": ""
  },
  "cols": 4,
  "rows": 7,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


### ShippingAddress

| Attribute | Type   | Description           | Required/Optional |
| :-------- | :----- | :-------------------- | :---------------- |
| firstName | String | User's first name     |                   |
| lastName  | String | User's last name      |                   |
| address_1 | String | User's address line 1 |                   |
| address_2 | String | User's address line 2 |                   |
| city      | String | User's city           | required          |
| state     | String | User's state          |                   |
| country   | String | User's country        | required          |
| postcode  | String | User's postcode       | required          |

**Note: Please refer to our [documentation](https://docs.fatzebra.com/reference#hosted-payment-pages) for more information on how to calculate the verification HMAC. Alternatively refer to [PaymentIntent](doc:paymentintent).**

** (Pseudo code) verification = hmac_md5(shared_secret, "reference:amount:currency") **

```javascript
var fz = new FatZebra({
  username: MERCHANT_USERNAME,
})

const capturePayment = {
  paymentIntent: {
    payment: {
      reference: reference,  // merchant-generated reference
      amount: 12000,
      currency: "AUD",
    },
    verification: verification
  },
  paymentMethod: {
    type: "paypal_order",
    data: {
      intent: "capture",  // "capture" | "authorize"
      options: {
        brandName: "EXAMPLE INC",
        landingPage: "NO_PREFERENCE", // "BILLING", "LOGIN"
        payeePreferredPayment: "UNRESTRICTED" // "IMMEDIATE_PAYMENT_REQUIRED"
      },
      purchases: [
        {
          description: "Sporting Goods",
          softDescriptor: "HighFashions",
          amount: {
            itemTotal: 9000,
            shipping: 2000,
            taxTotal: 1000
          },
          items: [
            {
              name: "T-Shirt",
              unitAmount: 9000,
              tax: 1000,
              qty: 1,
              sku: "sku01",
              category: "PHYSICAL_GOODS" // "DIGITAL_GOODS"
            }
          ],
          shipping_address: {
            method: "United States Postal Service 1",
            address: {
              firstName: "John",
              lastName: "Doe",
              address_1: "100 Kent Street",
              address_2: "Cafe Lane",
              city: "Sydney",
              state: "NSW",
              postcode: "2000",
              country: "AU"
            }
          }
        }
      ]
    }
  }
}

// This method should be called after setting event listeners!
fz.setupPayPal({
  currency: "AUD",
  payment: capturePayment,
  clientId: MERCHANT_PAYPAL_CLIENT_ID,
  containerId: "paypal-button-container"
})
```

## Create a PayPal Billing Agreement

| Attribute     | Type                                                                                                                | Description                                         | Required/Optional |
| :------------ | :------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------- | :---------------- |
| paymentMethod | [BillingAgreementPaymentMethod](https://docs.fatzebra.com/docs/paypal-payment-object#billingagreementpaymentmethod) | Includes required data for a fulfilling PayPal flow | required          |

### BillingAgreementPaymentMethod

| Attribute               | Type                                                                                   | Description                               | Required/Optional |
| :---------------------- | :------------------------------------------------------------------------------------- | :---------------------------------------- | :---------------- |
| type                    | String                                                                                 | value: **paypal_billing**                 | required          |
| data.name               | String                                                                                 | A name for the Billing Agreement          |                   |
| data.description        | String                                                                                 | A description for the Billing Agreement   |                   |
| data.shippingAddress    | [ShippingAddress](https://docs.fatzebra.com/docs/paypal-payment-object#shippingadress) | Shipping address provided by the merchant | required          |
| data.merchantCustomData | String                                                                                 | Merchant specific data, e.g. a UUID       |                   |

### ShippingAdress

| Attribute | Type   | Description           | Required/Optional |
| :-------- | :----- | :-------------------- | :---------------- |
| firstName | String | User's first name     |                   |
| lastName  | String | User's last name      |                   |
| address_1 | String | User's address line 1 | required          |
| address_2 | String | User's address line 2 |                   |
| city      | String | User's city           | required          |
| state     | String | User's state          | required          |
| country   | String | User's country        | required          |
| postcode  | String | User's postcode       | required          |

```javascript
const billingAgreementPayment = {
  paymentMethod: {
    type: "paypal_billing",
    data: {
      name: "Sample Billing Agreement",
      description: "Stored PayPal account",
      shippingAddress: {
        firstName: "John",
        lastName: "Doe",
        address_1: "100 Kent Street",
        address_2: "Cafe Lane",
        city: "Sydney",
        state: "NSW",
        postcode: "2000",
        country: "AU",
      },
      merchantCustomData: "UUID"
    }
  }
}

// This method should be called after setting event listeners!
fz.setupPayPal({
  currency: "AUD",
  payment: billingAgreementPayment,
  containerId: "paypal-button-container"
})
```

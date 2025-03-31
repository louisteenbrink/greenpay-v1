---
title: "Create Merchant"
slug: "create-merchant-api"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Wed May 25 2022 02:46:22 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed May 25 2022 03:07:45 GMT+0000 (Coordinated Universal Time)"
---
**Authentication**  
The Fat Zebra Reseller API requires HTTP Basic authentication - this uses the Username and Token for your Reseller account which can be found under the User Menu on the right hand side of the header under the API Credentials menu item. Note this can only be viewed by administrator users.

**Content Type**  
The Content-Type for requests must be application/json - if this is not included in the request headers your requests may fail.

**URLs**  
There are two base URLs for the Reseller API:

**Sandbox** - <https://reseller-sandbox.cloudpayments.com.au/api/1/>

**Production** - <https://reseller.cloudpayments.com.au/api/1/>

**Merchants**  
A merchant represents a legal entity which is able to perform credit card transactions against the Fat Zebra Payment gateway. Each merchant is configured with its associated acquirer details (merchant bank, merchant ID, terminal ID)

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "username",
    "0-1": "String",
    "0-2": "The preferred username for the merchant. Must be unique, and will be automatically prefixed with your reseller prefix.",
    "1-0": "name",
    "1-1": "String",
    "1-2": "The merchants Registered Name.",
    "2-0": "display_name",
    "2-1": "String",
    "2-2": "The merchants Trading Name.",
    "3-0": "registered_number",
    "3-1": "Number (9 or 12 digits)",
    "3-2": "The merchants ABN or ACN.",
    "4-0": "address",
    "4-1": "String (4 digits)",
    "4-2": "The merchants Street Address.",
    "5-0": "city",
    "5-1": "String (10 digits)",
    "5-2": "The merchants City.",
    "6-0": "state",
    "6-1": "String",
    "6-2": "The merchants State.",
    "7-0": "postcode",
    "7-1": "String",
    "7-2": "The merchants Post Code.",
    "8-0": "phone_number",
    "8-1": "String",
    "8-2": "The merchants Phone Number.",
    "9-0": "contact",
    "9-1": "String",
    "9-2": "The primary contact name for the merchant.",
    "10-0": "email",
    "10-1": "String (email format)",
    "10-2": "The primary contact email address for the merchant.",
    "11-0": "timezone_name",
    "11-1": "String",
    "11-2": "The timezone for the merchant. Allowed values: Canberra, Melbourne, Sydney, Hobart, Brisbane, Adelaide, Darwin, Perth  \nDefault: Canberra",
    "12-0": "merchant_bank",
    "12-1": "String",
    "12-2": "The merchant acquirer name.  \nMust be one of: Commonwealth, ANZ, StGeorge, NAB, Westpac, Bendigo, BankSA, Melbourne, Macquarie, FDMS Australia",
    "13-0": "merchant_id",
    "13-1": "String",
    "13-2": "The Merchant ID (MID) or Card Acceptor ID (CAID/CAIC) for the merchant, provided by the acquirer.",
    "14-0": "terminal_id",
    "14-1": "String",
    "14-2": "The Terminal ID (TID) or Card Acceptor Terminal ID (CATID) for the merchant, provided by the acquirer.  \n  \nNot required for all merchants.",
    "15-0": "amex_merchant_id",
    "15-1": "String (10 digits)",
    "15-2": "The American Express Merchant ID - optional.",
    "16-0": "diners_merchant_id",
    "16-1": "String (10 digits)",
    "16-2": "The Diners Merchant ID - optional.",
    "17-0": "currencies",
    "17-1": "String (comma separated)",
    "17-2": "The allowed currencies for the merchant. Permitted values are: AUD, NZD, USD, GBP, EUR, JPY, CHF, CAD, HKD, SGD. At least one value is required.  \nDefault: AUD",
    "18-0": "card_acceptor_name",
    "18-1": "String (25 characters)",
    "18-2": "The name configured by the acquiring bank for the card acceptor - this will be displayed on the cardholders statement",
    "19-0": "card_acceptor_location",
    "19-1": "String",
    "19-2": "The location configured by the acquiring bank for the card acceptor - this will be displayed on the cardholders statement",
    "20-0": "card_acceptor_country",
    "20-1": "String (2 characters)",
    "20-2": "The two-character country code for the card acceptor configured by the acquiring bank (e.g. AU) - this will be displayed on the cardholders statement",
    "21-0": "merchant_category_code",
    "21-1": "Numerical (4 digits)",
    "21-2": "The 4-digit Merchant Category Code (MCC) assigned by the acquiring bank.  \nA list of possible MCCs is available from VI SA or Find The Best, however it is recommended that the MCC assigned by the bank is used.",
    "22-0": "visa_payment_facilitator_indicator",
    "22-1": "String",
    "22-2": "Visa Payment Facilitator Indicator issued by scheme",
    "23-0": "mastercard_payment_facilitator_indicator",
    "23-1": "String",
    "23-2": "MasterCard Payment Facilitator Indicator issued by scheme",
    "24-0": "register_3ds",
    "24-1": "Boolean",
    "24-2": "Enables a merchant with 3D Secure  \n  \nDefault: false"
  },
  "cols": 3,
  "rows": 25,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]


The Fat Zebra Reseller API supports the option to update merchant details via a PUT request. All fields can be updated except the merchants username.

The Fat Zebra Reseller API supports the option to list merchant details via a GET request. You can list all merchants, or append the username to the Reseller API URL to retrieve the details for a single merchant.

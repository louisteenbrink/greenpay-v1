---
title: "User Permissions"
slug: "user-permissions"
excerpt: "User permissions can be set to give users access to various parts of the system."
hidden: false
createdAt: "Sun Nov 05 2023 21:02:36 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon May 06 2024 22:26:12 GMT+0000 (Coordinated Universal Time)"
---
## Admin User vs Standard User

> There are two main types of user: 
>
> - admin users
> - standard users

Admin users have read and write permissions across all parts of the merchant dashboard account. While standard users can enjoy selected permissions. User permissions can be added to a newly created user, or alternatively an existing standard user can have their permissions edited, with write permissions read access is automatically instated.

### Important assumption

It is important to note that the difference between and admin user and a standard user with all permissions set, is a standard user cannot view or edit other user accounts, only an admin has this privilege.

**Permissions Overview** 

These are the areas of the system where user access control can be applied in merchant dashboard:

[block:parameters]
{
  "data": {
    "h-0": "Checkbox",
    "h-1": "Prerequisite",
    "h-2": "Access",
    "0-0": "Purchases",
    "0-1": "Authorised Users",
    "0-2": "Payments > Transactions > Purchases",
    "1-0": "Refunds",
    "1-1": "Authorised Users",
    "1-2": "Payments > Transactions > Refunds",
    "2-0": "Disputes",
    "2-1": "Authorised Users that  \nbelong to a Third Party Processor (TPP)  \nenabled merchant",
    "2-2": "Payments > Transactions > Disputes",
    "3-0": "Batches",
    "3-1": "Authorised Users",
    "3-2": "Batch Payments > Batches",
    "4-0": "Direct Debits",
    "4-1": "Authorised Users & Merchant with Direct Entries enabled",
    "4-2": "Home » Direct Debits",
    "5-0": "Direct Credits",
    "5-1": "Authorised Users & Merchant with Direct Entries enabled",
    "5-2": "Home » Direct Credits",
    "6-0": "Customers",
    "6-1": "Authorised Users",
    "6-2": "Customers",
    "7-0": "Billing",
    "7-1": "Authorised Users",
    "7-2": "Billing > Invoices  \nBilling > Payment Plans  \nBilling > Payments  \nBilling > Search",
    "8-0": "Reports",
    "8-1": "Authorised Users",
    "8-2": "Reports > Authentication  \nReports > Transaction  \nReports > Disputes  \nReports > Settlements  \nReports > Payouts  \nReports > Payment Plans  \nReports > Subscribers"
  },
  "cols": 3,
  "rows": 9,
  "align": [
    "left",
    "left",
    "left"
  ]
}
[/block]

---
title: "Xero Integration"
slug: "xero-and-saasu"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Sun Mar 04 2018 23:56:43 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 20:55:48 GMT+0000 (Coordinated Universal Time)"
---
To add Fat Zebra as an invoice payment option for Xero Invoices the following steps should be taken within your Xero account:

1. Click on **Settings** and then **General Settings**
2. Click on **Invoice Settings**
3. Click the **Payment Services** button, and then click **Add Payment Service**, and then choose **Custom Payment URL**
4. Name the service **Fat Zebra**, and set the service URL to the following, replacing **username** with your Fat Zebra merchant username: <https://paynow.pmnts.io/invoice/username/[INVOICENUMBER]/[CURRENCY]/[AMOUNTDUE]>
5. Click **Save**
6. Go back to the **Invoice Settings** area, and click the **Options** button for the invoice template you wish to use this service for, and choose **Edit**
7. In the **Payment Services** drop down select the new **Fat Zebra** service you have created, and then click **Save** 

Once this is completed invoices which are sent via Xero will include a link to view the invoice online - the page hosting the invoice will also include a link to pay the invoice, which will redirect to Fat Zebra hosted payment page.

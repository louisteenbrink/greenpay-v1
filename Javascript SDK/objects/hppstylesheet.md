---
title: "v2 Hosted Stylesheet"
slug: "hppstylesheet"
excerpt: ""
hidden: true
createdAt: "Mon Aug 12 2024 22:07:25 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Sep 02 2024 00:59:35 GMT+0000 (Coordinated Universal Time)"
---
This is a .css stylesheet hosted on a domain secured by https. 

Classes to override styles

```Text css
body {
    background-color: rgba(36, 42, 38, 0.61);
    height: auto;
    min-height: auto;
    padding: 10px;
} 

input.payment-input {
    background-color: #ffffff;
    border: 0;
    height: 45px;
    color: #000000;
    padding-left: 16px;
    font-size: 16px;
    border-radius: 0;
    padding-right: 16px;
}

label {
    font-weight: lighter;
    font-size: 16px;
    line-height: 20px;
}

label[for="payment_request_card_holder"] {
    color: #0028ff;
}

label[for="payment_request_card_number"] {
    color: #941b6e;
}

label[for="payment_request_expiry_date"] {
    color: #0db059;
}


label[for="payment_request_security_code"] {
    color: #b00d8f;
}

input[name="payment_request[card_holder]"] {
    background-color: red;
}

input[name="payment_request[card_number]"] {
    background-color: #0048ff;
}

input[name="payment_request[expiry_date]"] {
    background-color: #3fcc6f;
}


input[name="payment_request[security_code]"] {
    background-color: #bb0fd7;
}

// pay now button

#pay-now {
    width: 100%;
    background-color: #41941b;
    font-size: 16px;
    line-height: 24px;
    height: 55px;
    color: #fafafa;
    border-radius: 0;
    background-image: none;
    border-style: unset;
    border: none;
}


```

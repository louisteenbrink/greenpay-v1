---
title: "v3 Stylesheet"
slug: "v3-stylesheet"
excerpt: ""
hidden: true
createdAt: "Mon Sep 02 2024 01:00:05 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Sep 05 2024 01:27:50 GMT+0000 (Coordinated Universal Time)"
---
This is a .css stylesheet hosted on a domain secured by https. 

Classes to override styles

```Text css
/ ****** document background ****** /

body {
    background-color: rgba(36, 42, 38, 0.61);
    height: auto;
    min-height: auto;
    padding: 10px;
}

// to select all fields - this contains a label and an input

.fields {
  padding: 10px;
} 

/ ****** labels by field ****** /

.card-holder-field label {
    color: red;
}

.card-number-field label {
    color: green;
}

.card-expiry-field label {
    color: blue;
}

.security-code-field label {
    color: pink;
}

/ ****** inputs by field  ****** /


.card-holder-field input {
    background: red;
}

.card-number-field input {
    background: green;
}

.card-expiry-field input {
    background: blue;
}

.security-code-field input {
    background: pink;
}

// to select disabled inputs

input:disabled {
   background: yellow;
}

// to select validation error

.card-number-field span {
   color: orange;
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

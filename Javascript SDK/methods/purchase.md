---
title: "purchase"
slug: "purchase"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jul 23 2020 12:46:10 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jan 18 2023 02:50:37 GMT+0000 (Coordinated Universal Time)"
---
If merchant decides to provide their own custom checkout button (hideButton: **true**) to work with the Hosted Payment Page loaded by **fatzebra.js**, they will need to call the _checkout_ method in order to trigger the payment flow. This method sends a trigger to the Hosted Payment Page within iframe's content view.

```javascript Example
const fz = new FatZebra({
  username: 'xxx',
  test: true
}); 

fz.renderPaymentsPage({...}) // omitted

const handler = function() {
  fz.checkout();
}

document.getElementById('checkoutButton').addEventListener('click', handler);
```

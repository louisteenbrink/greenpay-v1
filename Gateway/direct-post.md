---
title: "Direct Post"
slug: "direct-post"
excerpt: "Direct Post allows a merchant to create payments or tokenize credit card without having the customers credit card details transmitted through their infrastructure, greatly reducing the scope for PCI-DSS.\n\nWhen using Direct Post the communication of credit card details is between the customers browser and the Gateway, with the result being returned to the merchant via a GET request."
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Mar 01 2018 04:42:56 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Mar 01 2018 04:55:43 GMT+0000 (Coordinated Universal Time)"
---
## Benefits

Direct Post offers the following benefits over server integration or a hosted payment page:

- Reduced PCI-DSS Scope (the full card number is not transmitted through your systems)
- Control over branding and user experience
- Easy and straight-forward to implement
- Recurring payments are still possible with the returned card token 

> 📘 It is important to note that while credit card data is not being transmitted through the merchants systems using Direct Post there is still a risk of data loss if the appropriate measures are not taken to protect the security of the integration (for example ensuring the integration has not been tampered with to divert traffic). All merchants using Direct Post must complete the PCI DSS Self Assessment Questionnaire [SAQ A-EP](https://www.pcisecuritystandards.org/documents/SAQ_A-EP_v3.pdf) and complete regular security checks including external scans performed by an Authorised Scanning Vendor.

Direct Post is supported for [Purchases](ref:purchases) and [Credit Cards](ref:tokenized-credit-cards).

## Data Integrity

As the request to the Gateway and the response back to the merchant website is transmitted by the Customers browser data integrity measures have been put in place to ensure the critical data (amount, reference etc) are not modified. This verification is done using a signed hash with a shared secret. Before a request is accepted by the Gateway the data is verified against the hash provided and if this does not match the transaction is rejected. Specific details for the hash calculation are provided in each Direct Post operation's documentation, however an overview is provided below.

The verification value (the hash) is calculated using the following:

- a string of key values joined with a colon (e.g. ABC123:1000:AUD)
- the shared secret, known to both the Merchant and the Gateway - it is important that the shared secret be protected - should the hash need to be calculated dynamically this should be done server-side

The following example pseudo code demonstrates this process:

```
var amount = 100
var reference = "ABC123"
var currency = "AUD"
var shared_secret = "abcd1234"
 
# This will result in the following string: "100:ABC123:AUD"
var verification_string = [amount, reference, currency].join(':') 
# The result of this calculation will be: 5ee475f3047392ea54a1ba0cd5d84921
var hmac = hmac_md5(shared_secret, verification_string) 
```

In some cases the result of the HMAC may result in binary data - it is important that the Hex Digest be used for the verification value.

## JSONP support

In order to support submitting payments using AJAX the request needs to be sent using JSONP, as it is not possible to perform a Cross-domain request to the Gateway. To use JSONP:

- Append .json to the request URL (e.g. <https://gateway.pmnts.io/v2/purchases/direct/TEST.json>)
- Include a JSONP callback
- In the handler for the JSONP callback handle the data - the fields available match those normally returned in a standard Direct Post method 

Example script for performing a JSONP Direct Post request is below. Note: this script depends on jQuery.

```javascript
var pmntscb = function(data) {  
  if (data.r == 1) {
    // Successfully tokenized
    alert("Token: " + data.token);
  } else if (data.r == 97) {
    // Failed, validation error
    var error_message = "Validation error:\r\n";
    jQuery(data["errors[]"]).each(function() {
      error_message += "  " + this + "\r\n";
    });
    alert(error_message);
  } else {
    // Remaining errors could be:
    //   - 95 (merchant not found - check your username)
    //   - 99 (validation error - e.g. form has been tampered with)
    //   - 999 (gateway error - merchant should contact the Gateway if this error persists.)
    alert("Unknown Error. Please Try Again.");
  }
}
   
jQuery("form").submit(function(e) {
  e.preventDefault();
   
  var form = jQuery(this);
    
  $.ajax({
    type: "GET",
    url: form.attr("action"),
    data: form.serialize(),
    jsonpCallback: "pmntscb",
    contentType: "text/javascript",
    dataType: "jsonp",
    error: function(e) {
      // Handle errors here - all non HTTP 2xx errors, such as HTTP 500, 403, 401 etc
      // (very unlikely, but HTTP 500 or HTTP 502 is the most likely to happen)
      alert(e.message);
    }
  });
});
```

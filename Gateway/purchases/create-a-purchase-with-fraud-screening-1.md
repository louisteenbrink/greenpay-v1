---
title: "Create a purchase with fraud screening"
slug: "create-a-purchase-with-fraud-screening-1"
excerpt: ""
hidden: false
createdAt: "Tue Oct 09 2018 02:39:19 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Dec 15 2023 08:57:41 GMT+0000 (Coordinated Universal Time)"
---
# Data Notes

If a value is to be omitted (e.g. has no value, doesn't apply to your systems) you should use null or not include the key/value in the payload.  
There are maximum length constraints on the values for fraud checks. If the value provided is greater then the allowed length the value will be truncated.  
In general strings must only contain the following characters: 

- a-z
- A-Z
- 0-9
- \- (hyphen)
- \_ (underscore)
- ' (single quote)
- , (comma)
- . (period)
- ; (semi-colon)
- : (colon)
- space

Exceptions to the above rule includes email addresses and Device ID

# Fraud Detection Strategy

As a purchase can be made from either web browsers or mobile apps, different strategy is employed to defect fraudulent behaviour. If the purchase call is made from within the mobile app, you can specify a device object (see **Device** below) in the fraud payload.  The object contains information about the physical device and application that a purchase takes place. 

On the other hand if the purchase is made from web browsers (desktop or mobile), you can provide the device_id. See **Device ID**.

**Important**  
Please note that you only need to provide either a device object or device id. An error will be returned if both are present in the fraud payload.

# Device

Although UID is the only field marked as mandatory,  it is highly recommended that you provide all the fields enclosed within the device object in order to the optimise fraudulent behaviours tracking.

# Device ID

Fraud Screening uses Device ID, a customer fingerprinting technology to help accurately identify a customer regardless of where they are accessing a merchant website from. The use of Device ID is highly recommended as this assists in tracking fraudulent behaviour across multiple websites (the Device ID is specific to the customer's system, not the merchants website). To implement Device ID the following will need to be added to every page of the website:

```html
<!-- First add a hidden field with an ID of pmnts_id (or similar) to your form - ensure that the value of this field is included in your checkout postback -->
<input type='hidden' name='pmnts_id' id='pmnts_id' />
 
<!-- Then include the following script tag at the bottom of your page, right before </body> -->
<!-- For production -->
<script type='text/javascript' async defer src="https://gateway.pmnts.io/fraud/fingerprint/MERCHANT_USERNAME.js"></script>
<!-- For Sandbox -->
<script type='text/javascript' async defer src="https://gateway-sandbox.pmnts.io/fraud/fingerprint/MERCHANT_USERNAME.js"></script>
```

To test load the page where the script is included and then inspect the value of the field after a few seconds:

```javascript
alert(document.getElementById('pmnts_id').value);
```

The field should be populated with a large amount of encoded data. In the checkout page capture the value of the `pmnts_id` field and submit this in the request to the Gateway.

> 🚧 Placement of Fingerprint Scripts
> 
> It is important to ensure that this script is loaded on every page, to allow the fingerprinting scripts to accurately provide the customer interactions with your website. If you only add this script to your checkout page you may be impacted by incomplete data or false positives.

# Customer IP Considerations

When a payment request is sent one of the required fields is the customer_ip which most commonly is retrieved from the REMOTE_ADDR param of the server request (this is dependent on the framework being used to host the website). In cases where the website is behind a load balancer or proxies the true IP address will be of the last-hop server, and the original IP address will (if standards are being followed) be moved to the X-Forwarded-For header. In situations where there are multiple proxy hops before reaching the webserver this header may hold multiple IP addresses, separated with a comma and a space (e.g. X-Forwarded-For: 1.2.3.4, 99.98.99.1). In this case it is important that the IP address used is the first address from this set.

The following example code can be used to extract the correct customer IP address from the request:

```php
$customer_ip = $_SERVER['REMOTE_ADDR'];
if (isset($_SERVER['HTTP_X_FORWARDED_FOR'])) {
  $forwarded_ips = explode(', ', $_SERVER['HTTP_X_FORWARDED_FOR']);
  $customer_ip = $forwarded_ips[0];
}
```

# Testing

General testing procedures for Fat Zebra still apply, however there are additional requirements for testing with Fraud Screening.

The fraud screening has 3 different response types: **Accept**, **Challenge** and **Deny**. To simulate any of these responses use one of the following email addresses:

| Email                                             | Response                                                     |
| :------------------------------------------------ | :----------------------------------------------------------- |
| [accept@email.com](mailto:accept@email.com)       | Fraud Check **Accepted**, transaction processed as normal    |
| [challenge@email.com](mailto:challenge@email.com) | Fraud Check **Challenge**, transaction processed as normal   |
| [deny@email.com](mailto:deny@email.com)           | Fraud Check **Deny**, transaction declined and not processed |

Testing with email addresses other then this may result in mixed results (for example transactions may be accepted at first but start receiving challenge responses and eventually deny responses as a result of velocity rules). Should you need to test email functionality within your integration simply get in touch with Fat Zebra and we can temporarily disable Fraud Screening for this account.

An additional response type of Error may be returned if there is a problem processing the fraud request, including but not limited to invalid inputs or problems communicating with the fraud screening services. If this response is received the transaction will not be processed. If the request payload has been confirmed to meet the data type requirements details above and the Error response is still returned please contact support for further assistance.

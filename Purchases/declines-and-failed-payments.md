---
title: "Declines and failed payments"
slug: "declines-and-failed-payments"
excerpt: ""
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Jul 17 2018 12:10:22 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Nov 08 2018 05:57:01 GMT+0000 (Coordinated Universal Time)"
---
## Understanding Declines and Failed Payments

Something about Declines

## Payments declined by Issuers

## Reducing card issuer declines

## Stopped payments

Payments stopped by fraud

```json Stopped Payment Response
{
  "response": {
		"fraud_result": "Deny",
  	"fraud_messages": [
  		"Fraud Check Result Deny",
	    "An attribute associated with an Order matched a pre-configured 'Always Deny' rule."
  	]
	},
  "errors": []
}
```

## Invalid API calls

```http Failed (Permission Denied) - HTTP 403
{
  "successful": false,
  "response": null,
  "test": true,
  "errors": ["You do not have permissions to access this record"]
}
```

## Managing payment errors programatically

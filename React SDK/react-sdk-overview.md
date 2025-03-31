---
title: "React SDK - Overview"
slug: "react-sdk-overview"
excerpt: ""
hidden: false
createdAt: "Wed Jul 19 2023 04:33:17 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jun 05 2024 23:38:06 GMT+0000 (Coordinated Universal Time)"
---
## Introduction

Fat Zebra provides a JavaScript package called named **@fat-zebra/sdk** that enables merchants to access features including:

- [3DS2](3ds2-overview)
- Card tokenization

### Authentication

Each feature accessible via fatzebra.js requires OAuth authentication whereby merchants obtain an OAuth access token for each payment session required. Refer to [Obtain an OAuth token](doc:obtain-oauth-token) for more details.

### Usage

First, install this package by adding it into your `package.json` as a dependency.

```
"dependencies": {
   "@fat-zebra/sdk": "^1.5"
}
```

### Verify a new card

Then to use this package, we can import the relevant parts we need from the SDK. To then verify a card, we can use the `VerifyCard` component.

From this action of this component, we can pull out the token from the card tokenization event, and (if required) wait until the `PublicEvent.SCA_SUCCESS` event has happened before continuing with a customer's purchase.

```
import React from "react";
import { HmacMD5 } from "crypto-js";
import {
  Environment,
  Payment,
  PaymentIntent,
  PublicEvent,
  PaymentConfig,
  Handlers,
} from "@fat-zebra/sdk/dist";
import { VerifyCard } from "@fat-zebra/sdk/dist/react";
import { useState } from "react";

// This should be generated from your backend via your OAuth credentials.
const accessToken =
  "<your oauth access token goes here>";

export default function Checkout({ reference }: { reference: string }) {
  const [events, setEvents] = useState<Array<PublicEvent>>([]);

  const addEvent = (event: any) => {
    setEvents((prev: Array<PublicEvent>) => [...prev, event]);
  };

  const payment: Payment = {
    reference: reference,
    amount: 100,
    currency: "AUD",
  };

  // NEVER expose shared secret to client side. This is just to illustrate working example:
  const [verification] = useState(
    HmacMD5(
      `${payment.reference}:${payment.amount}:${payment.currency}`,
      "<your shared secret goes here>" // Your "Shared Secret"
    ).toString()
  );

  // These are typically sourced from your backend
  const paymentIntent: PaymentIntent = {
    payment,
    verification,
  };

  const config: PaymentConfig = {
    username: "your-username-here",
    environment: Environment.sandbox, // or Environment.production
    accessToken: accessToken,
    paymentIntent: paymentIntent,
    options: {
      sca_enabled: true,
    },
  };

  const tokenizationSuccessful = (event: any) => {
    addEvent(event);
  };

  const scaSuccess = (event: any) => {
    addEvent(event);
  };

  const scaError = (event: any) => {
    addEvent(event);
  };

  // Subscribe to the particular events you wish to handle
  const handlers: Handlers = {
    [PublicEvent.FORM_VALIDATION_ERROR]: addEvent,
    [PublicEvent.FORM_VALIDATION_SUCCESS]: addEvent,
    [PublicEvent.TOKENIZATION_SUCCESS]: tokenizationSuccessful,
    [PublicEvent.SCA_SUCCESS]: scaSuccess,
    [PublicEvent.SCA_ERROR]: scaError,
  };

  return (
    <div className="App flex gap-8 mx-8">
      <div className="w-1/2">
        <VerifyCard
          handlers={handlers}
          config={config}
          iframeProps={{ width: "100%", height: "700px" }}
        />
      </div>
    </div>
  );
}

```

### Verify Existing Card

To then verify a card, we can use the `VerifyExistingCard` component.

From the action of this component, the successful or failed tokenised credit card event will fire. Indicating whether or not a card has been previously tokenised.

This component will return either: “Could not find card on file” or “fz.tokenization.success” status and run sca on each verification.

#### Calculation of verification hash

The verification hash for verify an existing card is calculated by hashing the card token. This is to be done server-side as an example: 

```Text JavaScript

const CARD_TOKEN = "fdsde3yx" 
const SHARED_SECRET = "TEST" -- never expose this to the client
const HIDE_CARD_HOLDER = true
const hash = CryptoJS.HmacMD5(
  CARD_TOKEN,
  SHARED_SECRET
).toString()
```

```typescript React
import React, {useState} from "react";
import {
  Environment,
  PublicEvent
} from "@fat-zebra/sdk/dist";
import {VerifyExistingCard} from "@fat-zebra/sdk/dist/react";

// app.jsx

export default function Main() {
  
  const REFERENCE = "1234"
  const ACCESS_TOKEN = "< oauth access token goes here >"
  const VERIFICATION = "<this hash is calculated server side as seen above using shared secret>"

  return  <VerifyOurCard verification={VERIFICATION} accessToken={ACCESS_TOKEN} reference={REFERENCE} />

}

// VerifyOurCard.jsx
export default function VerifyOurCard(verification, accessToken, reference) {
  const FZ_CARD_TOKEN = "1234"
  const payment = {
    reference,
    amount: 100,
    currency: "AUD"
  };

  const paymentIntent = {
    payment,
    verification,
  };

  const config = {
    username: "TEST",
    environment: Environment.development, // or Environment.production
    accessToken,
    paymentIntent: paymentIntent,
    options: {
      iframe: true
    },
  };
  
  const [events, setEvents] = useState([]);

  const handleEvent = (event) => {
    setEvents((prev) => [...prev, event.type]);
  }
 
  // Subscribe to the particular events you wish to handle
  const handlers = {
    [PublicEvent.FORM_VALIDATION_ERROR]: handleEvent,
    [PublicEvent.FORM_VALIDATION_SUCCESS]: handleEvent,
  };

  return <>
    <VerifyExistingCard
      config={config}
      handlers={handlers}
      cardToken={FZ_CARD_TOKEN}
      iframeProps={{width: "100%", height: "700px"}}
    />
    <div className="flex flex-col overflow-hidden h-max-[100px]">
      {
        events.map((event, index) => <div
          style={{background: event.includes('error') ? "red" : "green"}}>
          <strong>{index + 1} {event}</strong></div>)
      }
    </div>
  </>



}
```

### Creating a payment

There's currently no form support for taking a payment with this SDK.

Instead, we would recommend passing the token from a `TOKENIZATION_SUCCESS` event back to your backend, and then processing a payment from there using the FatZebra API.

---
title: "Apple Pay Button"
slug: "apple-pay-button"
excerpt: ""
hidden: true
createdAt: "Mon Aug 12 2024 02:20:04 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Aug 12 2024 02:20:05 GMT+0000 (Coordinated Universal Time)"
---
```Text JavaScript
import React, {useState} from "react";
import {
  Environment,
  Payment,
  PaymentIntent,
  PublicEvent,
  PaymentConfig,
  Handlers,
} from "@fat-zebra/sdk/src";
import {ApplePayButton} from "@fat-zebra/sdk/src/react"
import {SupportedNetwork, MerchantCapability} from "@fat-zebra/sdk/src/applepay/clients/apple-pay-client";

export default function ApplePayForm({
                                             reference,
                                             verification,
                                             oauthToken,
                                             username,
                                             environment,
                                             options
                                           }: {
  username: string;
  environment: Environment;
  reference: string,
  verification: string,
  oauthToken: string;
  options: { allowed_card_networks: Array<SupportedNetwork>
    allowed_card_types: Array<MerchantCapability> }
  }) {
  const [events, setEvents] = useState<Array<PublicEvent>>([]);

  const payment: Payment  = {
    reference: reference,
    amount: 100,
    currency: "AUD"
  };

  const paymentIntent: PaymentIntent = {
    payment,
    verification,
  };

  const config: PaymentConfig = {
    username,
    environment,
    accessToken: oauthToken,
    paymentIntent: paymentIntent,
    options
  };

  const handleEvent = (event: CustomEvent) => {
    setEvents((prev: Array<PublicEvent>) => [...prev, event.type]);
  }

  // Subscribe to the particular events you wish to handle
  const handlers: Handlers = {
    [PublicEvent.PAYMENT_SUCCESS]: handleEvent,
    [PublicEvent.PAYMENT_ERROR]: handleEvent
  };


  return (
    <div className="App flex gap-8 mx-8">
      <div style={{height: '40px', width: '400px'}}>
        <ApplePayButton
          config={config}
          handlers={handlers} />
      </div>
      <div className="flex flex-col overflow-hidden h-max-[100px]">
        {
          events.map((event: PublicEvent, index: number) => <div
            className={event.includes('error') ? "ml-6 is-danger" : "ml-6 is-success"}>
            <strong>{index + 1} {event}</strong></div>)
        }
      </div>

    </div>
  );
}
```

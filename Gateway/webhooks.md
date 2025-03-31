---
title: "Webhooks"
slug: "webhooks"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Thu Jan 18 2018 04:44:03 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Sep 07 2018 06:20:47 GMT+0000 (Coordinated Universal Time)"
---
# Introduction

Webhooks provide a method for the gateway to send notifications of events to an external service. It is a preferred alternative to polling the system for changes as the notification is usually sent as soon as something happens and it requires less resources on both the source and destination side to maintain.

While webhooks can be created from within the Merchant Dashboard it is also possible to create them programmatically for automating systems.

# Fields

| Field     | Type   | Description                                                                                                                                                                                                    |
| :-------- | :----- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `address` | String | URL that the web hook payload will be sent to.                                                                                                                                                                 |
| `name`    | String | A name for the webhook (e.g. to identify if webhooks are being sent to multiple systems)                                                                                                                       |
| `mode`    | String | The webhook mode - Live or Test                                                                                                                                                                                |
| `events`  | String | The events a webhook target should receive. Events are formatted in a `type:event` format, and wildcards can be used (for example, `purchase:successful`, `purchase:*` and `*` are valid webhook event types). |

# Events

The available Webhook Events are documented [Here](doc:events)

> 📘 Events and Idempotency
> 
> It is important that the system that receives the webhook requests is setup to handle unexpected messages - if you have defined a webhook with wildcards it is possible that newly created and/or unpublished event types may be sent this this endpoint.
> 
> We recommend that when handling the request you check the webhook payload for the event type and discard any messages you do not expect to process to avoid any issues.
> 
> It is also important that the system handling these requests handles idempotency, as the webhook request may be sent multiple times until the request is deemed successful by the Gateway (for example, if there are network issues causing timeouts in the response to the webhook etc)

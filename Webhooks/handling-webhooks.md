---
title: "Handling Webhooks"
slug: "handling-webhooks"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Fri Sep 07 2018 06:16:04 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sat Sep 29 2018 10:33:29 GMT+0000 (Coordinated Universal Time)"
---
# 3rd Party System Responses

When you receive webhooks the Gateway will consider the webhook successfully sent if it receives a HTTP 200 or HTTP 201 response. The system which delivers the webhooks will not follow redirects (e.g. HTTP 301 or HTTP 302), and will consider these responses as failed.

# Retries

Failed webhooks will be retried on an exponential backoff, where each time a request fails, it will be pushed back onto the processing queue, and a delay will be added, growing each time until finally the retries are exhausted.

Webhooks will be attempted for up to 2 days until they are eventually considered permanently failed and will not be re-attempted.

# Idempotency

As webhooks are asynchronous and are transmitted across the internet there is always a chance that the successful posting of a webhook from the Gateway into the receiving system could fail, such as due to network timeouts, receiving end errors etc.

Because of this it is recommended that the systems receiving the webhooks act on the events idempotently. This means that if you depend on webhooks to, for example, dispatch an order, it is important that you check the status of that order in your system's database before executing the workflow to dispatch the order, just in case multiple webhooks for the same subject are received.

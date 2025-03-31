---
title: "Event Listeners"
slug: "event-listeners"
excerpt: "Subscribe to events"
hidden: false
createdAt: "Mon Oct 28 2024 00:00:15 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Oct 29 2024 00:13:09 GMT+0000 (Coordinated Universal Time)"
---
You can subscribe to [Events](doc:events-1) in different ways depending on how your application works:

- If the FatZebra class is instantiated as a singleton service, meaning it is created once and shared across the entire application, it is recommended to use the on method. This ensures the event listener remains active as long as the target object, such as window or a DOM element, exists.
  - If your application instantiates the FatZebra class as a singleton service (i.e. it is created once and shared across the entire application), it is recommended to use the on method. This ensures the event listener remains active as long as the target object, such as window or a DOM element, exists.
    - Note that if a component using the listener is unmounted, the listener will not automatically detach unless you explicitly call off to remove it, which helps prevent memory leaks caused by lingering listeners.
  - If your application instantiates the FatZebra class each time the page renders or the method to create the class is called, it is better to use the onOnce method. This approach ensures the listener automatically unsubscribes itself after receiving the event, preventing unnecessary listeners from remaining active and avoiding potential duplicate events from arising.

<br />

| Method | Behaviour                                                                                                    |
| :----- | :----------------------------------------------------------------------------------------------------------- |
| on     | subscribes to the events for the lifecycle of the window object                                              |
| off    | unsubscribe from the event - usually called when the component is unmounted                                  |
| onOnce | The onOnce method listens for an event, and as soon as that event happens, it automatically stops listening. |

## Subscribing to an event for lifecycle of window

```javascript Example
const fz = new FatZebra({
  username: "MerchantXYZ"
});

// Handle errors related to general errors. For example, client-side validations.
fz.on('fz.validation.error', function(event) {
  // ...
});

// Handle errors related to payment processing. HPP only.
fz.on('fz.payment.error', function(event) {
  // prompt error to customer
  console.log('payment errors: ' + JSON.stringify(event.detail.errors));
});

// Handle successful payment processing. HPP only.
fz.on('fz.payment.success', function(event) {
  console.log('payment data: ' + JSON.stringify(event.detail.data));
});
```

## Unsubscribing from an event

```javascript Example
const fz = new FatZebra({
  username: "MerchantXYZ"
});

// Remove event listener HPP only.
fz.off('fz.payment.success');
```

## Subscribing to onOnce event

```javascript Example
const fz = new FatZebra({
  username: "MerchantXYZ"
});

// Handle successful payment processing. HPP only. Discard the listener once event has been received
fz.onOnce('fz.payment.success', function(event) {
  console.log('payment data: ' + JSON.stringify(event.detail.data));
});
```

---
title: "Events"
slug: "events-1"
excerpt: ""
hidden: false
createdAt: "Thu Jul 23 2020 13:01:50 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Oct 29 2024 00:14:24 GMT+0000 (Coordinated Universal Time)"
---
The **fatzebra.js** Javascript SDK will emit various events that your client-side Javascript code can [subscribe](doc:event-listeners) to.

An event may be emitted along with a `data` payload, which is encapsulated into a [CustomEvent](https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent) object and can be retrieved via the [detail](https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent/detail) property of the event.

## List of fatzebra.js events

- [Validation](doc:validation) 
- [SCA](doc:sca) 
- [Tokenization](doc:tokenization) 
- [Payment](doc:payment)

## Successful Event Data Format

| Attribute | Type   | Description |
| :-------- | :----- | :---------- |
| `message` | string | message     |
| `data`    | object | data        |

```javascript example
{
  message: "xxx",
  data: {
   ... 
  }
}
```

## Error Event Data Format

| Attribute | Type            | Description                                   |
| :-------- | :-------------- | :-------------------------------------------- |
| `errors`  | array of string | error messages                                |
| `data`    | object          | This could be `null` if no data is available. |

```javascript example
{
  errors: [
    "xxx",
    ...
  ],
  data: {
   //  
  }
}
```

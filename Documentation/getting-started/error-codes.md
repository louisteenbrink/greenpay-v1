---
title: "Errors & Timeouts"
slug: "error-codes"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Jul 17 2018 07:35:48 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 06 2022 23:29:53 GMT+0000 (Coordinated Universal Time)"
---
Fat Zebra uses standard HTTP response codes to indicate success or failure of an API request. In general, codes in the 2XX range indicate success. Codes in the 4XX range indicate an error based on the information provided (e.g., a required parameter was omitted, a charge failed). Codes in the 5XX range indicate an error with Fat Zebra's systems. 

Some 4XX errors can be handled programmatically (e.g., a card is declined) and include an error code that briefly explains the error reported.

## HTTP status code summary

| Status Code                        | Summary                                                                                                                                                                                                                 |
| :--------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 200 - OK                           | The request was successfully completed.                                                                                                                                                                                 |
| 201 - Created                      | The request was successful and a transaction was created.                                                                                                                                                               |
| 400 - Bad Request                  | Bad data was received.                                                                                                                                                                                                  |
| 401 - Unauthorised                 | Your API credentials were not valid.                                                                                                                                                                                    |
| 403 - Forbidden                    | The resource you were requesting is not available for your credentials. You will most commonly see this is you are attempting to fetch a payment or refund created by your live credentials with your test credentials. |
| 404 - Not Found                    | The requested object was not found.                                                                                                                                                                                     |
| 422 - Unprocessable Entity         | The data provided was unprocessable, however the syntax of the request was correct.                                                                                                                                     |
| 500, 502, 503, 504 - Server Errors | Something went wrong with Fat Zebra's systems or the underlying infrastructure.                                                                                                                                         |

## Timeouts

When making requests to the Gateway it is important to understand transaction processing timeouts to ensure the best customer experience possible.

Fat Zebra sets a strict timeout of 45 seconds on transactions being processed against the card networks - this means that from the time a request arrives in Fat Zebra's systems, it is permitted to process for up to 45 seconds before the Gateway stops the transaction, and a timeout response sent back to the merchant systems. It is suggested that merchants allow up to 50 seconds for a transaction to complete before retrying.

When a transaction is timed out by the Gateway our systems will automatically issue a transaction reversal, to void any in-flight transactions in the event it may have been successfully processed.

If a merchant chooses to use a lower timeout when communicating with the Gateway it is important to ensure that a query and subsequent void is issued against the transaction reference, to avoid any orphaned transactions impacting card holders.

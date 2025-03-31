---
title: "Test Card Numbers"
slug: "test-card-numbers"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Sun May 13 2018 23:34:12 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Mar 15 2023 02:08:11 GMT+0000 (Coordinated Universal Time)"
---
We provide test card numbers for use in our sandbox environment.  Each of the following card numbers has a predetermined purchase response code.

> ❗️ Important: Use Test Card Numbers Only
> 
> It is important that Merchants, Developers and Testers **only** use the provided test card numbers in the Fat Zebra Sandbox. If live card numbers are used the transactions will not be processed successfully.

For example, every purchase made with VISA 4005 5500 0000 0001 will respond with 00 Approved, and every purchase made with VISA 4557 0123 4567 8902 will respond with 05 Declined.

| Scheme         | Card number          | Purchase response code |
| :------------- | :------------------- | :--------------------- |
| Mastercard     | 5123 4567 8901 2346  | 00 Approved            |
|                | 5313 5810 0012 3430  | 05 Declined            |
| VISA           | 4005 5500 0000 0001  | 00 Approved            |
|                | 4557 0123 4567 8902  | 05 Declined            |
| AMEX           | 3456 789012 34564    | 00 Approved            |
|                | 3714 496353 98431    | 05 Declined            |
| JCB            | 3530 1113 3330 0000  | 00 Approved            |
|                | 3566 0020 2036 0505  | 05 Declined            |
| China UnionPay | 6250946000000016     | 00 Approved            |
|                | 6250947000000014     | 05 Declined            |

We also provide test card numbers with which you can set the purchase response code using the last two digits of the purchase amount.

For example, a purchase of AUD$50.09 with any card number below will respond with 09 Acquirer Busy.

Refer to our list of [Response Codes](response-codes).

| Scheme         | Card number                                    | Purchase response code              |
| :------------- | :--------------------------------------------- | :---------------------------------- |
| Mastercard     | 5555 5555 5555 4444                            | Last two digits of purchase amount. |
|                | 2221 0012 3456 7896                            |                                     |
| VISA           | 4242 4242 4242 4242                            |                                     |
|                | 4111 1111 1111 1111                            |                                     |
|                | 4000 0012 3456 2345 678 (19 digit card number) |                                     |
| AMEX           | 3700 000000 00002                              |                                     |
|                | 3760 701663 31008                              |                                     |
| China UnionPay | 6222 8212 3456 0017                            |                                     |
| Discover       | 6011 3325 6061 8887                            |                                     |
|                | 6011 1111 1111 1117                            |                                     |
| Diners         | 3670 01020 00000                               |                                     |

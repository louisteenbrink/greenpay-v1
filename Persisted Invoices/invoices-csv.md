---
title: "Upload Specification"
slug: "invoices-csv"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Nov 07 2017 23:55:46 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sat Sep 29 2018 09:15:18 GMT+0000 (Coordinated Universal Time)"
---
The Persisted Invoices CSV file must contain five columns in the following order: reference, description, currency, amount, payable. No header row should be included - the first row should contain details of the first invoice to be imported.

[block:parameters]
{
  "data": {
    "h-0": "Column",
    "h-1": "Type",
    "h-2": "Example",
    "h-3": "Description",
    "0-0": "reference",
    "0-1": "Alphanumeric String",
    "0-2": "abcd1234",
    "0-3": "A reference for the invoice.",
    "1-0": "description",
    "1-1": "Alphanumeric String",
    "1-2": "Doloribus qui odit fugit doloremque quod nihil.  \n  \nVoluptate eos sed debitis ut reiciendis distinctio consequuntur.  \n  \nAb culpa dolorem iste quisquam nesciunt reiciendis deserunt.",
    "1-3": "A description for the invoice. May contain new lines.",
    "2-0": "currency",
    "2-1": "ISO 4217 Currency Code",
    "2-2": "AUD",
    "2-3": "The currency that the invoice is payable in.",
    "3-0": "amount",
    "3-1": "Integer",
    "3-2": "123456",
    "3-3": "The amount due on the invoice measured in the minor units of currency e.g. cents, pennies etc. For example AUD + 123456 = $1,234.56",
    "4-0": "payable",
    "4-1": "Boolean",
    "4-2": "true",
    "4-3": "Whether or not the invoice can be paid."
  },
  "cols": 4,
  "rows": 5,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


```text example.csv
410c2106,"Nostrum esse ipsa deserunt ut aut quidem eaque.
Officiis qui et optio qui quaerat quas eligendi.
Quae rerum repellat officia sunt exercitationem laboriosam.",GBP,545936,true
8f25c865,"Sit perferendis minus et.
Aut odit voluptatem laudantium molestiae ullam.
Explicabo vitae et voluptatem.",AUD,836755,false
```

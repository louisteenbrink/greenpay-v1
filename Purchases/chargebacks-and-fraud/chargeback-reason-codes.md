---
title: "Chargeback Reason Codes"
slug: "chargeback-reason-codes"
excerpt: "Visa and MasterCard each use their own set of reason codes."
hidden: true
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Jul 24 2018 11:22:46 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Mon Aug 06 2018 10:38:59 GMT+0000 (Coordinated Universal Time)"
---
> 🚧 Note:
> 
> Fraud is the most common chargeback reason code

## Visa Chargeback Reason Codes

[block:parameters]
{
  "data": {
    "h-0": "Dispute Condition Description",
    "h-1": "Dispute Condition Code",
    "h-2": "Category Code",
    "h-3": "Category Code Description",
    "0-0": "EMV Liability Shift",
    "0-1": "10.1",
    "0-2": "10",
    "0-3": "Fraud",
    "1-0": "EMV Liability Shift Non-counterfeit Fraud",
    "1-1": "10.2",
    "1-2": "10",
    "1-3": "Fraud",
    "2-0": "Other Fraud: Card-Present Environment",
    "2-1": "10.3",
    "2-2": "10",
    "2-3": "Fraud",
    "3-0": "Other Fraud: Card-Absent Environment",
    "3-1": "10.4",
    "3-2": "10",
    "3-3": "Fraud",
    "4-0": "Visa Fraud Monitoring Program",
    "4-1": "10.5",
    "4-2": "10",
    "4-3": "Fraud",
    "5-0": "Card Recovery Bulletin",
    "5-1": "11.2",
    "5-2": "11",
    "5-3": "Authorisation",
    "6-0": "Declined Authorisation",
    "6-1": "11.2",
    "6-2": "11",
    "6-3": "Authorisation",
    "7-0": "No Authorisation",
    "7-1": "11.3",
    "7-2": "11",
    "7-3": "Authorisation",
    "8-0": "Late Presentment",
    "8-1": "12.1",
    "8-2": "12",
    "8-3": "Processing Error",
    "9-0": "Incorrect Transaction Code",
    "9-1": "12.2",
    "9-2": "12",
    "9-3": "Processing Error",
    "10-0": "Incorrect Currency",
    "10-1": "12.3",
    "10-2": "12",
    "10-3": "Processing Error",
    "11-0": "Incorrect Account Number",
    "11-1": "12.4",
    "11-2": "12",
    "11-3": "Processing Error",
    "12-0": "Incorrect Amount",
    "12-1": "12.5",
    "12-2": "12",
    "12-3": "Processing Error",
    "13-0": "Duplicate Processing/Paid by Other Means",
    "13-1": "12.6",
    "13-2": "12",
    "13-3": "Processing Error",
    "14-0": "Invalid Data",
    "14-1": "12.7",
    "14-2": "12",
    "14-3": "Processing Error",
    "15-0": "Merchandise/Services Not Received",
    "15-1": "13.1",
    "15-2": "13",
    "15-3": "Consumer Disputes",
    "16-0": "Cancelled Recurring Transaction",
    "16-1": "13.2",
    "16-2": "13",
    "16-3": "Consumer Disputes",
    "17-0": "Not as Described or Defective  \nMerchandise/Services",
    "17-1": "13.3",
    "17-2": "13",
    "17-3": "Consumer Disputes",
    "18-0": "Counterfeit Merchandise",
    "18-1": "13.4",
    "18-2": "13",
    "18-3": "Consumer Disputes",
    "19-0": "Misrepresentation",
    "19-1": "13.5",
    "19-2": "13",
    "19-3": "Consumer Disputes",
    "20-0": "Credit Not Processed",
    "20-1": "13.6",
    "20-2": "13",
    "20-3": "Consumer Disputes",
    "21-0": "Cancelled Merchandise/Services",
    "21-1": "13.7",
    "21-2": "13",
    "21-3": "Consumer Disputes",
    "22-0": "Original Credit Transaction Not Accepted",
    "22-1": "13.8",
    "22-2": "13",
    "22-3": "Consumer Disputes",
    "23-0": "Non-Receipt of Cash or Load Transaction Value",
    "23-1": "13.9",
    "23-2": "13",
    "23-3": "Consumer Disputes"
  },
  "cols": 4,
  "rows": 24,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


## MasterCard Chargeback Reason Codes

| Mastercard Reason Code Description                             | Code | Category                   |
| :------------------------------------------------------------- | :--- | :------------------------- |
| No Cardholder Authorization                                    | 4837 | Fraud                      |
| Fraudulent Processing of Transactions                          | 4840 | Fraud                      |
| Questionable Merchant Activity                                 | 4849 | Fraud                      |
| Cardholder Does Not Recognize—Potential Fraud                  | 4863 | Fraud                      |
| Chip Liability Shift                                           | 4870 | Fraud                      |
| Chip/PIN Liability Shift                                       | 4871 | Fraud                      |
| Warning Bulletin File                                          | 4807 | Authorization              |
| Authorization-Related Chargeback                               | 4808 | Authorization              |
| Account Number Not On File                                     | 4812 | Authorization              |
| Point-of-Interaction Error                                     | 4834 | Point-of-Interaction Error |
| Transaction Amount Differs                                     | 4831 | Point-of-Interaction Error |
| Late Presentment                                               | 4842 | Point-of-Interaction Error |
| Correct Transaction Currency Code Not Provided                 | 4846 | Point-of-Interaction Error |
| Installment Billing Dispute                                    | 4850 | Point-of-Interaction Error |
| Domestic Chargeback Dispute (Europe Region Only)               | 4999 | Point-of-Interaction Error |
| Cardholder Dispute                                             | 4853 | Cardholder Disputes        |
| Canceled Recurring or Digital Goods Transactions               | 4841 | Cardholder Disputes        |
| Cardholder Dispute—Not Elsewhere Classified (U.S. Region Only) | 4854 | Cardholder Disputes        |
| Goods or Services Not Provided                                 | 4855 | Cardholder Disputes        |
| Addendum, No-show, or ATM Dispute                              | 4859 | Cardholder Disputes        |
| Credit Not Processed                                           | 4860 | Cardholder Disputes        |

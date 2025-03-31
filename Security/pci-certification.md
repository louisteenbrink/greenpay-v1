---
title: "PCI Certification"
slug: "pci-certification"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jul 08 2020 22:11:33 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 08 2020 22:11:33 GMT+0000 (Coordinated Universal Time)"
---
Fat Zebra is a PCI DSS Tier 1 certified service provider. Essentially this means that we have passed a yearly audit from a Qualified Security Assessor (QSA) – in our case, [PCI Consulting Australia](http://www.pciconsultingaustralia.com.au/). This audit covers 12 different requirements including physical security, the storage and transmission of credit card data, data security and more.

For mode details on the PCI-DSS requirements please visit the [PCI-DSS website](https://www.pcisecuritystandards.org/).

## Encryption

In order to protect your customers data, your passwords and your information we encrypt information stored within our database and information transmitted between website users and Fat Zebra's website.

Passwords are stored as a non-reversible hash (this means that if our database is compromised your passwords will not be leaked, and are required to be changed every 90 days. We recommend that you use a passphrase, instead of a password - this is commonly 4 or 5 words which you can remember easily but is still secure.

Credit Card data is encrypted with asymmetric encryption, with a keypair uniquely assigned to your merchant account, along with a 2048-bit passphrase required to decypt the card data. Card data decryption is a bit more complicated - in order to unlock the private key associated with your merchant account an approved operator must provide their own secure passphrase. This allows for quick revocation of keys and rotation of encryption keys regularly.

At the end of the day this may seem complicated, but in testing and in practice we have found this is secure and fast. With security being one of our biggest concerns we're happy to have things a little bit more complicated if it means peace of mind.

## Physical Security

Fat Zebra hosts its equipment, including its Cardholder Data Environment (CDE) within a secure data centre located in Canberra. Access to the computer room facilities require the following:

- Identification is presented and mobile phones/cameras are surrendered
- Visitors sign in and passes are issues
- If after hours, the computer room master key is obtained from a Class B security safe (each visitor has individually assigned access codes)
- The Class 3 alarm is disarmed with the visitors unique access code and the swipe pass is used to access the computer room doors.
- The visitors sign into the computer room
- The key to the secured rack is obtained from the key safe, which is accessed with the swipe pass
- Signing out (and if necessary, re-arming and locking of the computer room) is required before surrendering passes and retrieving identification and mobile phones
- In addition to this, access to our hosting racks is restricted to authorized Fat Zebra staff, however data centre operations staff are granted access with permission from Fat Zebra.

## Data Security and Redundancy

To ensure that your data is always available we have redundant systems in place including a highly available database cluster with off site backups, redundant power, backup power supplies from diesel generators (provided within the data center), redundant cooling and redundant network links.

## Intrusion Detection

Fat Zebra have implemented an industry standard Intrusion Detection System which monitors all traffic on our network for any potentially malicious traffic. When this system detects malicious traffic our security staff are notified, who then investigate the event to determine whether or not further action is required.

## Disclosure

We believe that as a payment gateway, trust between us and our merchants is the most important aspect of doing business.

In the event of any security vulnerabilities, intrusion attempts, data theft/loss or successful intrusions we commit to inform our merchants, merchant banks and the PCI-DSS council as soon as we are aware of the issues. If you have any questions please feel free to contact us.

## Accountability

Fat Zebra staff should never need to see your merchant account, unmasked credit card numbers or your transaction data, except for the following situations:

- Troubleshooting and support
- Security Investigations
- Requests from regulation or law enforcement bodies
- Exceptional situations deemed necessary by the directors of Fat Zebra

If credit card numbers need to be unmasked by authorized Fat Zebra staff appropriate procedures must be followed, and all decryption operations are recorded with full justification.

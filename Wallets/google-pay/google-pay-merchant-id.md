---
title: "Google Pay Merchant ID"
slug: "google-pay-merchant-id"
excerpt: ""
hidden: false
createdAt: "Wed Nov 30 2022 04:24:51 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jul 24 2024 04:19:05 GMT+0000 (Coordinated Universal Time)"
---
All new merchant accounts setup in the Fat Zebra platform are configured to support Google Pay by default.

In order to setup Google Pay in your website or app you will require the **gatewayMerchantID** which is a unique value assigned to each merchant.

As this is automatically setup we have configured our system to create the **gatewayMerchantID** deterministically, so that partners and merchants can determine this themselves when using automated onboarding.

The following steps can be used to build the **gatewayMerchantID**:

1. Take the API token, and derive a SHA256 hash of the value as a hexadecimal digest - the result should be in lower case:

```ruby
digest = OpenSSL::Digest::SHA256.hexdigest(token)
# IF required:
digest = digest.downcase
```

> 🚧 Resulting Digest MUST be lowercase
> 
> Different systems may emit a hexadecimal digest in uppercase. It is important to ensure that you convert this to a lowercase string to ensure you have the correct value, as it is case sensitive.

2. Take the merchant username, and the first 16 characters of the digest, and join these with a hyphen (-):

```ruby
merchant_id = "#{username}-#{digest[0, 16]}"
```

3. The final resulting ID will look something like the following: `username-ce91989e4d0f0fd1`

A full example (in Ruby) is below:

```ruby
username = "TESThooli"
token = "738439923571d79914391d257afb0c3e"

digest = OpenSSL::Digest::SHA256.hexdigest(token)

merchant_id = "#{username}-#{digest[0, 16]}"
```

With these inputs, the resulting value will be `TESThooli-63b648806b4eba75` - you can use these inputs and this resulting value to test your code to ensure the values match.

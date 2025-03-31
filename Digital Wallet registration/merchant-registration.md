---
title: "Apple Pay on the Web - Domain Registration"
slug: "merchant-registration"
excerpt: ""
hidden: false
createdAt: "Wed May 19 2021 11:46:31 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Aug 09 2024 02:22:28 GMT+0000 (Coordinated Universal Time)"
---
In order to start using Apple Pay on the Web each merchant domain and associated sub domains where the Apple Pay on the Web will be used need to be registered and validated with Apple.

The steps do to this are as follows:

1. Download the domain association file for the environment you are setting up the domain for from the list below:

- [Production](https://fatzebra-applepay.s3-ap-southeast-2.amazonaws.com/production.txt)
- [Sandbox](https://fatzebra-applepay.s3-ap-southeast-2.amazonaws.com/sandbox.txt)

2. Place the domain association file on your web server so that it is accessible in the following path:

```text
/.well-known/apple-developer-merchantid-domain-association
```

For example, if your domain is `www.example.com` you should be able to access the file at the following URL: <https://www.example.com/.well-known/apple-developer-merchantid-domain-association>

3. Test the URL to ensure the association file is returned properly:

```shell
curl https://www.example.com/.well-known/apple-developer-merchantid-domain-association
```

4. Make an API request to the Gateway API to register this new domain:

```http
POST https://gateway.pmnts-sandbox.io/v1.0/utilities/apple_pay/domains/www.example.com
```

This will trigger verification of your domain with Apple, and could take up to 45 seconds (in most cases this is completed very quickly).

> 📘 More than one domain?
> 
> If you have more then one domain you can register them with multiple requests.

5. Once this step is completed you can start accepting Apple Pay on the Web for the domains registered. You can now follow the [Apple Pay on the Web](https://developer.apple.com/documentation/apple_pay_on_the_web) documentation to implement the button on your website.

> 🚧 Security Configuration Requirements
> 
> **Note**: if you do not use HTTPS, your HTTPS configuration is not secure, or the domain association file cannot be accessed on your domains via HTTPS this step will fail and the status of the registration will be **Error**

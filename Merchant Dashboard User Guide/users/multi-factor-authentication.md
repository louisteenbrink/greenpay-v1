---
title: "Multi-factor authentication"
slug: "multi-factor-authentication"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Tue Jan 17 2023 02:25:56 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Jan 17 2023 02:25:56 GMT+0000 (Coordinated Universal Time)"
---
## Enabling multi-factor authentication

1. Open the top-left menu by clicking on your name. Then choose "Account Settings". You'll see the screen below:

![](https://files.readme.io/f590422-Untitled.png "Untitled.png")

Click the link that says "Click here to configure MFA". You'll then see a form with a large QR code:

![](https://files.readme.io/278b415-mfasetup.png "mfasetup.png")

You can use a multi-factor password app on your computer or phone -- apps such as 1Password or Authy. Use these apps to scan the QR code. The multi-factor app will then give you a six-digit code. You must enter your _current_ password, and the new code to finish setting this up.

When you have completed this process, you'll see this success message. Take note: this code will regenerate  every 30 seconds to a new random 6 digit number.

![](https://files.readme.io/12bb067-success.png "success.png")

## Signing in with a multi-factor authentication code

When you sign in to the Merchant Dashboard, if it has been more than 6 hours since you've last signed in, you will be prompted to enter an MFA code after first entering your email and password.

![](https://files.readme.io/7033727-signin.png "signin.png")

For the MFA field, enter the code that has been generated from your MFA application.

## Disabling multi-factor authentication

1. Open the top-left menu by clicking on your name. Then choose "Account Settings". You'll see the screen below:

![](https://files.readme.io/dbcf74d-mfa_enabled.png "mfa_enabled.png")

Click the link that says "Click here to disable multi-factor authentication".

You'll then see this screen:

![](https://files.readme.io/d4dc0ea-mfa-enabled-screen.png "mfa-enabled-screen.png")

Enter your _current_ password on this screen. For the code field, open the app that you used to generate this code and enter that code that is displayed now. Clicking the disable button will then disable multi-factor authentication for your account. You will no longer be required to enter an MFA code for your account when signing in. 

## Requiring multi-factor authentication for all users

Fat Zebra support staff can configure an entire merchant to enforce a multi-factor authentication requirement for all users. Contact Fat Zebra support if you wish to do this.

When this feature is enabled, if a user signs in and they _do not_ have an MFA code setup, they'll be prompted to set up one. 

If the user has already configured an MFA code, they'll be prompted to sign in with this MFA code during their regular sign in process.

---
title: "Setting up a sandbox account"
slug: "setup-clover-sandbox-account"
hidden: false
metadata: 
  description: "The Clover sandbox allows you test all app functionality before publishing your app. Learn how to create a sandbox account and test merchant."
  image: 
    0: "https://files.readme.io/8f44079-clover-symbol-green_2.png"
    1: "clover-symbol-green (2).png"
    2: 144
    3: 144
    4: "#228800"
createdAt: "2018-08-21T18:42:04.953Z"
updatedAt: "2021-07-26T21:56:06.548Z"
---
[block:html]
{
  "html": "<!-- This page has content shared with the partner docs. If you update\nthis page, be sure to check if the same change applies to\n\"Settng up a sandbox account\". -->"
}
[/block]
The Clover open platform provides tools for you to design and build solutions for Clover merchants.

The Clover sandbox environment is a testbed where you can experiment with the platform capabilities. You can create test merchant accounts to manage merchant data and also to install and test your solutions for these test accounts. You can also create test merchants in other regions where you want to make your app available.
[block:callout]
{
  "type": "warning",
  "title": "IMPORTANT",
  "body": "If you process credit cards, we highly recommend you secure your account with two-factor authentication to protect merchants and their data."
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "Creating, updating, and deleting apps in the sandbox environment won't affect your published apps installed by Clover merchants using Clover's App Market. Solutions used by Clover merchants are built in the Clover production environment.\n\nTo learn more about the different Clover developer environments and related accounts, see [Developer Accounts](https://docs.clover.com/docs/developer-accounts).",
  "title": "NOTE"
}
[/block]

# Create a sandbox developer account
To create your sandbox developer account:
1. On the sandbox <a href="https://sandbox.dev.clover.com/developer-home/create-account" target="_blank">account creation page</a>, enter your email address. 
2. In the confirmation email you receive, follow the instructions to verify your email address. You are redirected to the Developer Dashboard to complete your account information.
3. Fill in the following information about your account:
  * **Full Name**: Your identification information in the sandbox environment
  * **Public Developer Name**: Either your developer name or company name. The developer name is displayed to users when viewing your app on the <a href="https://www.clover.com/appmarket" target="_blank">Clover App Market</a>.
  * **Create your Test Merchant**: Your first test merchant. You can edit this information at a later point and also create more test merchants in the Developer Dashboard. Use the following table to complete the test merchant information.
[block:callout]
{
  "type": "warning",
  "title": "IMPORTANT",
  "body": "If you are creating a test merchant for any region besides the US, be sure to select the correct currency for testing your app. Some regions, such as Canada, allow processing in more than one currency, and this setting cannot be changed once the test merchant is created."
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Field",
    "h-1": "Description",
    "0-0": "Merchant Name",
    "1-0": "Country",
    "2-0": "Zip/Postal/Pin Code",
    "3-0": "Street Address",
    "4-0": "City",
    "5-0": "State/Province",
    "6-0": "Currency",
    "8-0": "Timezone",
    "9-0": "Employee Passcode Length",
    "0-1": "The name of the merchant, which appears in your dashboard and on DevKit's tied to the account",
    "1-1": "The country where the merchant operates",
    "2-1": "A valid postal code for the merchant",
    "3-1": "The street and building information for the merchant",
    "4-1": "The city of the merchant business",
    "5-1": "The state or province of the merchant business. If the selected country does not have states or provinces, enter `n/a`.",
    "6-1": "The currency accepted by the merchant",
    "8-1": "The timezone for the merchant",
    "9-1": "Select whether employees must use a four- or six-digit code to log on to the test device",
    "7-0": "Phone Number",
    "7-1": "A phone number for the merchant"
  },
  "cols": 2,
  "rows": 10
}
[/block]
4. After you have entered your account information, select **Create Account**. You now see the Developer Dashboard for your account in the sandbox environment.

#Sample inventory
We’ve created a <a href="https://clover.box.com/s/y08he8u7llov7shufskgyb5stlgcs6s8" target="_blank">sample inventory file</a> that will help you get started with your test merchant.

After you log on to your sandbox account, select your test merchant from the drop-down list in the header. Select the Inventory app and then import the sample inventory file.


#Clover platform status updates
Sign up on Clover's Status page, https://status.clover.com/, to stay informed about maintenance windows. Using this information you can plan your work so that you don't attempt to connect to Clover's resources when they will be less responsive than usual or down for maintenance.

The URLs for all sandbox services now have dynamic IP addresses. Any developers using static IP addresses for connecting to sandbox services must support the URLs instead.

Learn more about [Clover environments](doc:clover-environments).
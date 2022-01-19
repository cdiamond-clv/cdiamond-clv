---
title: "DRAFT Monetize your apps"
slug: "draft-monetize-your-apps"
hidden: true
createdAt: "2020-11-06T15:57:16.817Z"
updatedAt: "2020-11-06T17:46:47.255Z"
---
Clover’s billing system enables you to charge for paid apps. After a <<glossary:billable merchant>> subscribes to the Clover App Market, Clover tracks the merchant's app usage and does the following:
* Manages the billing, collects merchant payments, and disburses your share for the merchant’s app usage.
* Tracks the free trial charges and generates a statement from the following month until the merchant uninstalls the app and terminates all subscriptions. Billing starts at the end of the free trial period.
* Processes the previous month’s refund adjustments at the beginning of the month and credits the amount to the merchant before the payment period.

All app fees, merchant app usage payments, and merchant-customer payment processing must be implemented within the Clover or Fiserv platforms. You make 70% of the amount collected from the merchant for an installed app. For more information, see Part 1, section 9.2 of the <a href="https://www.clover.com/developer-agreement" target="_blank">Clover App Market Developer Terms</a>.

If you want to understand about merchant app fees, see the <a href="https://www.clover.com/us/en/help/understand-statements-rates-and-fees/" target="_blank">merchant-facing help</a>.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bb49839-DS-491_-_Billing_Stages.png",
        "DS-491 - Billing Stages.png",
        1380,
        200,
        "#f6f0da"
      ],
      "caption": "Stages of billing: pricing strategy, build app, set up billing, publish approved app, manage refunds"
    }
  ]
}
[/block]
You can build robust apps if you plan your strategy in advance. Follow these guidelines to deliver your apps:
* Identify the most suitable pricing strategy for your app.
* Configure pricing for your apps.
* Publish your app and track the payment statuses.
* Handle lapsed merchants in the app. 
* Initiate refunds for your merchants.

##Billing Cycle
At the beginning of the month Clover generates a statement for a merchant’s subscription charges for the current month, and metered event charges of the previous month. After the merchant’s account is debited in the middle of the month, Clover disburses the payment to you in the third week of the following month. For example, in the third week of September 2019, we disburse payments for merchants billed on the first of August 2019.

#Planning Your Pricing Strategy
Before you begin building apps, it’s important that you take time to decide how you want to price your app for Clover merchants. A pricing strategy helps you plan how you want to build your apps and also avoid making changes after your app is published and merchants have installed it. 
[block:parameters]
{
  "data": {
    "0-0": "Subscription",
    "1-0": "Metered",
    "2-0": "Subscription and Metered",
    "0-1": "Clover creates an advance charge at the beginning of the month. If a merchant upgrades or downgrades their subscription, or a trial period ends, Clover billing adjusts the prorated amounts daily on your account. If a merchant upgrades and then downgrades the same day no charges are added. If a merchant upgrades and uninstalls an app on the same day, Clover billing just refunds the unused portion of the advance charge and doesn't charge for the upgrade.\n\nFor example, a merchant installs a gift card app on 1 June which charges $10 a month for up to five gift cards. Clover exports an advance charge of $10 in June. If there is a trial period, Clover exports an advance of $10 for July which is accounted for in the July statement.",
    "0-2": "<code>Charge amount = Number of days remaining in current month * Subscription price / number of days in current month</code>",
    "h-0": "heading",
    "h-1": "heading",
    "h-2": "heading",
    "1-1": "Clover charges the merchant for each action they take on the app throughout the month. Clover generates a statement on the first of the following month for the total number of actions in the previous month. For example, your gift card app charges $2 for each gift card purchased. A merchant installs the app in June and purchases four gift cards. The merchant’s bill on the first of July shows a charge of $8.",
    "2-1": "You can use a combination of the subscription and metered tiers if your business requires it. The merchant sees two charges in their monthly statement: a single subscription charge for the new month, and a separate charge for the metered event from the previous month. You can enable a 30-day trial period for the subscription tier.",
    "2-2": "For example, your gift card app has the following structure:\n* A $10/month subscription charge for up to five gift cards\n* $2 for every gift card thereafter\nIf the merchant used eight gift cards during the month of May, they would be charged the following amounts on June 1st:\n* A $10 subscription charge for June 1-July 1\n* A $6 (three additional gift cards * $2 = $6) metered charge for May\n\nClover collects this charge from the merchant’s account and pays you your share by the middle of the following month. \n\nYou can add or change pricing for your apps at a later time. For example, if the price of a commodity goes up you can change the price to a new one. \n\nHowever, any merchants who previously downloaded the app will continue under the old subscription price until they reinstall the app. Since Clover’s Terms of Service don’t require merchants to upgrade to new pricing tiers, merchants can continue using the tier price from when they first installed the app.\n\nTo set up your pricing strategy for an app on the Developer Dashboard, see [configuring billing](doc:configuring-billing)."
  },
  "cols": 3,
  "rows": 7
}
[/block]
You can choose from these 3 pricing strategies for your apps:
* Subscription
* Metered
* Subscription and Metered

##Subscription
Clover creates an advance charge at the beginning of the month. If a merchant upgrades or downgrades their subscription, or a trial period ends, Clover billing adjusts the prorated amounts daily on your account. If a merchant upgrades and then downgrades the same day no charges are added. If a merchant upgrades and uninstalls an app on the same day, Clover billing just refunds the unused portion of the advance charge and doesn't charge for the upgrade.

<code>Charge amount = Number of days remaining in current month * Subscription price / number of days in current month</code>

For example, a merchant installs a gift card app on 1 June which charges $10 a month for up to five gift cards. Clover exports an advance charge of $10 in June. If there is a trial period, Clover exports an advance of $10 for July which is accounted for in the July statement.

##Metered
Clover charges the merchant for each action they take on the app throughout the month. Clover generates a statement on the first of the following month for the total number of actions in the previous month. For example, your gift card app charges $2 for each gift card purchased. A merchant installs the app in June and purchases four gift cards. The merchant’s bill on the first of July shows a charge of $8. 

##Subscription and Metered
You can use a combination of the subscription and metered tiers if your business requires it. The merchant sees two charges in their monthly statement: a single subscription charge for the new month, and a separate charge for the metered event from the previous month. You can enable a 30-day trial period for the subscription tier. 

For example, your gift card app has the following structure:
* A $10/month subscription charge for up to five gift cards
* $2 for every gift card thereafter
If the merchant used eight gift cards during the month of May, they would be charged the following amounts on June 1st:
* A $10 subscription charge for June 1-July 1
* A $6 (three additional gift cards * $2 = $6) metered charge for May

Clover collects this charge from the merchant’s account and pays you your share by the middle of the following month. 

You can add or change pricing for your apps at a later time. For example, if the price of a commodity goes up you can change the price to a new one. 

However, any merchants who previously downloaded the app will continue under the old subscription price until they reinstall the app. Since Clover’s Terms of Service don’t require merchants to upgrade to new pricing tiers, merchants can continue using the tier price from when they first installed the app.

To set up your pricing strategy for an app on the Developer Dashboard, see [configuring billing](doc:configuring-billing).
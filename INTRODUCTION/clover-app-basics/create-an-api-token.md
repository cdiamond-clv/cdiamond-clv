---
title: "Generating a test API token"
slug: "create-an-api-token"
hidden: false
metadata: 
  description: "Clover's API requires apps to authenticate with OAuth 2.0. Learn how to generate tokens with this tutorial."
  image: 
    0: "https://files.readme.io/23a41a4-clover-symbol-green_2.png"
    1: "clover-symbol-green (2).png"
    2: 144
    3: 144
    4: "#228800"
createdAt: "2018-08-21T18:53:06.619Z"
updatedAt: "2021-03-02T18:50:54.941Z"
---
Clover uses OAuth 2.0 to create a secure connection between your Web apps and Clover merchant information.
[block:callout]
{
  "type": "info",
  "title": "NOTE",
  "body": "For your Android app, you can simply [generate an API token and query web services](doc:query-web-services) using Clover Android SDK."
}
[/block]
The Clover OAuth 2.0 framework requires you to retrieve an API token before you can query merchant information, such as inventory, orders, and payments.

Clover’s implementation of [OAuth 2.0](doc:using-oauth-20) consists of the following parts:
[block:parameters]
{
  "data": {
    "h-0": "ID",
    "h-1": "Description",
    "0-0": "Client ID (App ID)",
    "1-0": "Client Secret (App Secret)",
    "2-0": "Merchant ID (MID)",
    "3-0": "Authorization Code",
    "4-0": "API Token",
    "0-1": "The Client ID or App ID uniquely identifies an app on Clover App Market.",
    "1-1": "The Client Secret or App Secret is a secret key that is assigned to your app by Clover.",
    "2-1": "The merchant ID uniquely identifies Clover merchants (including test merchants) on the Clover platform. MIDs are 13 characters in length. On the Merchant Dashboard, you can find the MID for your test merchant in the browser window URL.",
    "3-1": "When a merchant has signed in to Clover with their merchant account, you receive an authorization code. With this code, you can request for an API token.",
    "4-1": "With the API token, your app can make REST API calls and access merchant data."
  },
  "cols": 2,
  "rows": 5
}
[/block]
You can view the **App ID** and **App Secret** on the [App Settings](doc:app-settings) page.

# Generating an API token
To generate a test API token for use in the sandbox environment:
1. On the <a href="https://sandbox.dev.clover.com/developer-home/login" target="_blank">sandbox Developer Dashboard</a>, select a test merchant from the header menu. You are redirected to the test merchant dashboard.
2. Click **Setup > API Tokens** from the side-nav. This is where you generate test API tokens.
3. On the API Tokens page, click **Create New Token**.
4. In the **Create new token** modal, enter a name and set permissions based on the test merchant information you want to query and manage. Note that these are app permissions and they map to platform API endpoints.
5. Select **Create Token**. You can create as many test API tokens as required.

With your test API token, you can make a REST API call and access Clover merchant data.
[block:callout]
{
  "type": "danger",
  "body": "Tokens generated with the **Setup** app should only be used when testing the API in sandbox. Using these merchant tokens in production is forbidden.",
  "title": "WARNING"
}
[/block]
---
title: "Making a REST API call"
slug: "make-a-rest-api-call"
hidden: false
metadata: 
  description: "Clover's REST APIs provide access to merchant data so you can build apps that make business run better."
  image: 
    0: "https://files.readme.io/5ca7493-clover-symbol-green_2.png"
    1: "clover-symbol-green (2).png"
    2: 144
    3: 144
    4: "#228800"
createdAt: "2018-08-21T18:54:21.561Z"
updatedAt: "2021-01-11T21:46:04.155Z"
---
The Clover REST API enables you to query relevant information about Clover merchants in your Web app. Relevant information, such as merchant inventory, orders, and payments is available to you using our REST API. Each type of merchant information is represented by an endpoint.
[block:callout]
{
  "type": "success",
  "title": "TIP",
  "body": "For your Android app, you can simply [generate an API token and query web services](doc:query-web-services) using Clover Android SDK."
}
[/block]
# **Making a REST API call**
In this topic, we guide you to make a sample REST API call and retrieve your test merchant’s name.

To make a REST API call:
1. Navigate to the [API Reference](https://docs.clover.com/reference).
2. Under **MERCHANTS > Get a single merchant**, enter the **Merchant Id** value. This value is 13 characters in length and is found in the browser window URL of your test merchant dashboard.
3. Select the **Query Auth** icon at the top-right next to the **Try It** button.
4. Enter the **access_token** value. This value is the test API token that you generated in the sandbox Developer Dashboard.
5. Click **Try It**. The output JSON of the API call is generated at the right of the screen. In the results, the value of the **Name Key** is your test merchant’s name.

For more information about the Clover REST API service, see [Clover REST API](doc:making-rest-api-calls). Use this <a href="https://clover.box.com/s/y08he8u7llov7shufskgyb5stlgcs6s8" target="_blank">sample inventory file</a> to test more REST API calls for your test merchant. On the Merchant Dashboard, select the **Inventory** app and then follow the instructions to upload the sample inventory file.
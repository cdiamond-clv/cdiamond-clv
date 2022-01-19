---
title: "Text formatting conventions"
slug: "text-formatting-conventions"
hidden: false
metadata: 
  description: "Clover's developer docs use specific formatting to explain technical concepts. This page describes the formatting that appears throughout the site."
  image: 
    0: "https://files.readme.io/f350207-clover-symbol-green_2.png"
    1: "clover-symbol-green (2).png"
    2: 144
    3: 144
    4: "#228800"
createdAt: "2019-04-15T16:03:43.046Z"
updatedAt: "2020-10-16T21:06:58.189Z"
---
## Text formatting

The developer docs use the following text conventions to assist with understanding and emphasize important information.

### Curly braces

Text enclosed in braces varies from user to user and should be replaced with values unique to you or your environment. 

For example, each Clover merchant has a unique identifier. In the docs, this is represented with a placeholder: `{mId}` or `{merchantId}`. When copying sample code that includes bracketed values, replace both the brackets and sample values with your own data. 

In the case of an GET request for a single merchant, the sample URL includes the bracketed value `{mId}`.
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://apisandbox.dev.clover.com/v3/merchants/{mId}",
      "language": "text",
      "name": "GET request with placeholder"
    }
  ]
}
[/block]
When using the URL in your own code, replace `{mId}` with the ID value of the merchant you want to retrieve.
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://apisandbox.dev.clover.com/v3/merchants/XKNP0ZWV58J8E",
      "language": "text",
      "name": "GET request with actual value"
    }
  ]
}
[/block]
### Bold text

Bold is used for field labels, button names, menus, and other user interface elements.

Example: On the home screen, tap **Orders**.

### Italics

In a list of steps, italics indicate the result of an action. They are also used for variable text, such as folder names or ID values that are different for each user.

Example: _The sale is processed and the customer receipt is printed._

### Monospace

Monospaced, gray-highlighted text is used for short code samples, file paths, system messages, and user inputs.

Example: Open a web browser and navigate to `http://localhost:8080`.

### Links

[Green text](doc:text-formatting-conventions) is used for links to other sections of the docs or to external resources like our GitHub SDK repos.

## Code blocks

Long code samples are presented in separate blocks for easier reading. The content of each block can be easily copied for use in your code by clicking **Copy**.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"elements\": [\n      { \"item\": {\"id\": \"ABWN2X43EXJN8\"}},\n      { \"item\": {\"id\": \"ABWN2X43EXJN8\"}},\n      { \"item\": {\"id\": \"F1RBG5MKD3SQR\"}},\n      { \"item\": {\"id\": \"F1RBG5MKD3SQR\"}},\n      { \"item\": {\"id\": \"S9230FJR93DFJ\"}},\n      { \"item\": {\"id\": \"S9230FJR93DFJ\"}}\n  ]\n}",
      "language": "json",
      "name": "JSON code block"
    }
  ]
}
[/block]
## Note blocks

As you read the docs, you may encounter a note block that provides additional information or warns you about certain actions.
[block:callout]
{
  "type": "info",
  "title": "NOTE",
  "body": "Notes are informational and provide you with extra details for the section you're reading."
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "IMPORTANT",
  "body": "Important blocks contain information you need to read to ensure your code will work properly with the Clover platform."
}
[/block]

[block:callout]
{
  "type": "danger",
  "title": "WARNING",
  "body": "Warnings caution you against actions that may cause data loss or damage to a Clover device."
}
[/block]
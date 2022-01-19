---
title: "Developer guidelines"
slug: "developer-guidelines"
hidden: true
createdAt: "2018-06-25T21:23:33.918Z"
updatedAt: "2020-11-18T23:41:01.791Z"
---
Welcome to the [Clover App Market](https://www.clover.com/appmarket?clientCountry=US), the world's largest point-of-sale app platform. As a third-party developer, your apps can add functionality and address new use cases for the rapidly expanding Clover merchant community. The following guidelines are designed to help you produce high quality apps, with a smooth development and launch process. These foundations can help your apps provide the kind of excellent merchant experiences that attract and keep loyal subscribers.

In this article, we discuss:
----------------------------

*   [Hardware](#hardware)
*   [Best Practices](#best_practices)
*   [Android Development](#android)
*   [Web Development](#web)
*   [Design Considerations](#design)
*   [Publishing Checklist](#publishing)

Hardware
========

We strongly encourage all developers to [order a Clover DevKit](http://cloverdevkit.com/). DevKits enable you to experience transactions end-to-end from the merchant and customer perspectives. Access to the same environment your customers are using is invaluable. Clover offers merchants custom POS hardware running our own Android-based software.

*   [Clover Station](https://docs.clover.com/build/android-apps/clover-devices/#clover-station)
*   [Clover Station (2018)](https://docs.clover.com/build/clover-devices/#clover-station-2018)
*   [Clover Mobile](https://docs.clover.com/build/android-apps/clover-devices/#clover-mobile)
*   [Clover Mini](https://docs.clover.com/build/android-apps/clover-devices/#clover-mini)
*   [Clover Flex](https://docs.clover.com/build/android-apps/clover-devices/#clover-flex)

Best Practices
==============

There are several best practices you should follow while developing your app.

*   Before you get started, submit a Clover Developer Account for the [US App Market](http://clover.com/developers) or [EU App Market](http://eu.clover.com/developers).
*   Design your app to respond to the needs of [Clover merchants](https://docs.clover.com/welcome-to-clover/meet-our-merchants/).
*   Design your app around Clover's [modules and merchant plans](https://docs.clover.com/build/modules/).
*   Ensure that your app complies with Clover's [App Market Policies](https://www.clover.com/app-market-policies).
*   Do not require users to manually input data that's already accessible to your app via the Clover APIs (other than login credentials).
*   Implement OAuth tokens (if applicable) for authenticating with Clover. Using merchant generated tokens (from the Setup app) will subject your app to removal.
*   Provide a smooth and easy-to-follow onboarding flow for new merchants joining from Clover App Market.
*   Use Clover data objects and representations within your app and configure them to synchronize with Clover services.
*   Set up your app to process all app fees, payment from the merchant for use of your app, and merchant-customer payments within Clover and/or First Data. Refer to the [Developer Agreement](https://www.clover.com/developer-agreement) and the [Billing Documentation](https://docs.clover.com/launch/billing/) for details.
*   Verify that any externally-generated data is syncing with the Clover platform correctly.
*   Thoroughly test your app. Apps that do not function as expected will be rejected.
*   Provide a good end-to-end experience. Apps that do not have a significant and reasonable amount of functionality may be rejected during the review process.
*   Familiarize yourself with Clover's [Developer Agreement](https://www.clover.com/developer-agreement) and [Launch Checklist](https://docs.clover.com/launch/) before you [submit your app for approval](https://docs.clover.com/launch/app-submission/).

### Best Practices for API Usage

#### Rate Limiting

*   If your app or service must trigger requests from multiple merchants, these requests should be staggered as much as possible to avoid bursts of high traffic volume.
*   Use webhooks to trigger updates. Avoid constant polling.
*   Cache your own data when you need to store specialized values or rapidly review very large datasets.
*   If you need to backfill data, it is best to do so during non-peak business hours.
*   Use the [Export API](https://github.com/clover/export-api-examples) if backfilling more than the previous two months of order or payment data.
*   **Per-second Rate Limits:** We maintain per-second rate limits on apps to ensure quality of service for both merchants and developers.

    Level

    Per-second Rate Limit

    Per app

    50

    Per token

    16


*   **Concurrent Rate Limits:** To better control multiple retry requests to CPU-intensive API endpoints, we maintain concurrent rate limiting. The concurrent rate limits are set for the number of in-progress API requests you can have at the same time.

    Level

    Concurrent Rate Limit

    Per app

    10

    Per token

    5

    For instance, if the concurrent rate limit has been set to 5, you can make up to 5 running API requests at the same time. While the server is responding to these 5 requests, your 6th API request will lead to a 429 HTTP response (rate limit reached).

*   **Handling 429 HTTP responses:** You can avoid the 429 HTTP response by staggering API requests in a queue such that the server is never responding to requests more than the set limit. We recommend that you respond with [exponential back-off](https://medium.com/clover-platform-blog/conquering-api-rate-limiting-dcac5552714d).

    The following table can help you identify the type of 429 HTTP response you are receiving in the response header.

    Level

    Response Header

    Per app

    `X-RateLimit-crossTokenLimit`

    Per token

    `X-RateLimit-tokenLimit`

    Per app (Concurrent)

    `X-RateLimit-crossTokenConcurrentLimit`

    Per token (Concurrent)

    `X-RateLimit-tokenConcurrentLimit`

    If your product requires more capacity, please [contact us](mailto:appmarketbusiness@clover.com) and submit a request for review.


#### Security

*   Protect sensitive customer and employee data. Do not expose names, addresses, or phone numbers publicly.
*   Never expose auth tokens or passwords of any kind.

#### Monetary Calculations

*   Your app should calculate taxes using [this algorithm](https://docs.clover.com/build/web-apps/calculating-order-totals).
*   Always pass in monetary values as longs representing the smallest denomination of the merchant's currency.

#### Other Best Practices

*   Do not multithread client `POST` calls. This behavior can create system delays due to deadlocks.
*   Query with `modifiedTime` filters when possible to avoid repolling unmodified data.
*   Minimize data usage. Merchants may be on limited mobile data plans.

Android Development
===================

#### Best Practices

*   We strongly encourage you to integrate some form of crash reporting utility into your Android products. This will help you maintain operational awareness of your product.
*   We also recommend that you collect metrics on app usage. This will help you build better products and increase your awareness of any issues.
*   To avoid confusing consumers, **do not use the term** **PIN**in your app.

#### Code Quality

Your app should conform to the following Java and Android programming practices:

*   [Android Developer Guidelines](http://developer.android.com/guide/index.html)
*   Principles of object-oriented design (SOLID)
*   [Java Style Guidelines](https://google.github.io/styleguide/javaguide.html)

You should also understand the [difference between compileSdkVersion, targetSdkVersion, and minSdkVersion](http://developer.android.com/guide/topics/manifest/uses-sdk-element.html). Leverage the native Android buttons, such as the Back and Home buttons.

#### Device Rotations

Note that display rotation is disabled on Clover Mobile and Clover Mini. Clover Station uses display rotation when switching from merchant-facing mode to customer-facing mode. If your app will be available on Clover Station, it must gracefully handle display rotation.

#### Async Tasks and Executors

*   Minimize or eliminate work on the main UI thread.
*   Verify that your activity isn't finished or destroyed upon completion of an AsyncTask's background task.
*   Use a back-off switch when responding to errors and confirm normal functioning before proceeding, instead of starting new loops.

#### Security

*   Do not check app tokens into your source code online.
*   Use Google's Android Keychain when storing tokens on the Clover device.
*   Do not prompt users to enter sensitive cardholder data, such as card numbers and expiration dates, except as part of Clover's payments SDK
    *   This requirement means that third party Clover Apps are _not_ payment apps as the term is defined in [PCI PA DSS](https://www.pcisecuritystandards.org/minisite/en/docs/PA-DSS_v3.pdf).
*   See our [guidance on SSL/TLS](https://docs.clover.com/faq/what-ssltls-cipher-suites-should-i-support/).
*   Follow the [SEI Cert Java Secure Coding Guidelines](https://www.securecoding.cert.org/confluence/display/java/SEI+CERT+Oracle+Coding+Standard+for+Java).

Web Development
===============

#### Security

Familiarize yourself with basic web security principles. The Open Web Application Security Project (OWASP) offers several resources that will help you get started:

*   [OWASP homepage](https://www.owasp.org/index.php/Main_Page)
*   [OWASP Top Ten Project](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
*   [Developer Guide](https://github.com/OWASP/DevGuide)
*   [Cheat Sheets](https://www.owasp.org/index.php/OWASP_Cheat_Sheet_Series)

#### Merchant Data

*   Because the Clover API allows access to a database, you will need to follow the security standards for database access.
*   Web applications should access the Clover API via server-to-server requests when possible.
*   You must store any data that your own services cache securely.

#### Limiting Client Access

*   Customer and employee-facing apps must prevent unauthorized users from accessing privileged data, including the Clover credentials your app uses.
*   Use secure logins and session tracking if needed.
*   Server logic should prevent unauthorized access to data via injection.
*   Any data passed to the client in any format should be considered vulnerable.

#### Clover Integration

*   Make it easy for merchants to login. The URL for your web app should launch the login flow, not navigate to the general home page for your business.
*   Include your Web URL prior to submission, and test it with an example OAuth request.
*   All apps must be mobile-friendly.

Design Considerations
=====================

#### Image Assets

Your app's Launcher Icons should be [mipmap resources](http://developer.android.com/tools/projects/index.html#mipmap). Icons must conform to standard Android sizes:

*   Clover Station - 48 × 48 (mdpi)
*   Clover Mini/Mobile - 72 × 72 (hdpi)
*   Clover Mini/Mobile (first three apps) - 192 × 192 (xxxhdpi)

You can use [third-party icon generators](https://romannurik.github.io/AndroidAssetStudio/index.html) to resize your logo.

#### Graphic Design

*   Be aware of the screen dimensions of all of the [Clover devices](https://docs.clover.com/build/android-apps/clover-devices/) you plan to support, and design with these dimensions in mind.
*   A single merchant may have any or all of the Clover devices. Aim for a consistent cross-device experience.
*   If your app will include a customer-facing component, your design will reflect on the business using your app. These interfaces should be pleasing and professional.

#### Usability

*   Your app will be used under fast-paced working conditions. Strive for clear, easy to use, and robust workflows that involve as few steps as possible.
*   App design should emphasize clarity and accessibility. Use high-contrast, readable fonts, as well as large text and inputs.
*   If you're adapting an app that was developed for another platform, make sure it only includes features and buttons that are relevant to the Clover user.
*   [Google's Material Design Guidelines](https://www.google.com/design/spec/material-design/introduction.html#) are a good place to start.

 Publishing Checklist
=====================

#### App Details

Your app details must include:

*   A clear, detailed description outlining the app's features and functionality.
*   High-resolution screenshots.
*   A help/FAQ site URL.
*   Contact information for merchant support.

You can improve your app's visibility in the [Clover App Market](https://www.clover.com/appmarket) by including descriptive keywords in the tagline.

#### App Pricing

*   Set your subscription levels, and be sure to enable and disable them as needed.
*   Consider a freemium model to make your app attractive to download.
*   You will not be able to alter metered, pay-per-action billing events after we've approved your app for the Clover App Market.
*   Review the [Billing](https://docs.clover.com/launch/billing/) section for more details.

#### App Submission

*   Be sure that your app does not infringe on the intellectual property rights of others, including the Clover brand. For example, do not use "Clover" or any other registered trademark in your app name, as this would imply ownership. You should also avoid using the Clover brand in the root domain of your help site.
*   The [Clover App Market](https://www.clover.com/appmarket) is live in the US, UK, and Republic of Ireland.  When submitting to a new market, be aware of the differences between each country, including local currency.
*   Developers must provide relevant login credentials and any other hardware or resources required to review your app.
*   If you have an Android app, you must submit the APK with the app. Once we've approved your submission, be sure to publish both.
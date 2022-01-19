---
title: "How Apple Pay works and why it matters for developers"
slug: "how-apple-pay-works-and-why-it-matters-for-developers"
hidden: true
createdAt: "2018-06-25T21:23:33.918Z"
updatedAt: "2020-05-12T17:10:59.397Z"
---
_**Update:** If you'd like to learn more, come to Clover's Apple Pay developer event in Mountain View on Wed, Oct 8: __[http://www.eventbrite.com/e/apple-pay-deep-dive-how-it-works-and-what-it-means-tickets-13394038931?aff=blog](http://www.eventbrite.com/e/apple-pay-deep-dive-how-it-works-and-what-it-means-tickets-13394038931?aff=blog)__Background: Clover and First Data (our parent company) have been working with Apple to prepare for the launch of Apple Pay to support developers, merchant acquirers, and issuing banks (see First Data's [press release](https://www.firstdata.com/en_us/about-first-data/media/press-releases/09_09_14.html)). Clover is enabling all merchants to accept In-App payments, and will be In-Person/NFC enabling all merchants as well (see [https://www.clover.com/features/iphone](https://www.clover.com/features/iphone))__. Here's a bit of how it works from a developer's perspective, and why it matters._ Apple Pay marks the first time a popular operating system is making payments a platform service for real-world, non-digital-good transactions, in a broad, inclusive manner that is compatible with the mainstream payments processing industry. At Clover we're particularly excited because we believe it opens up lightweight apps that can interact and transact with small-and-medium brick-and-mortar restaurants. By lightweight, I mean that these apps won't need to maintain a user database, require user logins, worry about getting cards on file, or being an unwilling payment aggregator. i.e., it will be at least 10x easier. I expect a huge amount of innovation in real-world mobile commerce as a result over the coming years because of the revolution that Apple Pay is starting.

Network-Level Tokenization
--------------------------

> "All problems in computer science can be solved by another level of indirection". -- [David Wheeler](http://www.dmst.aueb.gr/dds/pubs/inbook/beautiful_code/html/Spi07g.html)

The first and most important thing to know about is tokenization.The payment networks (Visa, MasterCard, Amex, etc.) have been very busy building something called _tokenization_. I call this _network-level tokenization_ to distinguish it from the more familiar forms of tokenization, which is typically performed at either the gateway (such as the Braintree card vault) or the acquiring platform (such as First Data's TransArmor).

Ecommerce developers should be quite familiar with the concept of credit card vaults, which take in the PAN and give you back a token to use in its stead. These vaults are typically provided by ecommerce payment gateways, such as Braintree or Stripe, and let you put credit cards on file for your users. I call this _gateway-side tokenization_. The defining characteristic of these tokens is that they're scoped to a _single merchant._ They're useful for a developer who wants to keep a credit card on file (to enable low-friction transactions) but without the burden of securing (and associated compliance) of maintaining a database of PANs.Here's the authorization flow when a gateway-side token is used:

\[caption id="attachment_824" align="aligncenter" width="500"\][![acadia-drawing-acquirer-side-tokenization (1)](acadia-drawing-acquirer-side-tokenization-1-e1433197474532.png)](https://docs.clover.com/wp-content/uploads/2014/09/acadia-drawing-acquirer-side-tokenization-11.png) Gateway-side tokenization\[/caption\]  

The payment networks are proposing something very different: _network-side tokenization_. These tokens are very different. They are essentially aliases for PANs that are exchanged during an authorization by the network. These tokens are provisioned (see below) into the secure element on the iPhone 6 and used in authorization flows (further protected with 3-D Secure -- see below).Here's the authorization flow when a network-side token is used: \[caption id="attachment_826" align="aligncenter" width="500"\][![Network-side tokenization](https://docs.clover.com/wp-content/uploads/2014/09/acadia-network-level-tokenization-1-e1433197484799.png)](acadia-network-level-tokenization-1-e1433197484799.png) Network-side tokenization\[/caption\] There are several important things about these network-side tokens:

*   They look like standard PANs -- e.g. they're 16 digits. They're mostly compatible with the existing payment processing infrastructure.
*   The tokens are issued within a special BIN in the network's routing tables that flag it as a token rather than standard PAN.
*   They are exchanged via the network by _Token Service Providers,_ a new role in the ecosystem.
*   They are provisioned via a Token into a secure element of a mobile device or some other "secure enough" storage (perhaps [Android HCE](https://developer.android.com/guide/topics/connectivity/nfc/hce.html)), facilitated by the issuing bank.

Most developers reading this have likely never read an EMVCo specification, but this one is worth a read: [EMV Payment Tokenisation Specification - Technical Framework](http://www.emvco.com/specifications.aspx?id=263).This is the typical way that a developer would provision a token: \[caption id="attachment_829" align="aligncenter" width="500"\][![Token provisioning](acadia-old-school-token1-e1433197416950.png)](https://docs.clover.com/wp-content/uploads/2014/09/acadia-old-school-token11.png) Token provisioning\[/caption\] \[caption id="attachment_828" align="aligncenter" width="500"\][![tokenization](tokenization-e1433197497757.png)](https://docs.clover.com/wp-content/uploads/2014/09/tokenization1.png) Network-side tokenization\[/caption\] EMV token provisioning is entirely different -- it's between the issuer, the wallet, and the Token Service Provider:

The end result is a token that can be used across merchants and both online (In-App) and offline (NFC, In-Person).

User Logins
-----------

After thinking about it a second, you might realize "why do I need my user to create an account with an email address and password at all?" A primary driver (though not only) was to have an account to associate the gateway-side token with. This is no longer strictly necessary: A consumer could simply download an app that connects them with a local merchant, browse the menu, and buy something from their table. This is really important when it comes to apps for small- and medium-sized businesses (local merchants).

Accidental Merchant Aggregators
-------------------------------

Many mobile wallets and online-to-offline services have become merchant aggregators, where the company becomes the merchant-of-record for many submerchants.

Say you're an order-ahead app enabling consumers to buy food and pick it up later. You really don't want to be in the payments business, but how else do you collect money from the consumer and to the restaurant? There's so much friction in the system that the typical way is to become the merchant-of-record, which is a position you accept begrudingly. Chargebacks and disputes? It's your problem now.

Network-level tokenization, and iPhone in particular, will radically change this dynamic. Commerce apps won't be forced to become aggregators any longer -- they simply need to use the iOS payment SDKs, and the SDK from the merchant acquirer, to process the payment.Clover is making this even easier -- all Clover merchants will be enabled for In-App payments, which will give developers instant access to many thousands of merchants through our APIs (for submitting and reading orders, reading and updating menus and retail inventory, receipt printing, etc.). We're selling Clover Station to thousands of merchants a month, enabling developers to reach these merchants through the Clover App Market.

iOS Payments SDKs
-----------------

Developing an iOS app that uses Apple Pay In-App payments is quite simple. You will use two different APIs:

1.  iOS In-App payments API, for interacting with the user and getting a payment token.
2.  Your merchant acquirer's API, for processing the transaction with said token.

Check out First Data's [Payeezy SDK](https://developer.payeezy.com/) (even more so if you're a Clover developer). In the future all Clover merchants who desire it will automatically be able to accept In-App payments.

3-D Secure
----------

3-D Secure, known commonly as Verified by Visa and MasterCard SecureCode has been largely ignored in the U.S. This is a crude analogy, but 3-D Secure is the ecommerce analog to EMV (which authenticates a cardholder via cryptograms coming from the card). It provides authentication from the issuing bank to use the token that has been provisioned onto the iPhone.

Developers working on iPhone In-App payments don't need to know the details of 3-D Secure when they use Payeezy, but I find it interesting (and you'll find some references to 3-D Secure in the Payeezy SDK). Here's what a transaction message to a gateway looks like before 3-D Secure (from the Payeezy API docs):

> {
>     "merchant_ref": "Astonishing-Sale",
>     "transaction_type": "purchase",
>     "method": "credit_card",
>     "amount": "1299",
>     "currency_code": "USD",
>     "credit_card": {
>         "type": "visa",
>         "cardholder_name": "John Smith",
>         "card_number": "4788250000028291",
>         "exp_date": "1014",
>         "cvv": "123"
>     }
> }
> 
>  

And after 3-D Secure (also from the Payeezy API docs):

> {
>   "merchant_ref":"merchant-specific-info (This is optional)",
>   "transaction_type": "purchase",
>   "method": "3DS",
>   "3DS":  {
>     "type": "A",
>     "version": "EC_v1",
>     "merchantIdentifier": "mock-1",
>     "applicationData": "VGhpcyBpcyBzb21lIHRlc3QgZGF0YS4gIDAxMjM0NTY3ODk=",
>     "data": "v6cqGDrjcJUCLdpRkSQIt...",
>     "signature": "AKCAMIIBoTCCAUgCAQEwCQYHTBFMQswCQYDVQQGEwJVUzE...",
>  "header":  {
>       "applicationDataHash": "4b5745dd55d72886c06a2c65bb05...",
>       "ephemeralPublicKey": "MFkwEwYHKoZIzj0CAQYIKoZIzj0D...",
>       "publicKeyHash": "YmSWN7lj4+A6fVJVPicP8TgS7gI7oug...",
>       "transactionId": "34303833303938"
>     }
>   }

Apple Pay NFC Payments
----------------------

NFC has been derided for years in the U.S. (though my coworker's 65-year-old mother arrived from Australia a couple days ago complaining bitterly that merchants here can't take tap payments). It's a really great technology that's just been waiting for a tipping point. That point is here.Apple Pay uses industry-standard EMV contactless protocols over NFC (and MSD contactless for backward compatibility). This makes it compatible with a wide range of contactless payment terminals in deployment today. Clover is NFC-enabling all current and future Clover products.

_About the author: John Beatty is co-founder and President of Engineering at Clover. Follow him at [http://twitter.com/beatty](http://twitter.com/beatty). Follow Clover Engineering at [http://twitter.com/CloverEng](http://twitter.com/CloverEng). Press can be reached at [press@clover.com](mailto:press@clover.com)._
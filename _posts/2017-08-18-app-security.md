---
layout: post
title:  "Why you should think about webapps security"
date:   2017-08-18 9:12:39 +0100
categories: jekyll update
image: assets/images/pic08.jpg
description: "Take care of users data"

---

I have been recently adding a [Stripe][stripe] payment method to an existing website. When dealing with sensitive informations such as credit card data, one should take time to think about the possible security flaws when designing the payment flow.
Here are the best practices I have been following until now : 

### 1 - Never trust user input

Stripe proposes a very useful tool called [Checkout][checkout] : it provides the user with a clean and easy-to-use payment flow, taking care of most of the security steps.
But, and it's a bit tricky, one has to provide the Chekout component with the amount of the charge, to tell the customer how much he will have to pay. It is tempting to send this amount from the customer's browser back to the server, since it's already ready to use.

But, and this is a real issue, the customer could change this amount (in the chrome console for example) for 0 and pay nothing ! That's why the server should compute again the price to pay, according to the customer's consumption.

### 2 - HTTPS only makes the developer happy

The Stripe flow is kinda simple  : the customer provide its credit card informations to the checkout component, which sends them securely to the Stripe API in exchange of a one-time token. The token should then be passed back to our server where it'll be used to charge the customer. 
As a consequence, this flow should be fully encrypted to avoid possible man-in-the middle attack. By hijacking the one-time token, an attacker could charge the client with its account and retrieve his money, and you really don't want that ;)

### 3 - Read the docs

When using a framework, there is often a portion dedicated to security : reading it carefully will avoid you serious trouble, as you'll learn to protect yourself again many commons security flaws (CSRF attacks, sensitive data exposure,...).


[checkout]: https://stripe.com/docs/checkout
[stripe]: https://stripe.com

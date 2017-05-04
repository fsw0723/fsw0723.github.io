---
layout: post
title: "OAuth2 & Alexa account linking"
date: 2017-05-02 23:33:00 +0800
categories: others
---

I am working on Alexa account linking recently. 
Alexa account linking is based on standard OAuth2.
By linking Alexa with third-party application, Alexa is able to answer questions related to your account information.

Some readings about Alexa account linking:

* [Youtube](https://www.youtube.com/watch?v=mO0gZPeR45o)
* [Documentation](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/linking-an-alexa-user-with-a-user-in-your-system)
* [Code](https://github.com/bignerdranch/developing-alexa-skills-solutions/tree/master/5_accountLinking/solution)

About OAuth2

* [OAuth2](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)

As we need to allow individual users to access their personal information, user based token is required.
Thus Alexa account linking is using 3-legged OAuth flow. 
A typical 3-legged OAuth flow is as follows.

(picture here...)

Alexa supports two types of OAuth authorization grants: implicit grant & authorization code grant. 
Authorization code grant is suggested and it is able to refresh access token upon expiration.

## Auth code grant

Taking the easiest one for example, link your Alexa skill with Amazon login, where no extra code is required. 
[Tutorial here](https://developer.amazon.com/blogs/post/Tx3CX1ETRZZ2NPC/Alexa-Account-Linking-5-Steps-to-Seamlessly-Link-Your-Alexa-Skill-with-Login-wit)

In this example, suppose you already have a Amazon security profile client ID & client secret, what you need is only to fill in the following information:

* A authorization url to open Amazon grant access page where user can allow/deny account linking
* client id & client secret
* Access token URI
* In Amazon login case, scope is also required


Alexa will provide 2 redirection urls, e.g. https://pitangui.amazon.com/api/skill/link/A1234567.
Use one of them as the *redirection url* for Amazon security profile.

With all the setup above, when user request an account linking, Alexa will:

1. Open the Amazon grant access page which is defined as the **Authorization URL**.
2. Once the access is allowed, the page will be redirected to the **redirection url** with authorization code.
3. Immediately Alexa uses this authorization code, together with client ID & client secret to send a request to **Access token URI** 
4. Access token URI will respond with access token, refresh token, expires and some additional information back to Alexa. 
Account linking can now be successful.

To be continued...











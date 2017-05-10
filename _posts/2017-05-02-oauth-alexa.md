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

![3-legged Oauth flow](/assets/oauth/oauth1.png){:class="img-responsive"}

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

I mentioned this as the easiest one as it can be done by configuration only, 
since the request and response format for both Alexa and Amazon side can be matched.

However, in a lot cases, Alexa and authorization server's requests & responses format cannot match,
this is when middleware is needed. The new flow will look like below (top to bottom):

![Auth code grant with middleware](/assets/oauth/oauth2.png){:class="img-responsive"}

In details, when account linking starts, it will:

1. Alexa calls **Authorization URL**, which is under middleware server, 
passing state, client_id, redirect_uri and other parameters that are defined in the configuration.
2. Middleware gets the request, saves redirect_uri & state(if not available in the authorization response),
and redirect to authorization server withe client_id.
3. After user grants access, authorization server returns authorization code.
The redirect url for authorization server now is pointing to middleware server.
Middleware gets the authorization code and pass back to Alexa with code & state as parameter.
4. Alexa will send out another request to **Accesss Token URI**, which is again point to middleware here.
5. Middleware parse the request to the format that authorization server requires and redirect to authorization server.
6. Once authorization success, the server will return access token & refresh token in standard OAuth2 format.
 Alexa will show the success message once it receives the access token.
 
## Implicit grant

 
![Implicit grant with middleware](/assets/oauth/oauth3.png){:class="img-responsive"}

For implicit grant, the first part of getting authorization code is the same as Auth code grant.

After authorization code is returned to middleware from authorization server, 
the middleware will fetch access token directly instead of returning back to Alexa.
From this stage, the process is:

1. Middleware construct request to get access token, with the authorization code.
2. Authorization server responses with access token.
3. Using **Redirect URI**, access token and state, middleware redirects back to Alexa.
The redirect url will be something like this: 
```
https://pitangui.amazon.com/spa/skill/account-linking-status.html?vendorId=AAAAAAAAAAAAAA#state=xyz&access_token=2YotnFZFEjr1zCsicMWpAA&token_type=Bearer
```

Note that you must pass back parameters including *state*, *access_token* and *token_type* are in the URL fragment portion of the URL. This portion is appended to redirect uri using hashtag (#).


### PS:

I tried to use the redirect URI provided on Alexa skill configuration page but always gets an empty page after the redirection with access token.
Not sure what is the reason. It works after using the redirect uri provided when Alexa calls authorization url.

Feedback welcome.

 
 
 

    











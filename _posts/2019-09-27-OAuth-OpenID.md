---
title: "OAuth and OpenID"
layout: post
date: 2019-09-27
headerImage: false
tag:
- markdown
- components
- extra
category: blog
author: YY
description: Markdown summary with different options
---

## OAuth 2.0

### Terminologies

- Resource Owner: the user
- Client: client app/front-end, eg. yelp.com
- Authorizaion Server: eg. accounts.google.com
- Resource Server: eg. contacts.google.com
- Authorization Grant: resource owner granting permission, eg. Allow Yelp to access your public profile and contacts?
- Access Token: token needed to talk with resource server
- Scope: eg. email.read, 
- Consent
- Back Channel (highly secure channel)
- Front Channel (less secure channel)

### Example

![OAuth 2.0 Flow - Authorization code](../assets/images/OAuth.png)

1. Starting the flow

```
https://accounts.google.com/o/oauth2/v2/auth?
 client_id     = abc123&
 redirect_uri  = https://yelp.com/callback&
 scope         = profile&
 response_type = code&
 state         = foobar
```

Note: You use `state` to identify that the callback from the authorization server matches the request sent. If there wasn't `state`, a attacker could just call your callback url with a random access token that you didn't request. With `state` you know that the called callback is in response to the request you made.

2. Calling back

```
https://yelp.com/callback?
 error             = access_denied&
 error_description = The user did not consent.
```

```
https://yelp.com/callback?
 code             = oMasIaQmq23Tp13&
 state = foobar
```

3. Exchange code for an access token

```
POST www.googleapis.com/oauth2/v4/token
Content-Type: application/x-www-form-urlencoded

code          = oMasIaQmq23Tp13&
cliend_id     = abc123&
client_secret = secret123&
grant_type    = authorization_code
```

4. Authorization server returns an access token

```
{
    "access_token": "fFAGRdJurlFtz70BzhT3dg",
    "expires_in"  : 3920,
    "token_type"  : "Bearer",
}
```

5. Use the access token

```
GET api.google.com/some/endpoint
Authorization: Bearer fFAGRdJurlFtz70BzhT3dg
```

The resource server would `Validate Token` and `Use token scope for authorization`.

## OpenID Connect

![OAuth misused in different senarios](../assets/images/misuse.png)

### Problems before OpenID Connect

1. No standard way to get the user's info.
2. Every implementation is a littile different.
3. No common set of scropes.

### Solution

- OpenID Connect is for `authentication`
- OAuth 2.0 is for `authorization`

### What OpenID Connect adds

- ID token
- UserInfo endpoint for getting more user info
- Standard set of scopes
- Standarlized implementation

### Example

![OpenID Example](../assets/images/OpenID.png)

1. Start the flow

```
https://accounts.google.com/o/oauth2/v2/auth?
 client_id     = abc123&
 redirect_uri  = https://yelp.com/callback&
 scope         = openid profile&
 response_type = code&
 state         = foobar
```

2. Exchange code for access token and ID token

```
POST www.googleapis.com/oauth2/v4/token
Content-Type: application/x-www-form-urlencoded

code          = oMasIaQmq23Tp13&
cliend_id     = abc123&
client_secret = secret123&
grant_type    = authorization_code
```

3. Authorization server returns access and ID tokens

```
{
    "access_token": "fFAGRdJurlFtz70BzhT3dg",
    "id_token"    : "eyJraB03ds3F...",
    "expires_in"  : 3920,
    "token_type"  : "Bearer",
}
```

Note: ID token is usually JSON Web Token (JWT).

### OpenID changes the situation

![OpenID Example](../assets/images/OpenID_today.png)

### Use OAuth 2.0 for Authorization

- Granting access to API
- Getting access to user data in other systems

### Use OpenID Connect for Authentication:

- Logging the user in
- Making your accounts available in other systems

## Reference

1. [OAuth_and_OpenID_Connect_in_plain_English_v1.6__KCDC_.pdf](../assets/OAuth_and_OpenID_Connect_in_plain_English_v1.6__KCDC_.pdf)
2. [OAuth 2.0 and OpenID Connect](https://www.youtube.com/watch?v=996OiexHze0)
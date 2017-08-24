---
title: API Reference

language_tabs:
  - shell
  - javascript
  - swift
  - java

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - thumbor
  - cards
  - comments
  - conversations
  - events
  - eventrooms
  - like
  - map
  - mobile
  - questions
  - requests
  - responses
  - search
  - themes
  - translate
  - users
  - notifications
  - entities
  - errors
  - changelog

search: true
---

# Introduction

Welcome to the uCiC API! You can use our API to access uCiC API endpoints, which can return information on various themes, cards, and media in our database.

We presently only have language bindings in Shell. You can view code examples in the dark area to the right.


# Authentication

> An authenticated request looks like this

```shell
# With shell, you can just pass the correct header with each request
curl "https://node.ucic.vc/api/v05/user/get" -H "Authorization: <AUTHORIZATION_TOKEN>"
```

> Make sure to replace `<AUTHORIZATION_TOKEN>` with your access token.

uCiC uses auth tokens to allow access to the API. You can obtain a new auth token with a login request.

uCiC expects your authorization token to be included in all API requests to the server in a header that looks like the following:

`Authorization: <AUTHORIZATION_TOKEN>`

<aside class="notice">
You must replace <code>&lt;AUTHORIZATION_TOKEN&gt;</code> with your personal access token.
</aside>

# Idempotency

> An idempotent request looks like this

```shell
curl -X POST -H "Authorization: <AUTHORIZATION_TOKEN>" -H "Content-Type: application/json" -H "Idempotency-Key: iuovbzsafgQfSDdasd" -d '{ "text": "Adding an idempotent comment to a card" }' "https://node.ucic.vc/api/v05/card/DEC604AC-C29F-4764-B9C6-2CEC7351ABB6/comments"
```

Idempotency is supported for retrying POST requests.  To make an idempotent request, add the Idempotency-Key header with a string value.  This key along with the user, route, and response are stored in redis.  If the provided idempotency key for the same user and route is found in redis, the cached response is returned (instead of processing the request).  Redis will expire the key after 24 hours.

### Header Parameter
| Paramter        | Type   | Description                              |
| --------------- | ------ | ---------------------------------------- |
| Idempotency-Key | String | The client generated idempotency key for the provided post request |

### Response Codes
| Paramter    | Type | Description                              |
| ----------- | ---- | ---------------------------------------- |
| Retry-After | 503  | if an Idempotent request matching an existing Idempotent request which is still being processed arrives, a Retry-After 503 is returned requesting that the request wait until the prior idempotent request completes. |

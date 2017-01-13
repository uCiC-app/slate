---
title: API Reference

language_tabs:
  - shell
  - javascript

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - cards
  - comments
  - conversations
  - events
  - map
  - requests
  - themes
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


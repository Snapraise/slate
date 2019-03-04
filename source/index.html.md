---
title: Snap Advance API Documentation

language_tabs:
  - shell

toc_footers:
  - <a href='mailto:support@amploadvance.com'>Contact Support For API Access</a>

includes:
  - campaigns
  - users
  - donations
  - webhooks
  - errors


search: true
---

# Introduction

Welcome to the Snap Advance API!  You can use our HTTP API to perform basic Create,
Read, Update and Delete (CRUD) actions on various Campaign related data points
inside the Snap Advance system.

The Snap Advance API is currently in pre-release.  During pre-release, features and functionality
may change, including breaking changes.  Once pre-release is complete and we have an official
point release, all future changes made on the versioned namespace (i.e., /v1/) will
be fully backwards compatible.  

Future functionality may also include language wrappers for the API.

The Snap Advance API follows the [JSON API Specification Format](http://jsonapi.org/).
If there are any discrepancies with compatibility, please report it by contacting support.


# Rate Limits

The Snap Advance API has an exponential backoff rate limit.  Generally speaking, every
API token will be allowed approximately 1 request per second.  However, waiting
1 second between API requests isn't always a realistic or convenient way to request
data, so you will be able to make multiple simultaneous or back-to-back requests,
as long as there's a subsequent cooldown time such that it levels out to approximately
1 request per second over a longer period of time.  

The exact rate limit depends heavily on usage patterns.  To phrase this another way,
the rate limit is built to discourage thousands of simultaneous requests that all
occur at the same time (hourly, for example), and instead better support smaller
activity patterns that occurs over shorter, more regular intervals.

Best practices here to prevent rate limiting issues would be to make use of the
`last_updated_*` request parameters in order to ensure you're only grabbing the data you
need.

We do this in order to preserve the integrity of the donations coming into the system.
We want to ensure system resources are going to the right place - ensuring your
giving day is successful.


# Authentication

```shell
curl "https://api.amploadvance.com/v1/campaigns"
  -H "Authorization: Token token=12345123451234512345"
```


Please <a href="mailto:support@amploadvance.com">contact support</a> to have an
API key provisioned for you.

Snap Advance expects for the API key to be included in all API requests to the server
in a header that looks like the following:

`Authorization: Token token=12345123451234512345`

<aside class="notice">
You must replace <code>12345123451234512345</code> with your personal API key.
</aside>

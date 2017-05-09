---
title: Amplo API Documentation

language_tabs:
  - shell

toc_footers:
  - <a href='mailto:support@amploadvance.com'>Contact Support For API Access</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Amplo API!  You can use our HTTP API to perform basic Create,
Read, Update and Delete (CRUD) actions on various Campaign related data points
inside the Amplo system.

The Amplo API is currently in pre-release.  During pre-release, features and functionality
may change, including breaking changes.  Once pre-release is complete and we have an official
point release, all future changes made on the versioned namespace (i.e., /v1/) will
be fully backwards compatible.  

Future functionality may also include language wrappers for the API.

The Amplo API follows the [JSON API Specification Format](http://jsonapi.org/).
If there are any discrepancies with compatibility, please report it by contacting support.


# Rate Limits

The Amplo API has an exponential backoff rate limit.  Generally speaking, every
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
curl "https://app.amploadvance.com/api/v1/campaigns"
  -H "Authorization: 12345123451234512345"
```


Please <a href="mailto:support@amploadvance.com">contact support</a> to have an
API key provisioned for you.

Amplo expects for the API key to be included in all API requests to the server
in a header that looks like the following:

`Authorization: 12345123451234512345`

<aside class="notice">
You must replace <code>12345123451234512345</code> with your personal API key.
</aside>

# Campaigns

## List Campaigns


```shell
curl "https://app.amploadvance.com/api/v1/campaigns"
  -H "Authorization: 12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "asdfasdfasdfasdf",
      "name": "Amplo University Campaign 1",
      "url": "https://amplouniversity.com/pages/campaign-1-page",
      "start_date": 1494278379,
      "end_date": 149428000,
      "status": "active",
      "total_votes": 10,
      "total_donations": 10,
      "total_raised": 300,
      "external_id": "abc_123"
    },
    {
      "id": "111222333444555",
      "name": "Amplo University Campaign 2",
      "url": "https://amplouniversity.com/pages/campaign-2-page",
      "start_date": 1494278379,
      "end_date": 149428000,
      "status": "active",
      "total_votes": 11,
      "total_donations": 11,
      "total_raised": 270,
      "external_id": "abc_123"
    }
  ],
  "meta":{
    "pages": 1,
    "count": 2,
    "per_page": 100
  }
}
```

This endpoint retrieves all campaigns.

### HTTP Request

`GET https://app.amploadvance.com/api/v1/campaigns`

### GET Parameters

Parameter | Default | Required? | Type | Description
--------- | ------- | --------- | ---- | -----------
page | 0 | false | **integer** | Page number.  Increment and call again to fetch more Campaigns if there are multiple pages in the results.

<aside class="success">
On the Amplo API, the first page is page number 0!
</aside>

## Get a Specific Campaign

```shell
curl "https://app.amploadvance.com/api/v1/campaigns/abcdefabcedfabcedf"
  -H "Authorization: 12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "111222333444555",
    "type": "campaign",
    "attributes": {
      "name": "Amplo University Campaign 2",
      "url": "https://amplouniversity.com/pages/campaign-2-page",
      "logo": "https://amplouniversity.com/logo.png",
      "start_date": 1494278379,
      "end_date": 149428000,
      "status": "active",
      "category": "Student Clubs and Organizations",
      "campaign_type": "dollars",
      "allow_subscriptions": true,
      "total_votes": 11,
      "total_donations": 11,
      "total_raised": 270,
      "average_donation": 25,
      "join_code": 123456,
      "external_id": "abc_123",
      "goal": 1000,
      "member_goal": 20,
      "public": true
    }
  }
}
```

This endpoint retrieves a specific campaign.

### HTTP Request

`GET https://app.amploadvance.com/api/v1/campaigns/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Campaign to retrieve

# Users

## Get a Specific User By Email

```shell
curl "https://app.amploadvance.com/api/v1/users/api@amploadvance.com"
  -H "Authorization: 12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "111222333444555",
    "type": "user",
    "attributes": {
      "first_name": "Joe",
      "last_name": "Smith",
      "email": "api@amploadvance.com",
      "external_id": "1234_asdf",
      "donations": {
        "data": [{
          "id": "aabbccddeeffgg",
          "type": "donation",
          "attributes": {
            "beneficiary_type": "Campaign",
            "beneficiary_id": "111222333444555",
            "amount": 10,
            "status": "paid",
            "public": true,
            "donation_type": "cc",
            "external_id": "import_1234",
            "recurring": false
          }
        }]
      }
    }
  }
}
```

This endpoint retrieves a specific User by email address.  The purpose of this endpoint
is User validation and existence checking.

The Donations array returned with this User provides the same fields that the Donation list
endpoint provides.  To find more detail on a Donation, use the Donation show endpoint.  

### HTTP Request

`GET https://app.amploadvance.com/api/v1/users/<EMAIL>`

### URL Parameters

Parameter | Description
--------- | -----------
EMAIL | The full, unescaped email address for this User.

## Create a New User

```shell
curl "https://app.amploadvance.com/api/v1/users"
  -XPOST
  -d 'first_name=Joe'
  -d 'last_name=Smith'
  -d 'email=api@amploadvance.com'
  -d 'external_id=1234_asdf'
  -H "Authorization: 12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data":{
    "id": "111222333444555",
    "type": "user",
    "attributes": {
      "first_name": "Joe",
      "last_name": "Smith",
      "email": "api@amploadvance.com",
      "external_id": "1234_asdf"
    }
  }
}
```

This endpoint retrieves a specific User by email address.  The purpose of this endpoint
is User validation and existence checking.

The Donations array returned with this User provides the same fields that the Donation list
endpoint provides.  To find more detail on a Donation, use the Donation show endpoint.  

### HTTP Request

`POST https://app.amploadvance.com/api/v1/users`

### HTTP POST Parameters

Parameter | Required? | Type | Description
--------- | --------- | ---- | -----------
email | true | **string** | The full, unescaped email address for this User.
first_name | true | **string** | User first name
last_name | true | **string** | User last name
external_id | false | **string** | External ID can be used to link this User to another external software system for recordkeeping purposes.





# Donations

## List Donations


```shell
curl "https://app.amploadvance.com/api/v1/donations"
  -H "Authorization: 12345123451234512345"
```

```shell
curl "https://app.amploadvance.com/api/v1/campaigns/asdfasdfasdfasdf/donations"
  -H "Authorization: 12345123451234512345"
```

> The above commands returns JSON structured like this:

```json
{
  "data":[
    {
      "id": "aabbccddeeffgg",
      "type": "donation",
      "attributes": {
        "beneficiary_type": "Campaign",
        "beneficiary_id": "111222333444555",
        "amount": 10,
        "status": "paid",
        "public": true,
        "donation_type": "cc",
        "external_id": "import_1234",
        "recurring": false
      }
    },
    {
      "id": "11223344556677",
      "type": "donation",
        "attributes": {
        "beneficiary_type": "Campaign",
        "beneficiary_id": "111222333444555",
        "amount": 7,
        "status": "paid",
        "public": true,
        "donation_type": "cc",
        "external_id": "import_abcde",
        "recurring": false
      }
    }
  ],
  "meta":{
    "pages": 1,
    "count": 2,
    "per_page": 100
  }
}
```

These endpoint retrieves a paginated list of donations.

### HTTP Request

This URL will fetch all donations for all Campaigns:
`GET https://app.amploadvance.com/api/v1/donations`

This URL will fetch only donations made towards a specific Campaign:
`GET https://app.amploadvance.com/api/v1/campaigns/<CAMPAIGN_ID>/donations`

### URL Parameters

Campaign ID is only required when using the second URL.

Parameter | Required? | Type | Description
--------- | --------- | ---- | -----------
CAMPAIGN_ID | true | **string** | Campaign ID; obtained from Campaign list.

### GET Parameters

The `last_updated_*` parameters are used to help reduce the number of API requests send to
Amplo's API.  Best practices here would be for you to track the timestamp of the last time a
Donations list request was made, and only request donations that have been updated since then.

`last_updated_end` is not required and will always default to the timestamp at which
the request was made, but to avoid any possibility of donations falling through the
cracks that could be opened up in the few milliseconds of request round trip time,
we suggest setting this to an explicit value.   

Note that we are filtering Donations by their last updated at timestamp.  This means that
the list will not necessarily be full of new Donations.  For example, if a Donation gets
refunded, it will also show up in the list for you to possibly take action on.  

The Donations lists will always only show the most recent 100 Donations and the
response metadata will reflect only one page of results with only up to 100 entries.
However, if both `last_updated_start` and `last_updated_end` are provided, you will
be able to paginate through results using the `page` parameter if there are more than
100 entries.

Parameter | Required? | Default | Type | Description
--------- | --------- | ------- | ---- | -----------
last_updated_start | false | 0 |  **timestamp** | UNIX Timestamp used to limit the list of Donations.
last_updated_end | false | current timestamp | **timestamp** | UNIX Timestamp used to limit the list of Donations.
page | false | 0 |  **integer** | The results page; used to


## Get a Specific Donation

```shell
curl "https://app.amploadvance.com/api/v1/donations/abcdefabcedfabcedf"
  -H "Authorization: 12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "aabbccddeeffgg",
    "type": "donation",
    "attributes":{
      "user_id": "1122334455667788",
      "beneficiary_type": "Campaign",
      "beneficiary_id": "111222333444555",
      "amount": 10,
      "status": "paid",
      "public": true,
      "donation_type": "cc",
      "external_id": "import_1234",
      "recurring": false,
      "auth_code": "123456",
      "transact_id": "abcdefg",
      "note": "I love Amplo U",
      "check_number": null,
      "credit_card_fingerprint": "aaaaabbbbbcccccdddddeeeee",
      "tickets": [],
      "refunded": false,
      "refundable": true,
      "refund_donation_ids": [],
      "appeal": null,
      "causes_allocated_to": []
    }
  }

}
```

This endpoint retrieves a specific Donation.

### HTTP Request

`GET https://app.amploadvance.com/api/v1/donations/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Campaign to retrieve

## Create a New Donation

```shell
curl "https://app.amploadvance.com/api/v1/campaigns/111222333444555/donations"
  -XPOST
  -d 'user_id=aabbccddeeffgg'
  -d 'external_id=1234_asdf'
  -d 'amount=10'
  -d 'status=paid'
  -d 'donation_type=cash'
  -d 'public=true'
  -H "Authorization: 12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "09876543210987654321",
    "type": "donation",
    "attributes": {
      "user_id": "aabbccddeeffgg",
      "amount": 10,
      "status": "paid",
      "public": true,
      "donation_type": "cash",
      "external_id": "import_asdf",
      "recurring": false,
      "auth_code": null,
      "transact_id": null,
      "note": null,
      "check_number": null,
      "credit_card_fingerprint": null,
      "tickets": [],
      "refunded": false,
      "refundable": true,
      "refund_donation_ids": [],
      "appeal": null,
      "causes_allocated_to": []
    }
  }
}
```

This endpoint creates a new Donation in Amplo.  A few assumptions are made:

 * The status of the Donation created will always be "paid".
 * The Donation is non-recurring.

### HTTP Request

`POST https://app.amploadvance.com/api/v1/campaigns/<CAMPAIGN_ID>/donations`

### URL Parameters

Parameter | Description
--------- | -----------
CAMPAIGN_ID | The ID of the Campaign this Donation belongs to

### HTTP POST Parameters

Parameter | Required? | Type | Description
--------- | --------- | ---- | -----------
user_id | true | **string** | The Amplo User ID associated with the User who made this Donation.
amount | true | **float** | Donation amount in dollars
donation_type | true | **string** | Donation Type - Can be "cc", "cash", or "check"
public | false | **boolean** | Is this Donation public?  Defaults to true.
external_id | false | **string** | External ID can be used to link this Donation to another external software system for recordkeeping purposes.


# Campaigns

## List Campaigns


```shell
curl "https://api.amploadvance.com/v1/campaigns"
  -H "Authorization: Token token=12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "asdfasdfasdfasdf",
      "type": "campaigns",
      "attributes": {
        "name": "Snap Advance University Campaign 1",
        "url": "https://amplouniversity.com/pages/campaign-1-page",
        "start_date": 1494278379,
        "end_date": 149428000,
        "status": "active",
        "total_votes": 10,
        "total_donations": 10,
        "total_raised": 300,
        "external_id": "abc_123"
      }
    },
    {
      "id": "111222333444555",
      "type": "campaigns",
      "attributes": {
        "name": "Snap Advance University Campaign 2",
        "url": "https://amplouniversity.com/pages/campaign-2-page",
        "start_date": 1494278379,
        "end_date": 149428000,
        "status": "active",
        "total_votes": 11,
        "total_donations": 11,
        "total_raised": 270,
        "external_id": "abc_123"
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

This endpoint retrieves all campaigns.

### HTTP Request

`GET https://api.amploadvance.com/v1/campaigns`

### GET Parameters

Parameter | Default | Required? | Type | Description
--------- | ------- | --------- | ---- | -----------
page | 0 | false | **integer** | Page number.  Increment and call again to fetch more Campaigns if there are multiple pages in the results.

Default Sort Order: The object's creation date, ascending.

<aside class="success">
On the Snap Advance API, the first page is page number 0!
</aside>

## Get a Specific Campaign

```shell
curl "https://api.amploadvance.com/v1/campaigns/abcdefabcedfabcedf"
  -H "Authorization: Token token=12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "abcdefabcedfabcedf",
    "type": "campaigns",
    "attributes": {
      "name": "Snap Advance University Campaign 2",
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

`GET https://api.amploadvance.com/v1/campaigns/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Campaign to retrieve

# Donations

## List Donations


```shell
curl "https://api.amploadvance.com/v1/donations"
  -H "Authorization: Token token=12345123451234512345"
```

```shell
curl "https://api.amploadvance.com/v1/campaigns/asdfasdfasdfasdf/donations"
  -H "Authorization: Token token=12345123451234512345"
```

> The above commands returns JSON structured like this:

```json
{
  "data":[
    {
      "id": "aabbccddeeffgg",
      "type": "donations",
      "attributes":{
        "beneficiary_type": "Campaign",
        "beneficiary_id": "111222333444555",
        "beneficiary_name": "campaign name",
        "parent_beneficiary_name": "campaign name of the parent campaign",
        "amount": 10,
        "status": "paid",
        "public": true,
        "donation_type": "cc",
        "external_id": "import_1234",
        "recurring": false,
        "auth_code": "123456",
        "transact_id": "abcdefg",
        "note": "I love Snap Advance U",
        "check_number": null,
        "credit_card_fingerprint": "aaaaabbbbbcccccdddddeeeee",
        "tickets": [],
        "refunded": false,
        "refundable": true,
        "refund_donation_ids": [],
        "appeal": null,
        "affinities": "alumni, parents",
        "grad_year": "1983",
        "on_behalf_of": null,    
        "company_name": "microsoft",    
        "joint_gift_name": null,    
        "in_memory_honor": null,    
        "in_memory_honor_notes": null,    
        "donor_first_name": "John",
        "donor_last_name": "Smith",
        "donor_email": "test@test.com",
        "donor_phone": "123-123-1234",
        "donor_address1": "1234 Main St",
        "donor_address2": null,
        "donor_address3": null,
        "donor_city": "Chicago",
        "donor_region": "IL",
        "donor_zip": "12345",
        "donor_country": "United States",
        "donor_country_code": "USA",
        "card_last_4": "4242",
        "recurring": false,
        "created_at": 1498806295,
        "causes":{
          "data": [{
            "id": "000999888777",
            "type": "causes",
            "attributes": {
              "name": "Cause Name 1",
              "external_id": "0001234",
              "amount": 10
            }
          }]
        }
      }
    },
    {
      "id": "11223344556677",
      "type": "donations",
      "attributes":{
        "beneficiary_type": "Campaign",
        "beneficiary_id": "111222333444555",
        "beneficiary_name": "campaign name",
        "parent_beneficiary_name": "campaign name of the parent campaign",
        "amount": 10,
        "status": "paid",
        "public": true,
        "donation_type": "cc",
        "external_id": "import_1234",
        "recurring": false,
        "auth_code": "123456",
        "transact_id": "abcdefg",
        "note": "I love Snap Advance U",
        "check_number": null,
        "credit_card_fingerprint": "aaaaabbbbbcccccdddddeeeee",
        "tickets": [],
        "refunded": false,
        "refundable": true,
        "refund_donation_ids": [],
        "appeal": null,
        "affinities": "alumni, parents",
        "grad_year": "1983",
        "on_behalf_of": null,    
        "company_name": "microsoft",    
        "joint_gift_name": null,    
        "in_memory_honor": null,    
        "in_memory_honor_notes": null,    
        "donor_first_name": "John",
        "donor_last_name": "Smith",
        "donor_email": "test@test.com",
        "donor_phone": "123-123-1234",
        "donor_address1": "1234 Main St",
        "donor_address2": null,
        "donor_address3": null,
        "donor_city": "Chicago",
        "donor_region": "IL",
        "donor_zip": "12345",
        "donor_country": "United States",
        "donor_country_code": "USA",
        "card_last_4": "4242",
        "recurring": false,
        "created_at": 1498806295,
        "causes":{
          "data": [{
            "id": "000999888777",
            "type": "causes",
            "attributes": {
              "name": "Cause Name 1",
              "external_id": "0001234",
              "amount": 10
            }
          }]
        }
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

`GET https://api.amploadvance.com/v1/donations`

This URL will fetch only donations made towards a specific Campaign:

`GET https://api.amploadvance.com/v1/campaigns/<CAMPAIGN_ID>/donations`

### URL Parameters

Campaign ID is only required when using the second URL.

Parameter | Required? | Type | Description
--------- | --------- | ---- | -----------
CAMPAIGN_ID | true | **string** | Campaign ID; obtained from Campaign list.

### GET Parameters

The `last_updated_*` parameters are used to help reduce the number of API requests send to
Snap Advance's API.  Best practices here would be for you to track the timestamp of the last time a
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

Default Sort Order: The Object's last updated at timestamp in descending order.

## Get a Specific Donation

```shell
curl "https://api.amploadvance.com/v1/donations/abcdefabcedfabcedf"
  -H "Authorization: Token token=12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "aabbccddeeffgg",
    "type": "donations",
    "attributes":{
      "beneficiary_type": "Campaign",
      "beneficiary_id": "111222333444555",
      "beneficiary_name": "campaign name",
      "parent_beneficiary_name": "campaign name of the parent campaign",
      "amount": 10,
      "status": "paid",
      "public": true,
      "donation_type": "cc",
      "external_id": "import_1234",
      "recurring": false,
      "auth_code": "123456",
      "transact_id": "abcdefg",
      "note": "I love Snap Advance U",
      "check_number": null,
      "credit_card_fingerprint": "aaaaabbbbbcccccdddddeeeee",
      "tickets": [],
      "refunded": false,
      "refundable": true,
      "refund_donation_ids": [],
      "appeal": null,
      "affinity": "alumni",
      "grad_year": "1983",
      "on_behalf_of": null,    
      "company_name": "microsoft",    
      "joint_gift_name": null,    
      "in_memory_honor": null,    
      "in_memory_honor_notes": null,    
      "donor_first_name": "John",
      "donor_last_name": "Smith",
      "donor_email": "test@test.com",
      "donor_phone": "123-123-1234",
      "donor_address1": "1234 Main St",
      "donor_address2": null,
      "donor_address3": null,
      "donor_city": "Chicago",
      "donor_region": "IL",
      "donor_zip": "12345",
      "donor_country": "United States",
      "donor_country_code": "USA",
      "card_last_4": "4242",
      "recurring": false,
      "created_at": 1498806295,
      "causes":{
        "data": [{
          "id": "000999888777",
          "type": "causes",
          "attributes": {
            "name": "Cause Name 1",
            "external_id": "0001234",
            "amount": 10
          }
        }]
      }
    }
  }

}
```

This endpoint retrieves a specific Donation.

### HTTP Request

`GET https://api.amploadvance.com/v1/donations/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Campaign to retrieve

## Create a New Donation

```shell
curl "https://api.amploadvance.com/v1/campaigns/111222333444555/donations"
  -XPOST
  -d 'user_id=aabbccddeeffgg'
  -d 'external_id=1234_asdf'
  -d 'amount=10'
  -d 'status=paid'
  -d 'donation_type=cash'
  -d 'public=true'
  -H "Authorization: Token token=12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "09876543210987654321",
    "type": "donations",
    "attributes":{
      "beneficiary_type": "Campaign",
      "beneficiary_id": "111222333444555",
      "beneficiary_name": "campaign name",
      "parent_beneficiary_name": "campaign name of the parent campaign",
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
      "affinities": "alumni, parents",
      "grad_year": "1983",
      "on_behalf_of": null,    
      "company_name": "microsoft",    
      "joint_gift_name": null,    
      "in_memory_honor": null,    
      "in_memory_honor_notes": null,    
      "donor_first_name": "John",
      "donor_last_name": "Smith",
      "donor_email": "test@test.com",
      "donor_phone": "123-123-1234",
      "donor_address1": "1234 Main St",
      "donor_address2": null,
      "donor_address3": null,
      "donor_city": "Chicago",
      "donor_region": "IL",
      "donor_zip": "12345",
      "donor_country": "United States",
      "donor_country_code": "USA",
      "card_last_4": "4242",
      "recurring": false,
      "created_at": 1498806295,
      "causes":{
        "data": [{
          "id": "000999888777",
          "type": "causes",
          "attributes": {
            "name": "Cause Name 1",
            "external_id": "0001234",
            "amount": 10
          }
        }]
      }
    }
  }
}
```

This endpoint creates a new Donation in Snap Advance.  A few assumptions are made:

 * The status of the Donation created will always be "paid".
 * The Donation is non-recurring.

### HTTP Request

`POST https://api.amploadvance.com/v1/donations`

### HTTP POST Parameters

Parameter | Required? | Type | Description
--------- | --------- | ---- | -----------
user_id | true | **string** | The Snap Advance User ID associated with the User who made this Donation.
campaign_id | true | **string** | The Snap Advance Campaign ID associated with the Campaign to which this Donation was made.
amount | true | **float** | Donation amount in dollars
public | false | **boolean** | Is this Donation public?  Defaults to true.
external_id | false | **string** | External ID can be used to link this Donation to another external software system for recordkeeping purposes.

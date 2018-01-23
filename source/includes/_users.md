
# Users

## Get a Specific User By Email

```shell
curl "https://api.amploadvance.com/v1/users/api@amploadvance.com"
  -H "Authorization: Token token=12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "111222333444555",
    "type": "users",
    "attributes": {
      "first_name": "Joe",
      "last_name": "Smith",
      "email": "api@amploadvance.com",
      "external_id": "1234_asdf",
      "donations": {
        "data": [{
          "id": "aabbccddeeffgg",
          "type": "donations",
          "attributes":{
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

`GET https://api.amploadvance.com/v1/users/<EMAIL>`

### URL Parameters

Parameter | Description
--------- | -----------
EMAIL | The full, unescaped email address for this User.

## Create a New User

```shell
curl "https://api.amploadvance.com/v1/users"
  -XPOST
  -d 'first_name=Joe'
  -d 'last_name=Smith'
  -d 'email=api@amploadvance.com'
  -d 'external_id=1234_asdf'
  -H "Authorization: Token token=12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data":{
    "id": "111222333444555",
    "type": "users",
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

`POST https://api.amploadvance.com/v1/users`

### HTTP POST Parameters

Parameter | Required? | Type | Description
--------- | --------- | ---- | -----------
email | true | **string** | The full, unescaped email address for this User.
first_name | true | **string** | User first name
last_name | true | **string** | User last name
external_id | false | **string** | External ID can be used to link this User to another external software system for recordkeeping purposes.

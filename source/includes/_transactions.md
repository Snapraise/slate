# Transactions

## List Transactions


```shell
curl "https://api.amploadvance.com/v1/transactions"
  -H "Authorization: Token token=12345123451234512345"
```

> The above commands returns JSON structured like this:

```json
{
  "data":[
    {
      "id": "5a6686618ef88d008a44b47b",
      "type": "transaction-records",
      "attributes": {
        "entity-id": "547ca23d69702d745e040000",
        "gateway-id": null,
        "payment-profile-id": null,
        "transaction-id": null,
        "target-internal-transaction-id": null,
        "amount-cents": 520000,
        "amount-currency": "USD",
        "transaction-type": "charge",
        "most-recent-status": "success",
        "internal-transaction-id": "00000000-55bb-9f45-6970-2d269b002846",
        "gateway-transaction-id": null,
        "gateway-intermediary-transaction-id": null,
        "payment-profile-address-1": "1234 main st",
        "payment-profile-address-2": null,
        "payment-profile-city": "Seattle",
        "payment-profile-country": "United States",
        "payment-profile-first-name": "Jane",
        "payment-profile-last-name": "doe",
        "payment-profile-region": "WA",
        "payment-profile-type": "old-hist",
        "payment-profile-zipcode": null,
        "merchant-provided-customer-data": null,
        "merchant-provided-transaction-data": null,
        "merchant-provided-transaction-id": null,
        "created-at": 1136102400,
        "updated-at": 1136102400,
        "purchase-records": {
          "data": [
            {
              "id": "5a6686618ef88d008a44c803",
              "type": "purchase_records",
              "attributes": {
                "amount-cents": 520000,
                "amount-currency": "USD",
                "purchase-record-type": "Donation",
                "purchaser-id": "55bb9f4569702d269b002845",
                "beneficiary-id": "558c240569702d1135000094",
                "beneficiary-type": "Campaign",
                "recipient-id": "55bb9f4569702d269b002845"
              }
            }
          ]
        }
      }
    },
    {
      "id": "5a6686618ef88d008a44b47a",
      "type": "transaction-records",
      "attributes": {
        "entity-id": "547ca23d69702d745e040000",
        "gateway-id": null,
        "payment-profile-id": null,
        "transaction-id": null,
        "target-internal-transaction-id": null,
        "amount-cents": 15000,
        "amount-currency": "USD",
        "transaction-type": "charge",
        "most-recent-status": "success",
        "internal-transaction-id": "00000000-55bb-9f45-6970-2d269b002844",
        "gateway-transaction-id": null,
        "gateway-intermediary-transaction-id": null,
        "payment-profile-address-1": null,
        "payment-profile-address-2": null,
        "payment-profile-city": null,
        "payment-profile-country": null,
        "payment-profile-first-name": null,
        "payment-profile-last-name": null,
        "payment-profile-region": null,
        "payment-profile-type": "old-hist",
        "payment-profile-zipcode": null,
        "payment-profile-credit-card-last-4-digits": null,
        "merchant-provided-customer-data": null,
        "merchant-provided-transaction-data": null,
        "merchant-provided-transaction-id": null,
        "created-at": 1136102400,
        "updated-at": 1136102400,
        "purchase-records": {
          "data": [
            {
              "id": "5a6686618ef88d008a44c802",
              "type": "purchase_records",
              "attributes": {
                "amount-cents": 15000,
                "amount-currency": "USD",
                "purchase-record-type": "Donation",
                "purchaser-id": "55bb9e7c69702d269b001cf4",
                "beneficiary-id": "558c240569702d1135000094",
                "beneficiary-type": "Campaign",
                "recipient-id": "55bb9e7c69702d269b001cf4"
              }
            }
          ]
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

These endpoint retrieves a paginated list of transactions.

### HTTP Request

This URL will fetch all Transactions in the system:

`GET https://api.amploadvance.com/v1/transactions`

### GET Parameters

The `last_updated_*` parameters are used to help reduce the number of API requests send to
Snap Advance's API.  Best practices here would be for you to track the timestamp of the last time a
Transaction list request was made, and only request transactions that have been updated since then.

`last_updated_end` is not required and will always default to the timestamp at which
the request was made, but to avoid any possibility of transactions falling through the
cracks that could be opened up in the few milliseconds of request round trip time,
we suggest setting this to an explicit value.   

Note that we are filtering Transactions by their last updated at timestamp.  This means that
the list will not necessarily be full of new Transactions.  For example, if a Transactions gets
refunded, it will also show up in the list for you to possibly take action on.  

The Transactions lists will always only show the most recent 100 Transactions and the
response metadata will reflect only one page of results with only up to 100 entries.
However, if both `last_updated_start` and `last_updated_end` are provided, you will
be able to paginate through results using the `page` parameter if there are more than
100 entries.

Parameter | Required? | Default | Type | Description
--------- | --------- | ------- | ---- | -----------
last_updated_start | false | 0 |  **timestamp** | UNIX Timestamp used to limit the list of Transactions.
last_updated_end | false | current timestamp | **timestamp** | UNIX Timestamp used to limit the list of Transactions.
page | false | 0 |  **integer** | The results page; used to

Default Sort Order: The Object's last updated at timestamp in descending order.

## Get a Specific Transaction

```shell
curl "https://api.amploadvance.com/v1/transactions/abcdefabcedfabcedf"
  -H "Authorization: Token token=12345123451234512345"
```

> The above command returns JSON structured like this:

```json
{
  "data":{
    "id": "5a6686618ef88d008a44b47b",
    "type": "transaction-records",
    "attributes": {
      "entity-id": "547ca23d69702d745e040000",
      "gateway-id": null,
      "payment-profile-id": null,
      "transaction-id": null,
      "target-internal-transaction-id": null,
      "amount-cents": 520000,
      "amount-currency": "USD",
      "transaction-type": "charge",
      "most-recent-status": "success",
      "internal-transaction-id": "00000000-55bb-9f45-6970-2d269b002846",
      "gateway-transaction-id": null,
      "gateway-intermediary-transaction-id": null,
      "payment-profile-address-1": "1234 main st",
      "payment-profile-address-2": null,
      "payment-profile-city": "Seattle",
      "payment-profile-country": "United States",
      "payment-profile-first-name": "Jane",
      "payment-profile-last-name": "doe",
      "payment-profile-region": "WA",
      "payment-profile-type": "old-hist",
      "payment-profile-zipcode": null,
      "merchant-provided-customer-data": null,
      "merchant-provided-transaction-data": null,
      "merchant-provided-transaction-id": null,
      "created-at": 1136102400,
      "updated-at": 1136102400,
      "purchase-records": {
        "data": [
          {
            "id": "5a6686618ef88d008a44c803",
            "type": "purchase_records",
            "attributes": {
              "amount-cents": 520000,
              "amount-currency": "USD",
              "purchase-record-type": "Donation",
              "purchaser-id": "55bb9f4569702d269b002845",
              "beneficiary-id": "558c240569702d1135000094",
              "beneficiary-type": "Campaign",
              "recipient-id": "55bb9f4569702d269b002845"
            }
          }
        ]
      }
    }
  }
}
```

This endpoint retrieves a specific Transaction.

### HTTP Request

`GET https://api.amploadvance.com/v1/transactions/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Transaction to retrieve

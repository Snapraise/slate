# Webhooks

> The following is an example of JSON that would be POSTed to your webhook URL

```json
{
  "data": {
    "id": "aabbccddeeffgg",
    "type": "donations",
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

> The following is an example of JSON that would be POSTed to your Webhook URL after an object deletion occurs

```json
{
  "data": {
    "id": "aabbccddeeffgg",
    "type": "donations",
    "attributes":{
      "deleted_at": 1494355936,
    }
  }
}
```

Webhooks allow Amplo to push data into your system in a near real-time capacity.
This allows you to supplement your API usage or fully change the dynamic of your API
usage from primarily pull-based (you make a request, we send the data back) to
push-based (when something interesting in the system happens, we let you know).

For example, when a Donation happens in Amplo's system, the Amplo API will POST related
JSON data to your registered Webhook URL for your immediate consumption (a.k.a. a callback).  

Webhook URLs can be registered on the Entity level.  SSL is required.  The endpoint provided
must directly consume the data without redirection, and return a `200 OK` upon success.  

Contact support to set one up.

### Events

Create, update and delete actions trigger Webhook callbacks. This includes actions performed
through the API itself.  The following objects are Webhook enabled:

Object | Conditions
------ | -----------
Campaign | Core Campaign attributes (rollup stats changes won't trigger callbacks)
Donation | Any modification to a Donation object triggers a callback


### Format

The POSTed JSON data will largely follow the same format as the main API.  The data will
be equivalent to what you would get on a single object GET request.  ID and Type fields
can be used to distinguish the nature of the data, since all objects are posted to the same
single Webhook URL.  

### Rate Limits

Webhook callbacks do not count towards the regular API rate limits. However, Webhook
callbacks are processed in near real-time, which means that while Webhook callbacks are initiated
at the time of the event, there might be some delay before a Webhook callback fully
completes and POSTs to the URL.  This is because Amplo will always process Webhook
callbacks at a lower priority level to anything core to ensuring a successful Giving Day.

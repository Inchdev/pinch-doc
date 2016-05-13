## Create a webhook

```ruby
require 'pinch'

pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
pinch.webhook.create({
  webhook_type: 1, # Ticket creation
  url: "https://example.com/ticket_creation"
})
```

```shell
curl -X POST -H "Content-Type: application/json" \
-H "X-API-EMAIL: g.provider1@yahoo.fr" \
-H "X-API-TOKEN: MY_API_KEY" \
-d '{
    "url": "https://example.com/ticket_creation",
    "webhook_type": 1
}' "https://api-company.inchbase.com/api/v1/webhooks"
```


> If the parameters are correct, the above command returns JSON structured like this:

```json
{
  "id": 1,
  "url": "https://example.com/ticket_creation",
  "webhook_type": 1,
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
```

> If there is an error, you will receive an answer that looks like this :

```json
{
  "errors": {
    "webhook_type": [
      "can't be blank"
    ]
  }
}
```

This endpoint creates a webhook for the specified event.

### HTTP Request

`POST https://company.inchbase.com/api/v1/webhooks`

### Query Parameters

Parameter | Description
--------- | -----------
webhook_type | You have to set this value to one of the values returned by the webhook types list
url | This string has to be a correct url, if not, you will receive an error.

<aside class="success">
Remember — You can define several webhooks, update or delete them!
</aside>

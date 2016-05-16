# Webhooks

## Create a webhook

```ruby
require 'pinch'

pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
pinch.webhook.create({
  webhook_type: 1, # Ticket creation
  url: "https://example.com/ticket_creation"
})
```

```python
  import Pinch
  controller = WebhookController()
  controller.create({'webhook_type': 1, 'url': 'https://example.com/ticket_creation'})
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


## List webhooks

```ruby
require 'pinch'
pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
pinch.webhook.list
```

```python
  import Pinch
  controller = WebhookController()
  controller.list()
```

```shell
curl -X GET -H "X-API-EMAIL: g.provider1@yahoo.fr" \
-H "X-API-TOKEN: MY_API_KEY" \
"https://api-company.inchbase.com/api/v1/webhooks"
```

> If the parameters are correct, the above command returns JSON structured like this:

```json
[{
  "id": 1,
  "url": "https://example.com/ticket_creation",
  "webhook_type": 1,
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
},{
  "id": 2,
  "url": "https://example.com/ticket_new_message",
  "webhook_type": 2,
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}]
```

> If there is an error, you will receive an answer that looks like this :

```json
{
  "errors": {
    ...
  }
}
```

This endpoint lets you retrieve every webhooks you've configured.

### HTTP Request

`GET https://api-company.inchbase.com/api/v1/webhooks`


## Get a webhook

````ruby
  require 'pinch'
  webhook_id = 42
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.webhook.get(webhook_id)
````

```python
  import Pinch
  webhook_id = 42
  controller = WebhookController()
  controller.get(42)
```


```shell
curl -X GET -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
"https://api-company.inchbase.com/api/v1/webhooks/42"
```

> If the parameters are correct, the above command returns JSON structured like this:

```json
{
  "id": 2,
  "url": "https://example.com/ticket_new_message",
  "webhook_type": 3,
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
```

> If there is an error, you will receive an answer that looks like this :

```json
{
  "errors": {
    ...
  }
}
```

This endpoint lets you retrieve a single webhook

### HTTP Request

`GET https://api-company.inchbase.com/api/v1/webhooks/:id`

## Update a webhook

````ruby
  require 'pinch'
  webhook_id = 2
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.webhook.update(webhook_id, {
    url: "https://example.com/test",
    webhook_type: 3
  })
````

```python
  import Pinch
  controller = WebhookController()
  controller.update({'webhook_type': 3, 'url': 'https://example.com/test'})
```


```curl
curl -X PUT -H "Content-Type: application/json" \
-H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" -d '{
    "webhook": {
        "url": "https://example.com/test",
        "webhook_type": 1
    }
}' "https://api-company.inchbase.com/api/v1/webhooks/42"
```


> If the parameters are correct, the above command returns JSON structured like this:

```json
{
  "id": 2,
  "url": "https://example.com/test",
  "webhook_type": 3,
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
```

This endpoint lets you retrieve a webhook by using its id. The parameters you can update are the url and the webhook type.

### HTTP Request

`PUT/PATCH https://api-company.inchbase.com/api/v1/webhooks/:id`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the webhook you want to update
webhook_type | You have to set this value to one of the values returned by the webhook types list
url | This string has to be a correct url, if not, you will receive an error.

## Destroy a webhook

````ruby
  require 'pinch'
  webhook_id = 42
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.webhook.destroy webhook_id
````

```python
  import Pinch
  webhook_id = 42
  controller = WebhookController()
  controller.destroy(webhook_id)
```


```shell
curl -X DELETE -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
"https://api-company.inchbase.com/api/v1/webhooks/42"
```

> This query returns an empty answer

This endpoint lets you destroy a webhook by using its id.

### HTTP Request

`DELETE https://api-company.inchbase.com/api/v1/webhooks/:id`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the webhook you want to destroy

<aside class="warning">
Be careful, you won't be able to access this webhook and any stats that could have been generated will also be destroyed
</aside>

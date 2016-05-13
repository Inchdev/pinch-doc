# Webhook Types

## Get the webhook types

```ruby
  require 'pinch'
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.webhook_type.list
```

```shell
curl -X GET -H "X-API-EMAIL: g.provider1@yahoo.fr" \
-H "X-API-TOKEN: MY_API_KEY" \
"https://api-company.inchbase.com/api/v1/webhook_types"
```

```python
  import pinch

  pinch = pinch.authorize('MY_API_KEY')
  pinch.webhook_types()
```

This methods allows you see what webhooks you can register via the API.

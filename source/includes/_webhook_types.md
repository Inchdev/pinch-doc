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
  import Pinch
  controller = WebhookTypeController()
  response = controller.list()
```

```javascript
  var pinch = require('pinch-api');
  var fs = require('fs');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';

  pinch.WebhookTypeController.list(function(error, result){
    console.log(result);
  });
```

This methods allows you see what webhooks you can register via the API.

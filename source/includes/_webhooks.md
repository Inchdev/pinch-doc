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
from Pinch import *
controller = WebhookController()
controller.create({'webhook_type': 1, 'url': 'https://example.com/ticket_creation'})
```

```javascript
var pinch = require('pinch-api');
var fs = require('fs');

pinch.configuration.xAPITOKEN = 'MY_API_KEY';
pinch.configuration.xAPIEMAIL = 'myemail@example.com';

pinch.WebhookController.create({
  'webhook_type': 1,
  'url': 'https://example.com/ticket_creation'
}, function(error, result){
  console.log(result);
});
```

```shell
curl -X POST -H "Content-Type: application/json" \
-H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
-d '{
    "url": "https://example.com/ticket_creation",
    "webhook_type": 1
}' "https://api-company.inchbase.com/api/v1/webhooks"
```

```java
import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.Webhook;
import com.inchbase.pinch.models.WebhookBuilder;

public class Test {

  public static void main(String[] args) {
    String apiKey = "MY_API_KEY";
    String apiEmail = "myemail@example.com";
    PinchClient client = new PinchClient(apiKey, apiEmail);
    try {
      String url = "https://example.com/ticket_creation";
      int webhookType = 1;
      Webhook webhook = new WebhookBuilder().
        url(url).webhookType(webhookType).
        build();
      webhook = client.getWebhook().create(webhook);
      System.out.println(webhook.getId());
    } catch (Throwable e) {
      e.printStackTrace();
    }
  }
}
```

```csharp
using System;
using pinch;
using pinch.Models;

namespace ConsoleApplication1
{
    class Program
    {
        private static PinchClient client;

        static void Main(string[] args)
        {
            client = new PinchClient("MY_API_KEY", "myemail@example.com");

            var webhook = new Webhook();
            webhook.Url = "https://example.com/ticket_creation";
            webhook.WebhookType = 1;
            client.Webhook.Create(webhook);
        }
    }
}
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
  from Pinch import *
  controller = WebhookController()
  controller.list()
```

```javascript
var pinch = require('pinch-api');
var fs = require('fs');

pinch.configuration.xAPITOKEN = 'MY_API_KEY';
pinch.configuration.xAPIEMAIL = 'myemail@example.com';

pinch.WebhookController.list(function(error, result){
  console.log(result);
});
```

```shell
curl -X GET -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
"https://api-company.inchbase.com/api/v1/webhooks"
```

```java
import java.util.List;
import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.Webhook;

public class Test {

  public static void main(String[] args) {
    String apiKey = "MY_API_KEY";
    String apiEmail = "myemail@example.com";
    PinchClient client = new PinchClient(apiKey, apiEmail);
    try {
      List<Webhook> webhooks= client.getWebhook().list();
      for(Webhook webhook: webhooks){
        System.out.println(webhook.getUrl());
      }
    } catch (Throwable e) {
      e.printStackTrace();
    }
  }
}
```

```csharp
using System;
using pinch;
using pinch.Models;

namespace ConsoleApplication1
{
    class Program
    {
        private static PinchClient client;

        static void Main(string[] args)
        {
            client = new PinchClient("MY_API_KEY", "myemail@example.com");
            
            var webhooks = client.Webhook.List();
            foreach(var webhook in webhooks)
            {
                Console.WriteLine(webhook.Url);
            }
            Console.ReadLine();
        }
    }
}
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

```ruby
  require 'pinch'
  webhook_id = 42
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.webhook.get(webhook_id)
```

```python
  from Pinch import *
  webhook_id = 42
  controller = WebhookController()
  controller.get(webhook_id)
```

```javascript
var pinch = require('pinch-api');
var fs = require('fs');

pinch.configuration.xAPITOKEN = 'MY_API_KEY';
pinch.configuration.xAPIEMAIL = 'myemail@example.com';

var webhookId = 42;

pinch.WebhookController.get(webhookId, function(error, result){
  console.log(result);
});
```

```shell
curl -X GET -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
"https://api-company.inchbase.com/api/v1/webhooks/42"
```

```java
import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.Webhook;

public class Test {

  public static void main(String[] args) {
    String apiKey = "MY_API_KEY";
    String apiEmail = "myemail@example.com";
    PinchClient client = new PinchClient(apiKey, apiEmail);
    try {
      String webhookId = "42";
      Webhook webhook = client.getWebhook().get(webhookId);
      System.out.println(webhook.getId());
    } catch (Throwable e) {
      e.printStackTrace();
    }
  }
}
```

```csharp
using System;
using pinch;

namespace ConsoleApplication1
{
    class Program
    {
        private static PinchClient client;

        static void Main(string[] args)
        {
            client = new PinchClient("MY_API_KEY", "myemail@example.com");

            String webhookId = "42";
            var webhook = client.Webhook.Get(webhookId);
            Console.WriteLine(webhook.Url);
            Console.ReadLine();
        }
    }
}
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
  from Pinch import *
  controller = WebhookController()
  webhook_id = 42;
  controller.update(webhook_id, {'webhook_type': 3, 'url': 'https://example.com/test'})
```

```javascript
var pinch = require('pinch-api');
var fs = require('fs');

pinch.configuration.xAPITOKEN = 'MY_API_KEY';
pinch.configuration.xAPIEMAIL = 'myemail@example.com';

var webhookId = 42;

pinch.WebhookController.update(webhookId, {
  'webhook_type': 3,
  'url': 'https://example.com/test'
}, function(error, result){
  console.log(result);
});
```

```shell
curl -X PUT -H "Content-Type: application/json" \
-H "Accept: application/json" -H "Content-Type: application/json" \
-H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" -d '{
  "url": "https://example.com/test",
  "webhook_type": 1
}' "https://api-company.inchbase.com/api/v1/webhooks/42"
```

```java
import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.Webhook;

public class Test {

  public static void main(String[] args) {
    String apiKey = "MY_API_KEY";
    String apiEmail = "myemail@example.com";
    PinchClient client = new PinchClient(apiKey, apiEmail);
    try {
      String webhookId = "42";
      Webhook webhook =  client.getWebhook().get(webhookId);
      webhook.setWebhookType(3);
      webhook.setUrl("https://example.com/test");
      client.getWebhook().update(webhook.getId(), webhook);
    } catch (Throwable e) {
      e.printStackTrace();
    }
  }
}
```

```csharp
using System;
using pinch;

namespace ConsoleApplication1
{
    class Program
    {
        private static PinchClient client;

        static void Main(string[] args)
        {
            client = new PinchClient("MY_API_KEY", "myemail@example.com");

            String webhookId = "42";
            var webhookController = client.Webhook;
            var webhook = webhookController.Get(webhookId);
            webhook.Url = "https://example.com/test";
            webhook.WebhookType = 3;
            webhookController.Update(webhook.Id, webhook);
        }
    }
}
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
  from Pinch import *
  webhook_id = 42
  controller = WebhookController()
  controller.destroy(webhook_id)
```

```javascript
var pinch = require('pinch-api');
var fs = require('fs');

pinch.configuration.xAPITOKEN = 'MY_API_KEY';
pinch.configuration.xAPIEMAIL = 'myemail@example.com';
var webhookId = 42;
pinch.WebhookController.destroy(webhookId, function(error, result){
  console.log(result);
});
```


```shell
curl -X DELETE -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
"https://api-company.inchbase.com/api/v1/webhooks/42"
```

```java
import com.inchbase.pinch.PinchClient;

public class Test {

  public static void main(String[] args) {
    String apiKey = "MY_API_KEY";
    String apiEmail = "myemail@example.com";
    PinchClient client = new PinchClient(apiKey, apiEmail);
    try {
      int webhookId = 42;
      client.getWebhook().destroy(webhookId);
    } catch (Throwable e) {
      e.printStackTrace();
    }
  }
}
```

```csharp
using System;
using pinch;

namespace ConsoleApplication1
{
    class Program
    {
        private static PinchClient client;

        static void Main(string[] args)
        {
            client = new PinchClient("MY_API_KEY", "myemail@example.com");

            int webhookId = 42;
            var webhookController = client.Webhook.Destroy(webhookId);
        }
    }
}
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

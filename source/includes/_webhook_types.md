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
-H "Accept: application/json" -H "Content-Type: application/json" \
"https://api-company.inchbase.com/api/v1/webhook_types"
```

```python
  from Pinch import *
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

```java
import java.util.List;

import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.WebhookType;

public class Test {

	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			List<WebhookType> webhookTypes = client.getWebhookType().list();
			for(WebhookType webhookType : webhookTypes){
				System.out.println(webhookType.getName());
			}
		} catch (Throwable e) {
			e.printStackTrace();
		}
	}

}
```


```csharp
using System;
...
using System.Threading.Tasks;
using pinch;

namespace ConsoleApplication1
{
    class Program
    {
        private static PinchClient client;

        static void Main(string[] args)
        {
            client = new PinchClient("MY_API_KEY", "myemail@example.com");

            var webhookTypes = client.WebhookType.List();
            foreach(var webhookType in webhookTypes)
            {
                Console.WriteLine(webhookType.Name);
            }
            Console.ReadLine();
        }
    }
}
```

This methods allows you see what webhooks you can register via the API.

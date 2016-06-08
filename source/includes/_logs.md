# Logs

## List your requests

````ruby
  require 'pinch'
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  page_num = 1
  logs = pinch.logs.list page_num
  logs.each do |log|
    puts log.name
  end
````

````python
from Pinch import *
controller = LogController()
page_num = 1
logs = controller.list(page_num)
````

````javascript
var pinch = require('pinch-api');

pinch.configuration.xAPITOKEN = 'MY_API_KEY';
pinch.configuration.xAPIEMAIL = 'myemail@example.com';

var pageNum = 1;
pinch.LogController.list(pageNum, function(error, result){
  console.log(result);
});
````

```shell
curl -X GET -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
"https://api-company.inchbase.com/api/v1/logs?page=1"
```

```java
import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.Log;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
      int pageNum = 1;
			List<Log> logs = client.getLog().list(pageNum);
			for(Log log : logs){
        System.out.println(log.getId());
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
            var pageNum = 1;
            var logs = client.Log.List(pageNum);
            foreach(var log in logs){
              Console.WriteLine(log.Id);
            }
            Console.ReadLine();
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the list of your clients using Inch:

````json
[{
  "id": 42,
  "webhook_id": 41,
  "params": "{\"limit\":\"10\",\"page\":\"1\",\"sorting\":\"{}\",\"controller\":\"api/v1/webhooks\",\"action\":\"index\"}",
  "details": "webhooks / index",
  "created_at": "2016-05-11T20:03:46.769+02:00"
},
...
]
````

This endpoint lets you retrieve the list of all the requests you performed. It is a paginated request.

### HTTP Request

`GET https://api-company.inchbase.com/api/v1/logs`

### Query Parameters

Parameter | Description
--------- | -----------
page | The page number
limit | The page size (default to 50)
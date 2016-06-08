# Servers

## List clients using Inch

````ruby
  require 'pinch'
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  servers = pinch.servers.list
  servers.each do |server|
    puts server.name
  end
````

````python
from Pinch import *
controller = ServerController()
servers = controller.list()
````

````javascript
var pinch = require('pinch-api');

pinch.configuration.xAPITOKEN = 'MY_API_KEY';
pinch.configuration.xAPIEMAIL = 'myemail@example.com';

pinch.ServerController.list(function(error, result){
  console.log(result);
});
````

```shell
curl -X GET -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
"https://api-company.inchbase.com/api/v1/servers"
```

```java
import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.Server;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			List<Server> servers = client.getServer().list();
			for(Server server : servers){
        System.out.println(server.getName());
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
            var servers = client.Server.List();
            foreach(var server in servers){
              Console.WriteLine(server.Name);
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
  "name": "Demo",
  "server_short_name": "DEM",
  "logo_url": null
},
...
]
````

This endpoint lets you retrieve the list of all your clients using Inch. Please contact us if we forgot one.

### HTTP Request

`GET https://api-company.inchbase.com/api/v1/servers`

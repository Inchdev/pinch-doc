# Authentication

> To authorize, use this code:

```ruby
require 'pinch'

pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
```

```python
from Pinch import *

Configuration.x_api_token = 'MY_API_KEY'
Configuration.x_api_email = 'myemail@example.com'
```

```javascript
  pinch = require('pinch-api');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';
```

```shell
# With shell, you can just pass the correct header with each request
curl "https://api-company.inchbase.com/api/v1" \
  -H "X-API-EMAIL: myemail@example.com" \
  -H "X-API-TOKEN: MY_API_KEY" \
  -H "Accept: application/json" -H "Content-Type: application/json"
```

```java
import java.util.List;
import com.inchbase.pinch.PinchClient;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
	}
}
```

````cs
using System;
using System.Threading.Tasks;
...
using pinch;

namespace MyNamespace
{
    class MyProgram
    {
        private static PinchClient client;

        static void Main(string[] args)
        {
            client = new PinchClient("MY_API_KEY", "myemail@example.com");
        }
    }
}
```

> Make sure to replace `MY_API_KEY` with your API key.

Pinch uses API keys to allow access to the API. You can register a new Pinch API key by contacting us.

Pinch expects for the API key to be included in all API requests to the server in a header that looks like the following:

`X-API-EMAIL: myemail@example.com`

`X-API-TOKEN: MY_API_KEY`

<aside class="notice">
You must replace <code>MY_API_KEY</code> with your personal API key and myemail@example.com with your registered email.
</aside>
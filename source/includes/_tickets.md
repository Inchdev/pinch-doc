# Tickets

## Get a ticket

````ruby
  require 'pinch'
  ticket_id = 42
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.get ticket_id
````

````python
from Pinch import *
ticket_id = 42
controller = TicketController()
ticket = controller.get(ticket_id)
````

```javascript
  var pinch = require('pinch-api');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';

  var ticketId = 42;
  pinch.TicketController.get(ticketId, function(error, result){
    console.log(result);
  });
```

```shell
curl -X GET -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
"https://api-company.inchbase.com/api/v1/tickets/{{ticket_id}}"
```

```java
import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.Ticket;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			String ticketId = "DEM-42";
			Ticket ticket = client.getTicket().get(ticketId);
			System.out.println(ticket.getName());
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
            String ticketId = "42";
            var ticket = client.Ticket.Get(ticketId);
            Console.WriteLine(ticket.Name);
            Console.ReadLine();
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the updated ticket:

````json
{
  "id": 42,
  "name": "Gaine électrique arrachée",
  "description": "Dans le hall B",
  "contacts": [{
    "firstname": "Martin",
    "lastname": "Dupont",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Resident"
  },{
    "firstname": "Jean",
    "lastname": "Durand",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Caretaker"
  }],
  "status": "En attente de la facture",
  "building": {
    "reference": "1234",
    "name": "ALPINA 4",
    "address": "46 Rue René Clair",
    "zip_code": "92700",
    "city": "Paris",
    "country": "France",
    "latitude": "48.8939624",
    "longitude": "2.3518942"
  },
  "unit": {
    "reference": "002",
    "tenant_name": "Lucas Ferrand",
    "floor_number": "4",
    "kind": "Grenier",
    "french_floor_number": "4ème Gauche"
  },
  "access": "Digicode : 4633B",
  "agency": "Cabinet Inch Immobilier",
  "manager": "Thomas THIMOTHÉE",
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
````

This endpoint lets you retrieve a ticket.

### HTTP Request

`GET https://api-company.inchbase.com/api/v1/tickets/:id`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the ticket you want to retrieve

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>

## List opened tickets

````ruby
  require 'pinch'
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.list
````

```python
  from Pinch import *
  controller = TicketController()
  list = controller.list()
```

```javascript
  var pinch = require('pinch-api');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';

  pinch.TicketController.list(function(error, result){
    console.log(result);
  });
```


```shell
curl -X GET -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
"https://api-company.inchbase.com/api/v1/tickets"
```

```java
import java.util.List;
import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.Ticket;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			List<Ticket> tickets = client.getTicket().list();
      for(Ticket ticket : tickets){
        System.out.println(ticket.getName());
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
            var tickets = client.Ticket.List();
            foreach(var ticket in tickets){
              Console.WriteLine(ticket.Name);
            }
            Console.ReadLine();
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the updated ticket:

````json
[{
  "id": 42,
  "name": "Gaine électrique arrachée",
  "description": "Dans le hall B",
  "contacts": [{
    "firstname": "Martin",
    "lastname": "Dupont",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Resident"
  },{
    "firstname": "Jean",
    "lastname": "Durand",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Caretaker"
  }],
  "status": "En attente de la facture",
  "building": {
    "reference": "1234",
    "name": "ALPINA 4",
    "address": "46 Rue René Clair",
    "zip_code": "92700",
    "city": "Paris",
    "country": "France",
    "latitude": "48.8939624",
    "longitude": "2.3518942"
  },
  "unit": {
    "reference": "002",
    "tenant_name": "Lucas Ferrand",
    "floor_number": "4",
    "kind": "Grenier",
    "french_floor_number": "4ème Gauche"
  },
  "access": "Digicode : 4633B",
  "agency": "Cabinet Inch Immobilier",
  "manager": "Thomas THIMOTHÉE",
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
},
...
]
````

This endpoint lets you retrieve the list of all opened tickets you are currently dealing with. It may be quote or intervention requests. 

### HTTP Request

`GET https://api-company.inchbase.com/api/v1/tickets`

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>

## Accept an intervention

````ruby
  require 'pinch'
  ticket_id = 42
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.accept_intervention ticket_id
````

```python
  from Pinch import *
  ticket_id = 42
  controller = TicketController()
  controller.accept_intervention(ticket_id)
```

```javascript
  var pinch = require('pinch-api');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';

  var ticketId = 42;
  pinch.TicketController.acceptIntervention(ticketId, function(error,result){
    console.log(result);
  });
```

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
"https://api-company.inchbase.com/api/v1/REL-42/accept_intervention"
```

```java
import java.util.List;

import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.Ticket;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			String ticketId = "DEM-42";
			client.getTicket().acceptIntervention(ticketId);
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
            String ticketId = "DEM-42"; 
            client.Ticket.AcceptIntervention(ticketId);
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the updated ticket:

````json
{
  "id": 42,
  "name": "Gaine électrique arrachée",
  "description": "Dans le hall B",
  "contacts": [{
    "firstname": "Martin",
    "lastname": "Dupont",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Resident"
  },{
    "firstname": "Jean",
    "lastname": "Durand",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Caretaker"
  }],
  "status": "En attente de la facture",
  "building": {
    "reference": "1234",
    "name": "ALPINA 4",
    "address": "46 Rue René Clair",
    "zip_code": "92700",
    "city": "Paris",
    "country": "France",
    "latitude": "48.8939624",
    "longitude": "2.3518942"
  },
  "unit": {
    "reference": "002",
    "tenant_name": "Lucas Ferrand",
    "floor_number": "4",
    "kind": "Grenier",
    "french_floor_number": "4ème Gauche"
  },
  "access": "Digicode : 4633B",
  "agency": "Cabinet Inch Immobilier",
  "manager": "Thomas THIMOTHÉE",
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
````

When you want to notify the manager that you accepted the intervention, you can use this endpoint.

### HTTP Request

`POST https://api-company.inchbase.com/api/v1/tickets/:id/accept_intervention`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the ticket whose intervention you want to accept

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>

## Set an intervention date

````ruby
  require 'pinch'
  ticket_id = 42
  date = 2.months.ago
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.set_intervention_date date, ticket_id
````

```python
  from Pinch import *
  import datetime
  date = datetime.date.today()
  ticket_id = 42
  controller = TicketController()
  controller.set_intervention_date(date, ticket_id)
```

```javascript
  var pinch = require('pinch-api');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';
  
  var myDate = new Date();
  var ticketId = 42;

  pinch.TicketController.setInterventionDate(myDate, ticketId, function(error, result){
    console.log(result);
  });
```

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
-d '{
    "intervention_date": "2016-05-11T20:03:46.769+02:00"
}' \
"https://api-company.inchbase.com/tickets/DEM-42/set_intervention_date"
```

```java
import java.util.Date;
import java.util.List;

import com.inchbase.pinch.PinchClient;
import com.inchbase.pinch.models.Ticket;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			String ticketId = "DEM-42";
      Date interventionDate = new Date();
			client.getTicket().setInterventionDate(interventionDate, ticketId);
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
            String ticketId = "DEM-42";
            DateTime date = new DateTime();
            client.Ticket.SetInterventionDate(date, ticketId);
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the updated ticket:

````json
{
  "id": 42,
  "name": "Gaine électrique arrachée",
  "description": "Dans le hall B",
  "contacts": [{
    "firstname": "Martin",
    "lastname": "Dupont",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Resident"
  },{
    "firstname": "Jean",
    "lastname": "Durand",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Caretaker"
  }],
  "status": "En attente de la facture",
  "building": {
    "reference": "1234",
    "name": "ALPINA 4",
    "address": "46 Rue René Clair",
    "zip_code": "92700",
    "city": "Paris",
    "country": "France",
    "latitude": "48.8939624",
    "longitude": "2.3518942"
  },
  "unit": {
    "reference": "002",
    "tenant_name": "Lucas Ferrand",
    "floor_number": "4",
    "kind": "Grenier",
    "french_floor_number": "4ème Gauche"
  },
  "access": "Digicode : 4633B",
  "agency": "Cabinet Inch Immobilier",
  "manager": "Thomas THIMOTHÉE",
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
````

To inform the manager and notify the residents of an intervention date, you can use this endpoint.

### HTTP Request

`POST https://api-company.inchbase.com/api/v1/tickets/:id/intervention_done`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the ticket whose intervention date you want to set
intervention_date | The date the intervention was done

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>

## Declare an intervention as done

````ruby
  require 'pinch'
  ticket_id = 42
  date = 2.months.ago # Optional
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.declare_intervention_done ticket_id, date
````

```python
  from Pinch import *
  import datetime
  date = datetime.date.today()
  ticket_id = 42
  controller = TicketController()
  controller.declare_intervention_done(date, ticket_id)
```

```javascript
  var pinch = require('pinch-api');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';
  
  var myDate = new Date();
  var ticketId = 42;

  pinch.TicketController.declareInterventionDone(myDate, ticketId, function(error, result){
    console.log(result);
  });
```

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
-d '{
    "intervention_date": "2016-05-11T20:03:46.769+02:00"
}' \
"https://api-company.inchbase.com/tickets/DEM-42/intervention_done"
```

```java
import java.util.Date;
import java.util.List;

import com.inchbase.pinch.PinchClient;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			String ticketId = "DEM-42";
      Date interventionDate = new Date();
			client.getTicket().declareInterventionDone(ticketId, interventionDate);
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
            String ticketId = "DEM-42";
            DateTime date = new DateTime();
            client.Ticket.DeclareInterventionDone(ticketId, date);
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the updated ticket:

````json
{
  "id": 42,
  "name": "Gaine électrique arrachée",
  "description": "Dans le hall B",
  "contacts": [{
    "firstname": "Martin",
    "lastname": "Dupont",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Resident"
  },{
    "firstname": "Jean",
    "lastname": "Durand",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Caretaker"
  }],
  "status": "En attente de la facture",
  "building": {
    "reference": "1234",
    "name": "ALPINA 4",
    "address": "46 Rue René Clair",
    "zip_code": "92700",
    "city": "Paris",
    "country": "France",
    "latitude": "48.8939624",
    "longitude": "2.3518942"
  },
  "unit": {
    "reference": "002",
    "tenant_name": "Lucas Ferrand",
    "floor_number": "4",
    "kind": "Grenier",
    "french_floor_number": "4ème Gauche"
  },
  "access": "Digicode : 4633B",
  "agency": "Cabinet Inch Immobilier",
  "manager": "Thomas THIMOTHÉE",
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
````

You should use this endpoint when you have finished an intervention.

### HTTP Request

`POST https://api-company.inchbase.com/api/v1/tickets/:id/accept_intervention`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the ticket whose intervention you want to accept
intervention_date | The date the intervention was done

<aside class="notice">
  The intervention date can be sent but is optional
</aside>

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>

## Send a message in a ticket

````ruby
  require 'pinch'
  ticket_id = 42
  body = "Salut"
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.send_message body, ticket_id
````

```python
  from Pinch import *
  body = "Salut"
  ticket_id = 42
  controller = TicketController()
  controller.send_message(body, ticket_id)
```

```javascript
  var pinch = require('pinch-api');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';

  var ticketId = 42;

  pinch.TicketController.sendMessage(ticketId, function(error, result){
    console.log(result);
  });
```

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Accept: application/json" -H "Content-Type: application/json" \
-d '{
    "body": "Salut"
}' \
"https://api-company.inchbase.com/api/v1/tickets/DEM-42/message"
```

```java
import com.inchbase.pinch.PinchClient;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			String ticketId = "DEM-42";
			String body = "Hello !";
			client.getTicket().sendMessage(body, ticketId);
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
            String ticketId = "DEM-42";
            String body = "Hello !";
            client.Ticket.SendMessage(ticketId, body);
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the updated ticket:

````json
{
  "id": 42,
  "name": "Gaine électrique arrachée",
  "description": "Dans le hall B",
  "contacts": [{
    "firstname": "Martin",
    "lastname": "Dupont",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Resident"
  },{
    "firstname": "Jean",
    "lastname": "Durand",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Caretaker"
  }],
  "status": "En attente de la facture",
  "building": {
    "reference": "1234",
    "name": "ALPINA 4",
    "address": "46 Rue René Clair",
    "zip_code": "92700",
    "city": "Paris",
    "country": "France",
    "latitude": "48.8939624",
    "longitude": "2.3518942"
  },
  "unit": {
    "reference": "002",
    "tenant_name": "Lucas Ferrand",
    "floor_number": "4",
    "kind": "Grenier",
    "french_floor_number": "4ème Gauche"
  },
  "access": "Digicode : 4633B",
  "agency": "Cabinet Inch Immobilier",
  "manager": "Thomas THIMOTHÉE",
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
````

You can use this endpoint to send a message to the manager of the ticket.

### HTTP Request

`POST https://api-company.inchbase.com/api/v1/tickets/:id/message`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the ticket
body | The body of the message

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>

## Upload a document

````ruby
  require 'pinch'
  ticket_id = 42
  file = File.new('my_path.txt', 'rb')
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.upload_document file, ticket_id
````

```python
  from Pinch import *
  f = open('my_path.txt', 'rb')
  ticket_id = 42
  controller = TicketController()
  controller.upload_document(f, ticket_id)
```

```javascript
  var pinch = require('pinch-api');
  var fs = require('fs');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';

  var ticketId = 42;
  
  fs.readFile('DATA', 'utf8', function(err, contents) {
    pinch.TicketController.uploadDocument(contents, ticketId, function(error, result){
      console.log(result);
    });
  });
```

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" \
-F "file=@my_path.txt" \
"https://api-company.inchbase.com/api/v1/tickets/DEM-42/document_upload"
```

```java
import java.io.File;
import com.inchbase.pinch.PinchClient;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			String ticketId = "DEM-42";
			File file = new File("my_path.txt");
			client.getTicket().uploadDocument(file , ticketId);
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
            String ticketId = "DEM-42";

            var file = System.IO.File.OpenRead("my_path.txt");
            var stream = new pinch.Http.Client.FileStreamInfo(file);

            client.Ticket.UploadDocument(stream, ticketId);
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the updated ticket:

````json
{
  "id": 42,
  "name": "Gaine électrique arrachée",
  "description": "Dans le hall B",
  "contacts": [{
    "firstname": "Martin",
    "lastname": "Dupont",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Resident"
  },{
    "firstname": "Jean",
    "lastname": "Durand",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Caretaker"
  }],
  "status": "En attente de la facture",
  "building": {
    "reference": "1234",
    "name": "ALPINA 4",
    "address": "46 Rue René Clair",
    "zip_code": "92700",
    "city": "Paris",
    "country": "France",
    "latitude": "48.8939624",
    "longitude": "2.3518942"
  },
  "unit": {
    "reference": "002",
    "tenant_name": "Lucas Ferrand",
    "floor_number": "4",
    "kind": "Grenier",
    "french_floor_number": "4ème Gauche"
  },
  "access": "Digicode : 4633B",
  "agency": "Cabinet Inch Immobilier",
  "manager": "Thomas THIMOTHÉE",
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
````

This endpoint allows you to update any documents that are related to the ticket but are neither quotes, nor invoices, nor pictures.

### HTTP Request

`POST https://api-company.inchbase.com/api/v1/tickets/:id/document_upload`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the ticket
file | The file to upload

<aside class='warning'>You should not upload quotes, invoices or pictures via this endpoint!</aside>

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>


## Upload a picture

````ruby
  require 'pinch'
  ticket_id = 42
  file = File.new('my_path.txt', 'rb')
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.upload_picture file, ticket_id
````

```python
  from Pinch import *
  f = open('my_path.txt', 'rb')
  ticket_id = 42
  controller = TicketController()
  controller.upload_picture(f, ticket_id)
```

```javascript
  var pinch = require('pinch-api');
  var fs = require('fs');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';

  var ticketId = 42;
  
  fs.readFile('DATA', 'utf8', function(err, contents) {
    pinch.TicketController.uploadPicture(contents, ticketId, function(error, result){
      console.log(result);
    });
  });
```

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" \
-F "file=@my_path.txt" \
"https://api-company.inchbase.com/api/v1/tickets/DEM-42/picture_upload"
```

```java
import java.io.File;
import com.inchbase.pinch.PinchClient;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			String ticketId = "DEM-42";
			File file = new File("my_path.txt");
			client.getTicket().uploadPicture(file , ticketId);
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
            String ticketId = "DEM-42";

            var file = System.IO.File.OpenRead("my_path.txt");
            var stream = new pinch.Http.Client.FileStreamInfo(file);

            client.Ticket.uploadPicture(stream, ticketId);
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the updated ticket:

````json
{
  "id": 42,
  "name": "Gaine électrique arrachée",
  "description": "Dans le hall B",
  "contacts": [{
    "firstname": "Martin",
    "lastname": "Dupont",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Resident"
  },{
    "firstname": "Jean",
    "lastname": "Durand",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Caretaker"
  }],
  "status": "En attente de la facture",
  "building": {
    "reference": "1234",
    "name": "ALPINA 4",
    "address": "46 Rue René Clair",
    "zip_code": "92700",
    "city": "Paris",
    "country": "France",
    "latitude": "48.8939624",
    "longitude": "2.3518942"
  },
  "unit": {
    "reference": "002",
    "tenant_name": "Lucas Ferrand",
    "floor_number": "4",
    "kind": "Grenier",
    "french_floor_number": "4ème Gauche"
  },
  "access": "Digicode : 4633B",
  "agency": "Cabinet Inch Immobilier",
  "manager": "Thomas THIMOTHÉE",
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
````

You can upload here any picture related to the ticket (before or after it has been done).

### HTTP Request

`POST https://api-company.inchbase.com/api/v1/tickets/:id/picture_upload`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the ticket
file | The picture to upload

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>


## Upload a quote

````ruby
  require 'pinch'
  ticket_id = 42
  file = File.new('my_path.txt', 'rb')
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.upload_quote file, ticket_id
````

```python
  from Pinch import *
  f = open('my_path.txt', 'rb')
  ticket_id = 42
  controller = TicketController()
  controller.upload_quote(f, ticket_id)
```

```javascript
  var pinch = require('pinch-api');
  var fs = require('fs');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';

  var ticketId = 42;
  
  fs.readFile('DATA', 'utf8', function(err, contents) {
    pinch.TicketController.uploadQuote(contents, ticketId, function(error, result){
      console.log(result);
    });
  });
```

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" \
-F "file=@my_path.txt" \
"https://api-company.inchbase.com/api/v1/tickets/DEM-42/quote_upload"
```

```java
import java.io.File;
import com.inchbase.pinch.PinchClient;

public class Test {
	public static void main(String[] args) {
		String apiKey = "MY_API_KEY";
		String apiEmail = "myemail@example.com";
		PinchClient client = new PinchClient(apiKey, apiEmail);
		try {
			String ticketId = "DEM-42";
			File file = new File("my_path.txt");
			client.getTicket().uploadQuote(file , ticketId);
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
            String ticketId = "DEM-42";

            var file = System.IO.File.OpenRead("my_path.txt");
            var stream = new pinch.Http.Client.FileStreamInfo(file);

            client.Ticket.uploadQuote(stream, ticketId);
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the updated ticket:

````json
{
  "id": 42,
  "name": "Gaine électrique arrachée",
  "description": "Dans le hall B",
  "contacts": [{
    "firstname": "Martin",
    "lastname": "Dupont",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Resident"
  },{
    "firstname": "Jean",
    "lastname": "Durand",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Caretaker"
  }],
  "status": "En attente de la facture",
  "building": {
    "reference": "1234",
    "name": "ALPINA 4",
    "address": "46 Rue René Clair",
    "zip_code": "92700",
    "city": "Paris",
    "country": "France",
    "latitude": "48.8939624",
    "longitude": "2.3518942"
  },
  "unit": {
    "reference": "002",
    "tenant_name": "Lucas Ferrand",
    "floor_number": "4",
    "kind": "Grenier",
    "french_floor_number": "4ème Gauche"
  },
  "access": "Digicode : 4633B",
  "agency": "Cabinet Inch Immobilier",
  "manager": "Thomas THIMOTHÉE",
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
````

When being asked for a quote, you can use this endpoint to send your quote.

### HTTP Request

`POST https://api-company.inchbase.com/api/v1/tickets/:id/quote_upload`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the ticket
file | The quote to upload

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>

## Upload an invoice

````ruby
  require 'pinch'
  ticket_id = 42
  file = File.new('my_path.txt', 'rb')
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.upload_invoice file, ticket_id
````

```python
  from Pinch import *
  f = open('my_path.txt', 'rb')
  ticket_id = 42
  controller = TicketController()
  controller.upload_invoice(f, ticket_id)
```

```javascript
  var pinch = require('pinch-api');
  var fs = require('fs');
  
  pinch.configuration.xAPITOKEN = 'MY_API_KEY';
  pinch.configuration.xAPIEMAIL = 'myemail@example.com';

  var ticketId = 42;
  
  fs.readFile('DATA', 'utf8', function(err, contents) {
    pinch.TicketController.uploadInvoice(contents, ticketId, function(error, result){
      console.log(result);
    });
  });
```


```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" \
-F "file=@my_path.txt" \
"https://api-company.inchbase.com/api/v1/tickets/DEM-42/invoice_upload"
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
            String ticketId = "DEM-42";

            var file = System.IO.File.OpenRead("my_path.txt");
            var stream = new pinch.Http.Client.FileStreamInfo(file);

            client.Ticket.uploadInvoice(stream, ticketId);
        }
    }
}
```

> If the parameters are correct, the above command returns JSON structured like this representing the updated ticket:

````json
{
  "id": 42,
  "name": "Gaine électrique arrachée",
  "description": "Dans le hall B",
  "contacts": [{
    "firstname": "Martin",
    "lastname": "Dupont",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Resident"
  },{
    "firstname": "Jean",
    "lastname": "Durand",
    "home_phone_number": "01 02 03 04 05",
    "mobile_phone_number": "06 01 02 03 04",
    "role": "Caretaker"
  }],
  "status": "En attente de la facture",
  "building": {
    "reference": "1234",
    "name": "ALPINA 4",
    "address": "46 Rue René Clair",
    "zip_code": "92700",
    "city": "Paris",
    "country": "France",
    "latitude": "48.8939624",
    "longitude": "2.3518942"
  },
  "unit": {
    "reference": "002",
    "tenant_name": "Lucas Ferrand",
    "floor_number": "4",
    "kind": "Grenier",
    "french_floor_number": "4ème Gauche"
  },
  "access": "Digicode : 4633B",
  "agency": "Cabinet Inch Immobilier",
  "manager": "Thomas THIMOTHÉE",
  "created_at": "2016-05-11T20:03:46.769+02:00",
  "updated_at": "2016-05-11T20:03:46.769+02:00"
}
````

When being asked for an invoice, you can use this endpoint to send your invoice.

### HTTP Request

`POST https://api-company.inchbase.com/api/v1/tickets/:id/invoice_upload`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the ticket
file | The invoice to upload

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>
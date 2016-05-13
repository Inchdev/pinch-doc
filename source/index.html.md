---
title: Inch API for companies

language_tabs:
  - shell: cURL
  - ruby: Ruby
  - python: Python
  - csharp: C#
  - angular: AngularJS
  - node: NodeJS
  - java: Java
  - php: PHP

toc_footers:
  - Contact us for a developer key
  - <a href='mailto:contact@inchbase.com'>contact@inchbase.com</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Inch API! You can use our API to access Inch API endpoints, which can get help you configure webhooks to instantly receive ticket creations and update them.

We have language bindings in Shell, Ruby, Python and C Sharp, AngularJS, NodeJS, Java and PHP ! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```ruby
require 'pinch'

pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
```

```python
import pinch

api = pinch.authorize('MY_API_KEY')
```

```shell
# With shell, you can just pass the correct header with each request
curl "https://company.inchbase.com/api/v1"
  -H "Authorization: MY_API_KEY"
```

> Make sure to replace `MY_API_KEY` with your API key.

Pinch uses API keys to allow access to the API. You can register a new Pinch API key by contacting us.

Pinch expects for the API key to be included in all API requests to the server in a header that looks like the following:

`X-API-EMAIL: myemail@example.com`

`X-API-TOKEN: MY_API_KEY`

<aside class="notice">
You must replace <code>MY_API_KEY</code> with your personal API key and myemail@example.com with your registered email.
</aside>

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
  pinch.webhook.destroy
````

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

# Tickets

## Get a ticket

````ruby
  require 'pinch'
  ticket_id = 42
  pinch = Pinch::PinchClient.new(x_api_token: "MY_API_KEY", x_api_email: "myemail@example.com")
  pinch.ticket.get ticket_id
````

```shell
curl -X GET -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
"https://api-company.inchbase.com/api/v/1tickets/{{ticket_id}}"
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

```shell
curl -X GET -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
"https://api-company.inchbase.com/api/v1/tickets"
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

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
"https://api-company.inchbase.com/api/v1/42/accept"
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

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "intervention_date": "2016-05-11T20:03:46.769+02:00"
}' \
"https://api-company.inchbase.com/tickets/42/set_intervention_date"
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

`POST https://api-company.inchbase.com/api/v1/tickets/:id/set_intervention_date`

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

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "intervention_date": "2016-05-11T20:03:46.769+02:00"
}' \
"https://api-company.inchbase.com/tickets/42/declare_intervention_done"
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

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: application/json" \
-d '{
    "body": "Salut"
}' \
"https://api-company.inchbase.com/api/v1/tickets/42/message"
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

`POST https://api-company.inchbase.com/api/v1/tickets/:id/accept_intervention`

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

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" \
-F "file=@my_path.txt" \
"https://api-company.inchbase.com/api/v1/tickets/42/document_upload"
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

`POST https://api-company.inchbase.com/api/v1/tickets/:id/upload_document`

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

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" \
-F "file=@my_path.txt" \
"https://api-company.inchbase.com/api/v1/tickets/42/picture_upload"
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

`POST https://api-company.inchbase.com/api/v1/tickets/:id/upload_picture`

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

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" \
-F "file=@my_path.txt" \
"https://api-company.inchbase.com/api/v1/tickets/42/quote_upload"
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

`POST https://api-company.inchbase.com/api/v1/tickets/:id/upload_quote`

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

```shell
curl -X POST -H "X-API-EMAIL: myemail@example.com" \
-H "X-API-TOKEN: MY_API_KEY" \
-H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" \
-F "file=@my_path.txt" \
"https://api-company.inchbase.com/api/v1/tickets/42/invoice_upload"
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

`POST https://api-company.inchbase.com/api/v1/tickets/:id/upload_invoice`

### Query Parameters

Parameter | Description
--------- | -----------
id | The id of the ticket
file | The invoice to upload

<aside class="notice">
  Latitude and longitude float numbers may not be accurate.
</aside>

GRC Contact PHP API 
=================

GRC Contact (https://www.grc-contact.fr/) the simplest CRM software 
wich optimizes your business performance.

Table of contents
---------------

**[Intro](#intro)**

**[Usage](#usage)**

**[1. Events](#1-events)**
 - [1.1 To list events](#11-to-list-events)
 - [1.2 To fetch an event](#12-to-fetch-an-event)
 - [1.3 To create an event](#13-to-create-an-event)
 - [1.4 To delete an event](#14-to-delete-an-event)
 - [1.5 To update an event](#15-to-update-an-event)



##Intro

1. Create your API account on **GRC Contact**, you will just need your e-mail address and password to get your **GRC_API_TOKEN** and set into [**callAPI.php**](https://github.com/GRC-Contact/api_php/blob/master/callAPI.php).

![Creating a GRC Contact account] (https://www.grc-contact.fr/doc/grc-home.JPG)


2. Copy and paste the source / include the **callAPI.php** (https://github.com/GRC-Contact/api_php/blob/master/callAPI.php) in your php code.

3. You need to provide 4 paramaters to the callAPI function. They are $entity$, $data$,$method$, $content-type$.

- **$entity** should be one of *"contacts", "contacts/{id}","tasks", "tasks/{id}", "events", "events/{id}", "contacts/search/email/{email}"* depending on requirement.


-  **$data** must be a stringified JSON.
  ```javascript
  $data = array(
    ...
  );
  
  $data = json_encode($data);
  ```

- **$method** can be set to
  
      POST to create an entity (contact, task, event,...).
      
      GET to fetch an entity.
      
      PUT to update an entity.
      
      DELETE to remove an entity.

- **$content-type** can be set to
  
  application/json.

  application/x-www-form-urlencoded

##Usage


Response is stringified json, can use json_decode to change to json as below example:

```javascript
$result = callAPI("contacts/007", null, "GET", "application/json");
$result = json_decode($result, false, 512, JSON_BIGINT_AS_STRING);
$contact_lastname = $result->lastname;
echo $contact_lastname); // displays "BOND"
``` 



## 1. Events

#### 1.1 To list events
TODO
#### 1.2 To fetch an event
TODO
#### 1.3 To create a event

```javascript
$event_json = array(
  "date_start"=>2017-03-15 17:30:00, //datetime (YYYY-MM-DD HH:MM:SS)
  "date_end"=>2017-03-15 17:45:00, //datetime (YYYY-MM-DD HH:MM:SS)
  "all_day"=>false, //bool (true or false)
  "type_id"=>0 , //int (default NULL)
  "objet"=>"Title of event" , //string (default NULL)
  "description"=>"Long text describing this event", //string (default NULL)
  "place"=> ,//string (default NULL)
  "et_id"=> //int (company id attached to the event, default NULL)
);

$event_json = json_encode($event_json);
callAPI("events", $event_json, "POST", "application/json");
```

#### 1.4 To delete a event

```javascript
callAPI("events/123456", null, "DELETE", "application/json");
```

#### 1.5 To update a event

```javascript
$event_json = array(
  "id"=>123456,
  "start"=>1414155679,
  "end"=>1414328479,
  "title"=>"this is a test event",
  "contacts"=>array(5722721933590528),
  "allDay"=>false
);

$event_json = json_encode($event_json);
curl_wrap("events", $event_json, "PUT", "application/json");
```

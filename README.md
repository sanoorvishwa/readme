---
title: |

  \
---

# Purpose

This document describes the API and endpoint analysis done on Zendesk
developer portal. The purpose of this document is to provide
authentication details and API / Connector development between Zendesk
and Adobe experience Launch.

# Key Activities

This section provides a summary of all analysis activities performed
on Zendesk

 

  -------------------------------------------------------------------------------
  **Sl. No**   **Activity**
  ------------ ------------------------------------------------------------------
  1            Understanding the business of zendesk

  2            Creating a test business account to access API endpoints 

  3            Identify Authentication API and available authentication methods 

  4            Connect to endpoints using Postman tool and analyze data 

  5            Identify all relevant available event data endpoints and the data
               schema

  6            Select endpoints to build edge extensions. 
  -------------------------------------------------------------------------------

 

# About the Zendesk Destination/Products 

Zendesk is a service-first CRM company that builds software designed to
improve customer relationships.

A listing of products available from Zendesk

  -----------------------------------------------------------------------
  **Names**       **Description**
  --------------- -------------------------------------------------------
  Zendesk for     Zendesk provides the complete customer service
  Service         solution. It Provides customer interaction messaging,
                  live chat, social, email, or voice. Builds an
                  integrated help center and community forum. Uses
                  automation and AI-powered bots to help customers

  Zendesk for     Zendesk Sell is an easy-to-love sales tool designed to
  Sales           help sales teams boost productivity, make data-driven
                  decisions, and deliver better customer experiences.
  -----------------------------------------------------------------------

# Customer Prerequisites

Zendesk Customers should obtain a Zendesk Support account (also called
subdomain) and use either email (user id) and password or api
token/OAuth token for API access and authentication. Click
[here](https://www.zendesk.com/register/?utm_source=google&utm_medium=Search-Paid&utm_network=g&utm_campaign=SE_AW_AP_IN_EN_N_Sup_Brand_TM_Beta_D_H&matchtype=b&utm_term=%2Bzendesk&utm_content=547295512551&utm_adgroup=&gclsrc=aw.ds&&theme=&gclid=EAIaIQobChMIobvlza2r9QIVJdWWCh1kRwGHEAAYASACEgIAZ_D_BwE#step-1)
to create the Zendesk account.

# 5. Authentication {#authentication .list-paragraph}

## 5.1. Authentication Model {#authentication-model .list-paragraph}

Authentication model supported is basic, API Token and OAuth.

Authorization: Bearer {YOUR_TOKEN}

+---+---+---+--------------------------------------------------------------+
| * | * |   | **Notes**                                                    |
| * | * |   |                                                              |
| S | A |   |                                                              |
| l | u |   |                                                              |
| . | t |   |                                                              |
| N | h |   |                                                              |
| o | e |   |                                                              |
| * | n |   |                                                              |
| * | t |   |                                                              |
|   | i |   |                                                              |
|   | c |   |                                                              |
|   | a |   |                                                              |
|   | t |   |                                                              |
|   | i |   |                                                              |
|   | o |   |                                                              |
|   | n |   |                                                              |
|   | * |   |                                                              |
|   | * |   |                                                              |
+===+===+===+==============================================================+
| 1 | B |   | Email (userid)/password                                      |
|   | a |   |                                                              |
|   | s |   | Authorization: Basic {base64-encoded-string}                 |
|   | i |   |                                                              |
|   | c |   | Eg: jdoe@example.com:pa\$\$w0rd                              |
+---+---+---+--------------------------------------------------------------+
| 2 | A |   | {email_address}/token:{api_token}                            |
|   | P |   |                                                              |
|   | I |   | Authorization: Basic {base64-encoded-string}                 |
|   | T |   |                                                              |
|   | o |   |                                                              |
|   | k |   |                                                              |
|   | e |   |                                                              |
|   | n |   |                                                              |
+---+---+---+--------------------------------------------------------------+
| 3 | O | * | POST /services/oauth2/token HTTP/1.1                         |
|   | A | * |                                                              |
|   | u | G | Host: login.salesforce.com                                   |
|   | t | r |                                                              |
|   | h | a | Content-length: 307                                          |
|   | 2 | n |                                                              |
|   | . | t | Content-type: application/x-www-form-urlencoded\             |
|   | 0 | T | \                                                            |
|   |   | y | \                                                            |
|   |   | p | grant_type=authorization_c                                   |
|   |   | e | ode&code=aPrx0jWjRo8KRXssupkuHuwgOR7oRyHBTpqXzhsbOs_voQQqODH |
|   |   | * | BKsGONODW5ddc1TVRSOtAag==&client_id=3MVG9pRzvMkjMb6k63.Qu_e2 |
|   |   | * | UnUxndLSyFcsIRdmcl50t3FQlct2BkJPxeSZWF.HU1FwS8vsqCviB_xqp5bw |
|   |   |   | 7&client_secret=\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*&redir |
|   |   |   | ect_uri=https%3A%2F%2Fopenidconnect.herokuapp.com%2Fcallback |
+---+---+---+--------------------------------------------------------------+
|   |   | O |                                                              |
|   |   | p |                                                              |
|   |   | e |                                                              |
|   |   | n |                                                              |
|   |   | I |                                                              |
|   |   | d |                                                              |
|   |   | C |                                                              |
|   |   | o |                                                              |
|   |   | n |                                                              |
|   |   | n |                                                              |
|   |   | e |                                                              |
|   |   | c |                                                              |
|   |   | t |                                                              |
+---+---+---+--------------------------------------------------------------+
|   |   | P | https://login.salesforce.com/services/oauth2/token           |
|   |   | a |                                                              |
|   |   | s | -d \'grant_type=password\' -d \'client_id=consumer-key\' -d  |
|   |   | s | \'client_secret=consumer-secret\' -d                         |
|   |   | w | \'username=my-login@domain.com\' -d \'password=my-password\' |
|   |   | o |                                                              |
|   |   | r | -X POST                                                      |
|   |   | d |                                                              |
|   |   | c |                                                              |
|   |   | r |                                                              |
|   |   | e |                                                              |
|   |   | d |                                                              |
|   |   | e |                                                              |
|   |   | n |                                                              |
|   |   | t |                                                              |
|   |   | i |                                                              |
|   |   | a |                                                              |
|   |   | l |                                                              |
|   |   | s |                                                              |
+---+---+---+--------------------------------------------------------------+
|   |   | I | https://login.salesforce.com/servi                           |
|   |   | m | ces/oauth2/token?grant_type=password&client_id=\<\<client_id |
|   |   | p | \>\>&client_secret=\<\<client_secret \>\>[&username=\<\<     |
|   |   | l | username \>\>&password=\<\<password                          |
|   |   | i | \>\>](mailto:&username=praveen.thota0                        |
|   |   | c | 1@infosys.com&password=Iamhere@2021gIpjqNzlgF67bhX7joVuTZ1P) |
|   |   | i |                                                              |
|   |   | t |                                                              |
|   |   | f |                                                              |
|   |   | l |                                                              |
|   |   | o |                                                              |
|   |   | w |                                                              |
+---+---+---+--------------------------------------------------------------+

Note: Salesforce OAuth details are available
[here](https://support.zendesk.com/hc/en-us/articles/4408845965210)

# Potential Zendesk Destinations of Digital Behavior

+-------------+---------------------+--------------------+------------+
|             | **Description**     | **Major Features** | *          |
|             |                     |                    | *Reference |
|             |                     |                    | Links**    |
+=============+=====================+====================+============+
| Custom Data | The Events API lets | -   Create an      | [Events    |
| -- Events   | you build a         |     event          | API](ht    |
| API         | timeline of all     |                    | tps://deve |
|             | your customers'     | -   Tracking       | loper.zend |
|             | interactions from   |     events         | esk.com/do |
|             | any source. An      |                    | cumentatio |
|             | event can be any    | -   Accessing      | n/custom-d |
|             | programmatic event  |     events         | ata/events |
|             | that your           |                    | /getting-s |
|             | application or      | -   Deleting       | tarted-wit |
|             | system can          |     events         | h-events/) |
|             | associate with a    |                    |            |
|             | user.               |                    |            |
+-------------+---------------------+--------------------+------------+
| Custom Data | The Profiles API    | -   Create a       | [Profiles  |
| -- Profiles | allows you to       |     profile        | A          |
| API         | create a single     |                    | PI](https: |
|             | view of a customer  | -   Get a profile  | //develope |
|             | across applications |                    | r.zendesk. |
|             | and systems. A      | -   Update a       | com/docume |
|             | profile can contain |     profile        | ntation/cu |
|             | the various         |                    | stom-data/ |
|             | identities of a     |                    | profiles/g |
|             | user in different   |                    | etting-sta |
|             | applications and    |                    | rted-with- |
|             | systems.            |                    | profiles/) |
+-------------+---------------------+--------------------+------------+
| Custom Data | Custom Objects API  | -   Defining a     | [Custom    |
| -- Custom   | is used to create,  |     custom object  | Objects    |
| Objects API | read, update, and   |     type           | API        |
|             | delete objects that |                    | ](https:// |
|             | a customer creates. | -   Adding object  | developer. |
|             | It can also be used |     records        | zendesk.co |
|             | to define and       |                    | m/document |
|             | manage              | -   Modeling your  | ation/cust |
|             | relationships with  |     data           | om-data/cu |
|             | other objects,      |                    | stom-objec |
|             | including native    | -   Retrieving     | ts/getting |
|             | Zendesk objects     |     related        | -started-w |
|             | like tickets and    |     objects        | ith-custom |
|             | users.              |                    | -objects/) |
+-------------+---------------------+--------------------+------------+
|             |                     | -                  |            |
+-------------+---------------------+--------------------+------------+
| Ticketing   | Automatically       | -   Create Ticket  | [Ticketing |
|             | create ticket in    |                    | ](https:// |
|             | Zendesk. . Tickets  | -   Update Ticket  | developer. |
|             | can originate from  |                    | zendesk.co |
|             | a number of         | -   Delete Ticket  | m/api-refe |
|             | channels, including |                    | rence/tick |
|             | email, Help Center, |                    | eting/intr |
|             | chat, phone call,   |                    | oduction/% |
|             | Twitter, Facebook,  |                    | 23security |
|             | or the API. All     |                    | -and-authe |
|             | tickets have a core |                    | ntication) |
|             | set of properties.  |                    |            |
+-------------+---------------------+--------------------+------------+

## 5.1 Error Codes {#error-codes .list-paragraph}

Requesting an Authorization via /oauth2/authorize

  ---------------------------------------------------------------------------
  **Error Code**              **HTTP Status Code**    **Meaning**
  --------------------------- ----------------------- -----------------------
  invalid_request             400                     The request is
                                                      malformed, a required
                                                      parameter is missing or
                                                      a parameter has an
                                                      invalid value.

  unauthorized_client         400                     The client is not
                                                      authorized.

  access_denied               400                     The resource owner
                                                      denied the request for
                                                      authorization.

  unsupported_response_type   400                     Unsupported response
                                                      type.

  invalid_scope               400                     The scope is malformed
                                                      or invalid.

  server_error                400                     Unexpected error.

  temporarily_unavailable     400                     The authorization
                                                      server is not able to
                                                      handle the request.
  ---------------------------------------------------------------------------

Requesting an Access Token via /oauth2/token

  ------------------------------------------------------------------------
  **Error Code**           **HTTP Status Code**    **Meaning**
  ------------------------ ----------------------- -----------------------
  invalid_request          400                     The request is
                                                   malformed, a required
                                                   parameter is missing or
                                                   a parameter has an
                                                   invalid value.

  invalid_client           401                     Client authentication
                                                   failed.

  invalid_grant            400                     Invalid authorization
                                                   grant, grant invalid,
                                                   grant expired, or grant
                                                   revoked.

  unauthorized_client      400                     Client is not
                                                   authorized to use the
                                                   grant.

  unsupported_grant_type   400                     Authorization grant is
                                                   not supported by the
                                                   Authorization Server.

  invalid_scope            400                     The scope is malformed
                                                   or invalid.
  ------------------------------------------------------------------------

Revoking a Token via /oauth2/token/revoke

  ------------------------------------------------------------------------
  **Error Code**           **HTTP Status Code**    **Meaning**
  ------------------------ ----------------------- -----------------------
  invalid_request          400                     The request is
                                                   malformed, a required
                                                   parameter is missing or
                                                   a parameter has an
                                                   invalid value.

  invalid_client           401                     Client authentication
                                                   failed.

  invalid_grant            400                     Invalid authorization
                                                   grant, grant invalid,
                                                   grant expired, or grant
                                                   revoked.

  unauthorized_client      400                     Client is not
                                                   authorized to use the
                                                   grant.

  unsupported_grant_type   400                     Authorization grant is
                                                   not supported by the
                                                   Authorization Server.

  invalid_scope            400                     The scope is malformed
                                                   or invalid.

  unsupported_token_type   400                     The Authorization
                                                   Server does not support
                                                   revocation of the
                                                   presented token type.
  ------------------------------------------------------------------------

# Zendesk Events API

  -------------------------------------------------------------------------------------------------------------------------------------------------
  **Endpoints**                  **Functionality**   **Request**   **Sample cURL**                                               **Response**
  ------------------------------ ------------------- ------------- ------------------------------------------------------------- ------------------
  /api/v2/user_profiles/events   create an event by  POST          curl                                                          {"status":
                                 posting information               https://{subdomain}.zendesk.com/api/v2/user_profiles/events   "received"}
                                 about the event and               \\ -d \@event.json \\ -H "Content-Type: application/json" \\  
                                 the person who                    -v -u {email_address}:{password} -X POST                      
                                 triggered it                                                                                    

  -------------------------------------------------------------------------------------------------------------------------------------------------

## 6.1 Event Object Attributes {#event-object-attributes .list-paragraph}

> Events are represented as JSON objects with the following properties:

  ---------------------------------------------------------------------------------------------------------------
  **Name**      **Type**   **Read-only**   **Mandatory**                   **Description**
  ------------- ---------- --------------- --------------- --------------- --------------------------------------
  created_at    string     false           false                           ISO-8601 compliant date-time
                                                                           reflecting the time the event was
                                                                           created. If not set, the API sets the
                                                                           value when it receives the event

  description   string     false           false                           An event description

  id            string     true            false                           ID of the event

  properties    object     false           true            A custom JSON   
                                                           object with     
                                                           details about   
                                                           the event. Must 
                                                           comply with the 
                                                           JSON Schema     
                                                           specification   

  received_at   string     true            false           ISO-8601        
                                                           compliant       
                                                           date-time       
                                                           reflecting the  
                                                           time the event  
                                                           was received    

  source        string     false           true            Application     
                                                           which sent the  
                                                           event. Note:    
                                                           \'zendesk\' is  
                                                           a protected     
                                                           source name for 
                                                           Zendesk         
                                                           standard        
                                                           events. Any     
                                                           attempts to use 
                                                           this source     
                                                           when creating   
                                                           an event        
                                                           results in an   
                                                           error           

  type          string     false           true            Event name      
  ---------------------------------------------------------------------------------------------------------------

An event consists of a JSON object describing both the event and the
user who triggered the event.

  -----------------------------------------------------------------------------------------------------------------------------------
  **Name**     **Type**      **Required**   **Description**
  ------------ ------------- -------------- -----------------------------------------------------------------------------------------
  profile      object        yes            The user who triggered the event. For more information, see [profile
                                            object](https://developer.zendesk.com/rest_api/docs/sunshine/events_api#profile-object)

  event        object        yes            The event triggered by the user. For more information, see the [event
                                            object](https://developer.zendesk.com/rest_api/docs/sunshine/events_api#json-format)
  -----------------------------------------------------------------------------------------------------------------------------------

## 6.2 Profile Object {#profile-object .list-paragraph}

A profile object describes a user associated with an application or
system. The object has the following properties:

  ----------------------------------------------------------------------------------------------------------------------------------------
  **Name**      **Type**      **Required**   **Description**
  ------------- ------------- -------------- ---------------------------------------------------------------------------------------------
  source        string        yes            The product or service associated with the profile. For example, \"Support\", \"Salesforce\",
                                             or \"Chat\"

  type          string        yes            The type of profile. For example, \"Contact\" or \"Lead\"

  identifiers   object        yes            One or more user identities. See the [identifiers
                                             array](https://developer.zendesk.com/rest_api/docs/sunshine/profiles_api#identifiers-array)
  ----------------------------------------------------------------------------------------------------------------------------------------

Example request body:

{

\"profile\": {

\"source\": \"shoppingnow\",

\"type\": \"customer\",

\"identifiers\": \[

{

\"type\": \"shoppingnow_id\",

\"value\": \"361959350832\"

},

{

\"type\": \"external_id\",

\"value\": \"0987654321\"

}

\]

},

\"event\": {

\"source\": \"shoppingnow\",

\"type\": \"order_completed\",

\"created_at\": \"2018-11-05T22:26:00Z\",

\"description\": \"Added item to cart\",

\"properties\": {

\"item\": {

\"name\": \"Canon 429 EOS HD\",

\"query\": \"camera\",

\"price\": \"499.99\"

},

\"shipping\": {

\"eta_date\": \"2019/01/02\",

\"address\": {

\"address1\": \"1019 Market Street\",

\"city\": \"San Francisco\",

\"state\": \"CA\",

\"zipcode\": \"94103\"

}

}

}

}

}

## 6.3 Request Headers {#request-headers .list-paragraph}

Bearer Token needs to be send in header if opting for oauth token for
authorization

## 6.4 Supporting data Entities/Dictionary {#supporting-data-entitiesdictionary .list-paragraph}

**Identifiers**

The identifiers array consists of one or more values used to identify a
person in an application or system. Each identifier consists of a type
and a value property which are arbitrary. For example, an identifier can
be of type \"member_id\" with a value of \"0634335\".

It is recommended to submit the identifier types email, Facebook, phone,
SDK, Twitter, or external ID as \"email\", \"facebook\",
\"phone_number\", \"sdk\", \"twitter\", and \"external_id\",
respectively

  -----------------------------------------------------------------------
  **Identifier type **If type not     **Profile Name**  **Example**
  used**            present**                           
  ----------------- ----------------- ----------------- -----------------
  "email"           \-                Email address     foo@bar.foo

  "external_id"     "email"           "User" +          User FooBar123
                                      external_id       

  "phone_number"    "external_id"     "User" +          User 1111 222 333
                                      phone_number      

  "twitter"         "phone_number"    "Twitter user" +  Twitter user
                                      username          Foobar

  "facebook"        "twitter"         "Facebook user" + Facebook user
                                      username          Foobar

  "sdk"             "facebook"        "SDK user" +      SDK user
                                      sdk_value         FoobarSDK
  -----------------------------------------------------------------------

## 6.5 Event Parameters {#event-parameters .list-paragraph}

+--------+----------------------+-------------------------------------+
| **Data | *                    | **Notes**                           |
| P      | *Required/Optional** |                                     |
| oint** |                      |                                     |
+========+======================+=====================================+
| source | Required             | A user-defined name for the         |
|        |                      | application or system where the     |
|        |                      | events occur.                       |
|        |                      |                                     |
|        |                      | Example: \"source\": \"acme\"       |
+--------+----------------------+-------------------------------------+
| type   | Required             | A user-defined name that lets you   |
|        |                      | create different kinds of events    |
|        |                      | from a given source                 |
|        |                      |                                     |
|        |                      | Example: \"type\": \"cart\"         |
+--------+----------------------+-------------------------------------+
| descr  | Optional             | A description of the event to give  |
| iption |                      | more context to human consumers of  |
|        |                      | the data.                           |
|        |                      |                                     |
|        |                      | Example: \"description\":           |
|        |                      | \"Customer enabled 2-factor         |
|        |                      | authentication\"                    |
+--------+----------------------+-------------------------------------+
| prop   | Required             | A user-defined JSON object with     |
| erties |                      | details about the event. A property |
|        |                      | is typically information about the  |
|        |                      | event that\'s used in the source    |
|        |                      | application or system.              |
|        |                      |                                     |
|        |                      | Example:                            |
|        |                      |                                     |
|        |                      | \"properties\": {                   |
|        |                      |                                     |
|        |                      | \"passcode_preference\": \"SMS\"    |
|        |                      |                                     |
|        |                      | }                                   |
|        |                      |                                     |
|        |                      | \"properties\": {                   |
|        |                      |                                     |
|        |                      | \"customer\": {                     |
|        |                      |                                     |
|        |                      | \"display_name\": \"Go to customer  |
|        |                      | profile\...\",                      |
|        |                      |                                     |
|        |                      | \"url\":                            |
|        |                      | \"h                                 |
|        |                      | ttps://crm.acme.com/customers/123\" |
|        |                      |                                     |
|        |                      | }                                   |
+--------+----------------------+-------------------------------------+

## 6.6 Sample Event Request {#sample-event-request .list-paragraph}

+---------------+-------------------+----------------------------------+
| **            | **Request**       | **cURL**                         |
| Description** |                   |                                  |
+===============+===================+==================================+
| This will     | POST              | curl \--location \--request POST |
| send event    |                   | \'[https:                        |
| data to       | [https://d        | //d3v-dxinfosys.zendesk.com/api/ |
| zendesk       | 3v-dxinfosys.zend | v2/user_profiles/events\'](https |
| Events        | esk.com/api/v2/us | ://d3v-dxinfosys.zendesk.com/api |
| manager       | er_profiles/event | /v2/user_profiles/events%27) \\\ |
|               | s](https://d3v-dx | \--header \'Content-Type:        |
|               | infosys.zendesk.c | application/json\' \\\           |
|               | om/api/v2/user_pr | \--header \'Authorization:       |
|               | ofiles/events%27) | Bearer                           |
|               |                   | 53                               |
|               |                   | 24f6bddbd7e49d05e3e145fe9b4d759f |
|               |                   | 54bce5b86e3f2cf3da7b4f204d6943\' |
|               |                   | \\\                              |
|               |                   | \--header \'Cookie:              |
|               |                   | \_\_cfruid=545ea0e9c48467e724305 |
|               |                   | a1b1dcb4068dca1db86-1641978609\' |
|               |                   | \\\                              |
|               |                   | \--data-raw \'{\                 |
|               |                   | \"profile\": {\                  |
|               |                   | \"source\": \"123qw33\",\        |
|               |                   | \"type\": \"meow\",\             |
|               |                   | \"identifiers\": \[\             |
|               |                   | {\                               |
|               |                   | \"type\": \"email\",\            |
|               |                   | \"value\":                       |
|               |                   | \"test123@example.com\"\         |
|               |                   | }\                               |
|               |                   | \]\                              |
|               |                   | },\                              |
|               |                   | \"event\": {\                    |
|               |                   | \"source\": \"123qw33\",\        |
|               |                   | \"type\": \"meow\",\             |
|               |                   | \"description\": \"123 new test  |
|               |                   | source event meow\",\            |
|               |                   | \"properties\": {\               |
|               |                   | \"passcode_preference\":         |
|               |                   | \"Call\"\                        |
|               |                   | }\                               |
|               |                   | }\                               |
|               |                   | }\'                              |
+---------------+-------------------+----------------------------------+

# Open Questions

-   How to handle error scenarios from Zendesk api response?

Boundaries:

Custom Objects, Profiles, and Events API requests per minute 250 - 1000
per minute as per plan level.

# References

For API Reference Documentation, Click
[here](https://developer.zendesk.com/api-reference/)

# Appendix

Zendesk Events API

+--------+---------+------+----------------------+-------------------+
| *      | **F     | **R  | **cURL**             | **Response**      |
| *Endpo | unction | eque |                      |                   |
| ints** | ality** | st** |                      |                   |
+========+=========+======+======================+===================+
| /api   | create  | POST | curl                 | {\"status\":      |
| /v2/us | an      |      | https://{subdomain}  | \"received\"}     |
| er_pro | event   |      | .zendesk.com/api/v2/ |                   |
| files/ | by      |      | user_profiles/events |                   |
| events | posting |      | \\ -d \@event.json   |                   |
|        | info    |      | \\ -H                |                   |
|        | rmation |      | \"Content-Type:      |                   |
|        | about   |      | application/json\"   |                   |
|        | the     |      | \\ -v -u             |                   |
|        | event   |      | {email               |                   |
|        | and the |      | _address}:{password} |                   |
|        | person  |      | -X POST              |                   |
|        | who     |      |                      |                   |
|        | tr      |      |                      |                   |
|        | iggered |      |                      |                   |
|        | it      |      |                      |                   |
+--------+---------+------+----------------------+-------------------+
| /api/  | look up | GET  | curl                 | Status: 200 OK    |
| v2/use | a       |      | \"https://{          |                   |
| r_prof | cust    |      | subdomain}.zendesk.c | {\"events\":      |
| iles/e | omer\'s |      | om/api/v2/user_profi | \[{\"id\":        |
| vents? | profile |      | les/events?identifie | \"5c42123e98      |
|        | with an |      | r=acme:customer:emai | 326c0001b0b25c\", |
| ident  | ide     |      | l:jdoe@example.com\" | \"type\":         |
| ifier= | ntifier |      | \\ -v -u             | \"2fa_enabled\",  |
| {ident | query.  |      | {email               | \"source\":       |
| ifier_ |         |      | _address}:{password} | \"acme\",         |
| query} |         |      |                      | \"description\":  |
|        |         |      |                      | \"Customer        |
|        |         |      |                      | enabled 2-factor  |
|        |         |      |                      | authentication\", |
|        |         |      |                      | \"created_at\":   |
|        |         |      |                      | \"2020-03-30      |
|        |         |      |                      | T04:37:34.851Z\", |
|        |         |      |                      | \"received_at\":  |
|        |         |      |                      | \"2019-03-30      |
|        |         |      |                      | T04:37:34.851Z\", |
|        |         |      |                      | \"properties\": { |
|        |         |      |                      | \"passc           |
|        |         |      |                      | ode_preference\": |
|        |         |      |                      | \"SMS\" } } \],   |
|        |         |      |                      | \"links\": \[ {   |
|        |         |      |                      | \"next\":\"\" }   |
|        |         |      |                      | \] }              |
+--------+---------+------+----------------------+-------------------+
| /api   | delete  | DE   | curl                 | Status 204 OK     |
| /v2/us | events  | LETE | \                    |                   |
| er_pro | stored  |      | "https://coolbikes.z |                   |
| files/ | in      |      | endesk.com/api/v2/us |                   |
| {profi | Zendesk |      | er_profiles/01E1G0NJ |                   |
| le_id} | by      |      | SQPNPZRV096JXKXFAA\" |                   |
|        | d       |      | \\                   |                   |
|        | eleting |      |                      |                   |
|        | the     |      | -v -u                |                   |
|        | profile |      | devs@coo             |                   |
|        | ass     |      | lbikes.com:t1retube5 |                   |
|        | ociated |      | -X DELETE            |                   |
|        | with    |      |                      |                   |
|        | the     |      |                      |                   |
|        | events. |      |                      |                   |
+--------+---------+------+----------------------+-------------------+

**Business**

AEP uses the Events API of Zendesk to store and access user event data
generated in one or more systems or applications used by different
organization. For example, Zendesk can track user events that occur in a
company\'s business-to-consumer (B2C) application as well as in a
third-party app that a company uses for customer billing.

Zendesk can then use the event data to build solutions that create
better relationships with your customers. The possibilities include:

-   Giving your company more context about the customer in one-on-one
    conversations

-   Following up with the customer after certain events

-   Providing a more personalized user experience in your application or
    system

The Events API lets you build a timeline of all your customers\'
interactions from any source. An event can be any programmatic event
that your application or system can associate with a user. Examples
include purchase transactions, website visits, or customer service
interactions. Each event is associated with a customer who triggered the
event.

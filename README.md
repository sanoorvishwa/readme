# Purpose

This document describes the API and endpoint analysis done on Zendesk
developer portal. The purpose of this document is to provide
authentication details and API / Connector development between Zendesk
and Adobe experience Launch.

# Key Activities

This section provides a summary of all analysis activities performed
on Zendesk

 

| **Sl. No** | **Activity**                                                             |
|------------|--------------------------------------------------------------------------|
| 1          | Understanding the business of zendesk                                    |
| 2          | Creating a test business account to access API endpoints                 |
| 3          | Identify Authentication API and available authentication methods         |
| 4          | Connect to endpoints using Postman tool and analyze data                 |
| 5          | Identify all relevant available event data endpoints and the data schema |
| 6          | Select endpoints to build edge extensions.                               |

 

# About the Zendesk Destination/Products 

Zendesk is a service-first CRM company that builds software designed to
improve customer relationships.

A listing of products available from Zendesk

| **Names**           | **Description**                                                                                                                                                                                                                                      |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Zendesk for Service | Zendesk provides the complete customer service solution. It Provides customer interaction messaging, live chat, social, email, or voice. Builds an integrated help center and community forum. Uses automation and AI-powered bots to help customers |
| Zendesk for Sales   | Zendesk Sell is an easy-to-love sales tool designed to help sales teams boost productivity, make data-driven decisions, and deliver better customer experiences.                                                                                     |

# Customer Prerequisites

Zendesk Customers should obtain a Zendesk Support account (also called
subdomain) and use either email (user id) and password or api
token/OAuth token for API access and authentication. Click
[here](https://www.zendesk.com/register/?utm_source=google&utm_medium=Search-Paid&utm_network=g&utm_campaign=SE_AW_AP_IN_EN_N_Sup_Brand_TM_Beta_D_H&matchtype=b&utm_term=%2Bzendesk&utm_content=547295512551&utm_adgroup=&gclsrc=aw.ds&&theme=&gclid=EAIaIQobChMIobvlza2r9QIVJdWWCh1kRwGHEAAYASACEgIAZ_D_BwE#step-1)
to create the Zendesk account.

# 5. Authentication [authentication]

## 5.1. Authentication Model [authentication-model]

Authentication model supported is basic, API Token and OAuth.

Authorization: Bearer {YOUR_TOKEN}

<table>
<colgroup>
<col style="width: 3%" />
<col style="width: 3%" />
<col style="width: 5%" />
<col style="width: 88%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Sl.No</strong></th>
<th colspan="2"><strong>Authentication</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td colspan="2">Basic</td>
<td><p>Email (userid)/password</p>
<p>Authorization: Basic {base64-encoded-string}</p>
<p>Eg: jdoe@example.com:pa$$w0rd</p></td>
</tr>
<tr class="even">
<td>2</td>
<td colspan="2">API Token</td>
<td><p>{email_address}/token:{api_token}</p>
<p>Authorization: Basic {base64-encoded-string}</p></td>
</tr>
<tr class="odd">
<td rowspan="4">3</td>
<td rowspan="4">OAuth 2.0</td>
<td><strong>Grant Type</strong></td>
<td rowspan="2"><p>POST /services/oauth2/token HTTP/1.1</p>
<p>Host: login.salesforce.com</p>
<p>Content-length: 307</p>
<p>Content-type: application/x-www-form-urlencoded<br />
<br />
<br />
grant_type=authorization_code&amp;code=aPrx0jWjRo8KRXssupkuHuwgOR7oRyHBTpqXzhsbOs_voQQqODHBKsGONODW5ddc1TVRSOtAag==&amp;client_id=3MVG9pRzvMkjMb6k63.Qu_e2UnUxndLSyFcsIRdmcl50t3FQlct2BkJPxeSZWF.HU1FwS8vsqCviB_xqp5bw7&amp;client_secret=*******************&amp;redirect_uri=https%3A%2F%2Fopenidconnect.herokuapp.com%2Fcallback</p></td>
</tr>
<tr class="even">
<td>Open Id Connect</td>
</tr>
<tr class="odd">
<td>Password credentials</td>
<td><p>https://login.salesforce.com/services/oauth2/token</p>
<p>-d 'grant_type=password' -d 'client_id=consumer-key' -d
'client_secret=consumer-secret' -d 'username=my-login@domain.com' -d
'password=my-password'</p>
<p>-X POST</p></td>
</tr>
<tr class="even">
<td>Implicit flow</td>
<td>https://login.salesforce.com/services/oauth2/token?grant_type=password&amp;client_id=&lt;&lt;client_id
&gt;&gt;&amp;client_secret=&lt;&lt;client_secret &gt;&gt;<a
href="mailto:&amp;username=praveen.thota01@infosys.com&amp;password=Iamhere@2021gIpjqNzlgF67bhX7joVuTZ1P">&amp;username=&lt;&lt;
username &gt;&gt;&amp;password=&lt;&lt;password &gt;&gt;</a></td>
</tr>
</tbody>
</table>

Note: Salesforce OAuth details are available
[here](https://support.zendesk.com/hc/en-us/articles/4408845965210)

# Potential Zendesk Destinations of Digital Behavior

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 31%" />
<col style="width: 29%" />
<col style="width: 18%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th><strong>Description</strong></th>
<th><strong>Major Features</strong></th>
<th><strong>Reference Links</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Custom Data – Events API</td>
<td>The Events API lets you build a timeline of all your customers’
interactions from any source. An event can be any programmatic event
that your application or system can associate with a user.</td>
<td><ul>
<li><p>Create an event</p></li>
<li><p>Tracking events</p></li>
<li><p>Accessing events</p></li>
<li><p>Deleting events</p></li>
</ul></td>
<td><a
href="https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/">Events
API</a></td>
</tr>
<tr class="even">
<td>Custom Data – Profiles API</td>
<td>The Profiles API allows you to create a single view of a customer
across applications and systems. A profile can contain the various
identities of a user in different applications and systems.</td>
<td><ul>
<li><p>Create a profile</p></li>
<li><p>Get a profile</p></li>
<li><p>Update a profile</p></li>
</ul></td>
<td><a
href="https://developer.zendesk.com/documentation/custom-data/profiles/getting-started-with-profiles/">Profiles
API</a></td>
</tr>
<tr class="odd">
<td>Custom Data – Custom Objects API</td>
<td>Custom Objects API is used to create, read, update, and delete
objects that a customer creates. It can also be used to define and
manage relationships with other objects, including native Zendesk
objects like tickets and users.</td>
<td><ul>
<li><p>Defining a custom object type</p></li>
<li><p>Adding object records</p></li>
<li><p>Modeling your data</p></li>
<li><p>Retrieving related objects</p></li>
</ul></td>
<td><a
href="https://developer.zendesk.com/documentation/custom-data/custom-objects/getting-started-with-custom-objects/">Custom
Objects API</a></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td><ul>
<li></li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<td>Ticketing</td>
<td>Automatically create ticket in Zendesk. . Tickets can originate from
a number of channels, including email, Help Center, chat, phone call,
Twitter, Facebook, or the API. All tickets have a core set of
properties.</td>
<td><ul>
<li><p>Create Ticket</p></li>
<li><p>Update Ticket</p></li>
<li><p>Delete Ticket</p></li>
</ul></td>
<td><a
href="https://developer.zendesk.com/api-reference/ticketing/introduction/%23security-and-authentication">Ticketing</a></td>
</tr>
</tbody>
</table>

## 5.1 Error Codes [error-codes]

Requesting an Authorization via /oauth2/authorize

| **Error Code**            | **HTTP Status Code** | **Meaning**                                                                                    |
|---------------------------|----------------------|------------------------------------------------------------------------------------------------|
| invalid_request           | 400                  | The request is malformed, a required parameter is missing or a parameter has an invalid value. |
| unauthorized_client       | 400                  | The client is not authorized.                                                                  |
| access_denied             | 400                  | The resource owner denied the request for authorization.                                       |
| unsupported_response_type | 400                  | Unsupported response type.                                                                     |
| invalid_scope             | 400                  | The scope is malformed or invalid.                                                             |
| server_error              | 400                  | Unexpected error.                                                                              |
| temporarily_unavailable   | 400                  | The authorization server is not able to handle the request.                                    |

Requesting an Access Token via /oauth2/token

| **Error Code**         | **HTTP Status Code** | **Meaning**                                                                                    |
|------------------------|----------------------|------------------------------------------------------------------------------------------------|
| invalid_request        | 400                  | The request is malformed, a required parameter is missing or a parameter has an invalid value. |
| invalid_client         | 401                  | Client authentication failed.                                                                  |
| invalid_grant          | 400                  | Invalid authorization grant, grant invalid, grant expired, or grant revoked.                   |
| unauthorized_client    | 400                  | Client is not authorized to use the grant.                                                     |
| unsupported_grant_type | 400                  | Authorization grant is not supported by the Authorization Server.                              |
| invalid_scope          | 400                  | The scope is malformed or invalid.                                                             |

Revoking a Token via /oauth2/token/revoke

| **Error Code**         | **HTTP Status Code** | **Meaning**                                                                                    |
|------------------------|----------------------|------------------------------------------------------------------------------------------------|
| invalid_request        | 400                  | The request is malformed, a required parameter is missing or a parameter has an invalid value. |
| invalid_client         | 401                  | Client authentication failed.                                                                  |
| invalid_grant          | 400                  | Invalid authorization grant, grant invalid, grant expired, or grant revoked.                   |
| unauthorized_client    | 400                  | Client is not authorized to use the grant.                                                     |
| unsupported_grant_type | 400                  | Authorization grant is not supported by the Authorization Server.                              |
| invalid_scope          | 400                  | The scope is malformed or invalid.                                                             |
| unsupported_token_type | 400                  | The Authorization Server does not support revocation of the presented token type.              |

# Zendesk Events API

| **Endpoints**                | **Functionality**                                                                      | **Request** | **Sample cURL**                                                                                                                                                       | **Response**           |
|------------------------------|----------------------------------------------------------------------------------------|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| /api/v2/user_profiles/events | create an event by posting information about the event and the person who triggered it | POST        | curl https://{subdomain}.zendesk.com/api/v2/user_profiles/events \\ -d @event.json \\ -H “Content-Type: application/json” \\ -v -u {email_address}:{password} -X POST | {“status”: “received”} |

## 6.1 Event Object Attributes [event-object-attributes]

> Events are represented as JSON objects with the following properties:

| **Name**    | **Type** | **Read-only** | **Mandatory** |                                                                                                                                                                                      | **Description**                                                                                                                       |
|-------------|----------|---------------|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| created_at  | string   | false         | false         |                                                                                                                                                                                      | ISO-8601 compliant date-time reflecting the time the event was created. If not set, the API sets the value when it receives the event |
| description | string   | false         | false         |                                                                                                                                                                                      | An event description                                                                                                                  |
| id          | string   | true          | false         |                                                                                                                                                                                      | ID of the event                                                                                                                       |
| properties  | object   | false         | true          | A custom JSON object with details about the event. Must comply with the JSON Schema specification                                                                                    |                                                                                                                                       |
| received_at | string   | true          | false         | ISO-8601 compliant date-time reflecting the time the event was received                                                                                                              |                                                                                                                                       |
| source      | string   | false         | true          | Application which sent the event. Note: 'zendesk' is a protected source name for Zendesk standard events. Any attempts to use this source when creating an event results in an error |                                                                                                                                       |
| type        | string   | false         | true          | Event name                                                                                                                                                                           |                                                                                                                                       |

An event consists of a JSON object describing both the event and the
user who triggered the event.

| **Name** | **Type** | **Required** | **Description**                                                                                                                                              |
|----------|----------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| profile  | object   | yes          | The user who triggered the event. For more information, see [profile object](https://developer.zendesk.com/rest_api/docs/sunshine/events_api#profile-object) |
| event    | object   | yes          | The event triggered by the user. For more information, see the [event object](https://developer.zendesk.com/rest_api/docs/sunshine/events_api#json-format)   |

## 6.2 Profile Object [profile-object]

A profile object describes a user associated with an application or
system. The object has the following properties:

| **Name**    | **Type** | **Required** | **Description**                                                                                                                               |
|-------------|----------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| source      | string   | yes          | The product or service associated with the profile. For example, "Support", "Salesforce", or "Chat"                                           |
| type        | string   | yes          | The type of profile. For example, "Contact" or "Lead"                                                                                         |
| identifiers | object   | yes          | One or more user identities. See the [identifiers array](https://developer.zendesk.com/rest_api/docs/sunshine/profiles_api#identifiers-array) |

Example request body:

{

"profile": {

"source": "shoppingnow",

"type": "customer",

"identifiers": \[

{

"type": "shoppingnow_id",

"value": "361959350832"

},

{

"type": "external_id",

"value": "0987654321"

}

\]

},

"event": {

"source": "shoppingnow",

"type": "order_completed",

"created_at": "2018-11-05T22:26:00Z",

"description": "Added item to cart",

"properties": {

"item": {

"name": "Canon 429 EOS HD",

"query": "camera",

"price": "499.99"

},

"shipping": {

"eta_date": "2019/01/02",

"address": {

"address1": "1019 Market Street",

"city": "San Francisco",

"state": "CA",

"zipcode": "94103"

}

}

}

}

}

## 6.3 Request Headers [request-headers]

Bearer Token needs to be send in header if opting for oauth token for
authorization

## 6.4 Supporting data Entities/Dictionary [supporting-data-entitiesdictionary]

**Identifiers**

The identifiers array consists of one or more values used to identify a
person in an application or system. Each identifier consists of a type
and a value property which are arbitrary. For example, an identifier can
be of type "member_id" with a value of "0634335".

It is recommended to submit the identifier types email, Facebook, phone,
SDK, Twitter, or external ID as "email", "facebook", "phone_number",
"sdk", "twitter", and "external_id", respectively

| **Identifier type used** | **If type not present** | **Profile Name**           | **Example**          |
|--------------------------|-------------------------|----------------------------|----------------------|
| “email”                  | \-                      | Email address              | foo@bar.foo          |
| “external_id”            | “email”                 | “User” + external_id       | User FooBar123       |
| “phone_number”           | “external_id”           | “User” + phone_number      | User 1111 222 333    |
| “twitter”                | “phone_number”          | “Twitter user” + username  | Twitter user Foobar  |
| “facebook”               | “twitter”               | “Facebook user” + username | Facebook user Foobar |
| “sdk”                    | “facebook”              | “SDK user” + sdk_value     | SDK user FoobarSDK   |

## 6.5 Event Parameters [event-parameters]

<table>
<colgroup>
<col style="width: 13%" />
<col style="width: 32%" />
<col style="width: 53%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Data Point</strong></th>
<th><strong>Required/Optional</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>source</td>
<td>Required</td>
<td><p>A user-defined name for the application or system where the
events occur.</p>
<p>Example: "source": "acme"</p></td>
</tr>
<tr class="even">
<td>type</td>
<td>Required</td>
<td><p>A user-defined name that lets you create different kinds of
events from a given source</p>
<p>Example: "type": "cart"</p></td>
</tr>
<tr class="odd">
<td>description</td>
<td>Optional</td>
<td><p>A description of the event to give more context to human
consumers of the data.</p>
<p>Example: "description": "Customer enabled 2-factor
authentication"</p></td>
</tr>
<tr class="even">
<td>properties</td>
<td>Required</td>
<td><p>A user-defined JSON object with details about the event. A
property is typically information about the event that's used in the
source application or system.</p>
<p>Example:</p>
<p>"properties": {</p>
<p>"passcode_preference": "SMS"</p>
<p>}</p>
<p>"properties": {</p>
<p>"customer": {</p>
<p>"display_name": "Go to customer profile...",</p>
<p>"url": "https://crm.acme.com/customers/123"</p>
<p>}</p></td>
</tr>
</tbody>
</table>

## 6.6 Sample Event Request [sample-event-request]

<table>
<colgroup>
<col style="width: 22%" />
<col style="width: 28%" />
<col style="width: 48%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Description</strong></th>
<th><strong>Request</strong></th>
<th><strong>cURL</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>This will send event data to zendesk Events manager</td>
<td><p>POST</p>
<p><a
href="https://d3v-dxinfosys.zendesk.com/api/v2/user_profiles/events%27">https://d3v-dxinfosys.zendesk.com/api/v2/user_profiles/events</a></p></td>
<td>curl --location --request POST '<a
href="https://d3v-dxinfosys.zendesk.com/api/v2/user_profiles/events%27">https://d3v-dxinfosys.zendesk.com/api/v2/user_profiles/events'</a> \<br />
--header 'Content-Type: application/json' \<br />
--header 'Authorization: Bearer
5324f6bddbd7e49d05e3e145fe9b4d759f54bce5b86e3f2cf3da7b4f204d6943'
\<br />
--header 'Cookie:
__cfruid=545ea0e9c48467e724305a1b1dcb4068dca1db86-1641978609' \<br />
--data-raw '{<br />
"profile": {<br />
"source": "123qw33",<br />
"type": "meow",<br />
"identifiers": [<br />
{<br />
"type": "email",<br />
"value": "test123@example.com"<br />
}<br />
]<br />
},<br />
"event": {<br />
"source": "123qw33",<br />
"type": "meow",<br />
"description": "123 new test source event meow",<br />
"properties": {<br />
"passcode_preference": "Call"<br />
}<br />
}<br />
}'</td>
</tr>
</tbody>
</table>

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

<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 15%" />
<col style="width: 10%" />
<col style="width: 32%" />
<col style="width: 28%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Endpoints</strong></th>
<th><strong>Functionality</strong></th>
<th><strong>Request</strong></th>
<th><strong>cURL</strong></th>
<th><strong>Response</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>/api/v2/user_profiles/events</td>
<td>create an event by posting information about the event and the
person who triggered it</td>
<td>POST</td>
<td>curl https://{subdomain}.zendesk.com/api/v2/user_profiles/events \
-d @event.json \ -H "Content-Type: application/json" \ -v -u
{email_address}:{password} -X POST</td>
<td>{"status": "received"}</td>
</tr>
<tr class="even">
<td><p>/api/v2/user_profiles/events?</p>
<p>identifier={identifier_query}</p></td>
<td>look up a customer's profile with an identifier query.</td>
<td>GET</td>
<td>curl
"https://{subdomain}.zendesk.com/api/v2/user_profiles/events?identifier=acme:customer:email:jdoe@example.com"
\ -v -u {email_address}:{password}</td>
<td><p>Status: 200 OK</p>
<p>{"events": [{"id": "5c42123e98326c0001b0b25c", "type": "2fa_enabled",
"source": "acme", "description": "Customer enabled 2-factor
authentication", "created_at": "2020-03-30T04:37:34.851Z",
"received_at": "2019-03-30T04:37:34.851Z", "properties": {
"passcode_preference": "SMS" } } ], "links": [ { "next":"" } ]
}</p></td>
</tr>
<tr class="odd">
<td>/api/v2/user_profiles/{profile_id}</td>
<td>delete events stored in Zendesk by deleting the profile associated
with the events.</td>
<td>DELETE</td>
<td><p>curl
"https://coolbikes.zendesk.com/api/v2/user_profiles/01E1G0NJSQPNPZRV096JXKXFAA"
\</p>
<p>-v -u devs@coolbikes.com:t1retube5 -X DELETE</p></td>
<td>Status 204 OK</td>
</tr>
</tbody>
</table>

**Business**

AEP uses the Events API of Zendesk to store and access user event data
generated in one or more systems or applications used by different
organization. For example, Zendesk can track user events that occur in a
company's business-to-consumer (B2C) application as well as in a
third-party app that a company uses for customer billing.

Zendesk can then use the event data to build solutions that create
better relationships with your customers. The possibilities include:

-   Giving your company more context about the customer in one-on-one
    conversations

-   Following up with the customer after certain events

-   Providing a more personalized user experience in your application or
    system

The Events API lets you build a timeline of all your customers'
interactions from any source. An event can be any programmatic event
that your application or system can associate with a user. Examples
include purchase transactions, website visits, or customer service
interactions. Each event is associated with a customer who triggered the
event.

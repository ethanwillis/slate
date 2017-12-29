---
title: protocols.io API v3

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='https://protocols.io/developers'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction
Welcome protocols.io API v3 documentation!

# Authentication
protocols.io API v3 uses OAuth 2.0 authentication standarts.

Access is separated by 2 types: **private** and **public**

* **public** - you should use access_token of original client. This token allows you to get acccess to all public data (such as protocols, groups).
* **private** - you should use access_token of concrete user. To get this token you should use OAuth 2.0 authentication. This token allows you to get acccess to user private data (such as user profile details, user protocols etc).

<aside class="notice">
We support 2 scopes under OAuth: <code>read</code> and <code>readwrite</code>. With <code>public</code> token you will be able to use inly <code>read</code> scope, but with <code>private</code> token you will be able to give access to user data;
</aside>

Almost all API's requires Authentication header with Bearer access token.You can find your **public** token [here](https://protocols.io/developers) and can get **private** token by using OAuth authentication process. Header should looks like:

`Authentication: Bearer b2e9570895ae57efdc495e1ac27feb12e856aec9f354bb12aa0ceaa3b761f11a`

#### Authorize protocols.io user

> Example of **authorize** link

```
https://protocols.io/api/v3/oauth/authorize?client_id=[your_client_id]&redirect_url=[your_redirect_url]&response_type=code&scope=readwrite&state=[your_state]
```

1. Open [http://protocols.io/developers](https://protocols.io/developers) and get your `client_id` and `client_secret`;
2. Provide your redirect url under `private access` block;
3. Put **authorize** link inside your apication (or use our [sign-in](#sign-in-button) button):
4. Your requests will be redirected to `[your_redirect_url]?code=[new_code]&scope=[your_scope]` with new code and your scope right after your user sign in with protocols.io account;
5. Use received code to get user access_token by using [get token](#get-access-token) API with `grant_type: authorization_code`.
6. Right after you received user access_token you will be able to use it to get/modify protocols.io user private data.

<aside class="notice">
Access token lifetime is 1 year. Don't forget to strore refresh_token and renew access_token before it become expired.
</aside>

#### Refresh access token
> You will start receiving next warning for each API 1 month before access token is expired.

```json
"HTTP/1.1 200 Ok"
[
  {
    "status_code": 0,
    ...
    "warning_code": 1,
    "warning_message": "Your access token will expire in 24 days"
  }
]
```

> When access_token is expired you will recive next error

```json
"HTTP/1.1 400 Bad Request"
[
  {
    "status_code": 1219,
    "error_message": "token is expired"
  }
]
```


1. Take refresh_token which you received after authentication process;
2. Use [get token](link_to_get_token) API with `grant_type: refresh_token`;
3. Take and replace access_token and refresh_token in your apication.

<aside class="warning">
Right after you refresh access token, old token and refresh token will stop working. 
</aside>



# OAuth

## Get client

> Example Request

```curl

curl https://protocols.io/api/v3/oauth/clients/<client_id>
   -H "Authorization: Bearer [ACCESS_TOKEN]"
```

> the above command returns JSON structured like this:

```json
[
  {
    "status_code": 0,
    "client": {
      "client_id": "pr_live_id_lhk123jlasd",
      "client_secret": "pr_live_sc_d12gasdf12",
      "grant_type": "authorization_code",
      "scope": "readwrite",
      "redirect_url": "http://protocols.io/api/v3/oauth/test",
      "token": "8f0f5044f18ebdd0da480b423673ac35"
    }
  }
]
```

This method retrieves client information

### HTTP Request

`GET https://protocols.io/api/v3/oauth/clients/<id>`

## Get access code

You can recive access code bt using next link:

`https://protocols.io/api/v3/oauth/authorize?client_id=[your_client_id]&redirect_url=[tour_redirect_url]&response_type=code&scope=readwrite&state=[your_state]`

User will be redirected to protocols.io sign in form. Right after authentication user will be redirected to your `redirect_url` with new access code and your state. You can use this access code to obtain access_token which you can use to get access to user private data.

## Get access token

> Example Request | token by code

```curl
curl https://protocols.io/api/v3/oauth/token
   -d client_id=<cleitn_id>
   -d client_secret=<client_secret>
   -d grant_type=authorization_code
   -d code=<code>
```

> Example Request | token by refresh token

```curl
curl https://protocols.io/api/v3/oauth/token
   -d client_id=<cleitn_id>
   -d client_secret=<client_secret>
   -d grant_type=refresh_token
   -d refresh_token=<refresh_token>
```

> the above commands returns JSON structured like this:

```json
[
  {
    "status_code": 0,
    "client": {
      "client_id": "pr_live_id_lhk123jlasd",
      "client_secret": "pr_live_sc_d12gasdf12",
      "grant_type": "authorization_code",
      "scope": "readwrite",
      "redirect_url": "http://protocols.io/api/v3/oauth/test",
      "token": "8f0f5044f18ebdd0da480b423673ac35"
    }
  }
]
```


This method retrieves new access token

### HTTP Request

`POST https://protocols.io/api/v3/oauth/token`


### API Parameters

<params>
  <item>
    <parameter>
      client_id
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      The identifier of the client.
    </desc>
  </item>
  <item>
    <parameter>
      client_secret
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      Secret key of the client.
    </desc>
  </item>
  <item>
    <parameter>
      grant_type
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      should be `authorization_code` or `refresh_token`.
    </desc>
  </item>
  <item>
    <parameter>
      code
      <gray>optional, required for `authorization_code` grant_type</gray>
      <type>string</type>
    </parameter>
    <desc>
      code which you recive when client complite authentication on protocols.io.
    </desc>
  </item>
  <item>
    <parameter>
      refresh_token
      <gray>optional, required for `refresh_token` grant_type</gray>
      <type>string</type>
    </parameter>
    <desc>
      refresh token which you recive together with access_token.
    </desc>
  </item>
</params>

# Protocols

Some text about protocols

## Protocol item object

> Example Object

```json
[
  {
    "id": 6645,
    "title": "Quick Ligation Protocol (M2200)",
    "uri": "quick-ligation-protocol-m2200-iqvcdw6",
    "created_on": 1499033111,
    "public": 1,
    "first_name": "Vladimir",
    "last_name": "Frolov",
    "full_name": "New England Biolabs",
    "username": "vladimir-frolov",
    "user_affiliation": "MAI",
    "has_versions": 1,
    "version_id": 1,
    "doi": "dx.doi.org/10.17504/protocols.io.iqvcdw6",
    "link": "https://www.neb.com/protocols/1/01/01/quick-ligation-protocol",
    "published_on": 1502240985,
    "number_of_steps": 4,
    "protocol_img": "https://s3.amazonaws.com/pr-journal/caybvew.png",
    "authors_list": [
      {
        "name": "Matt Sullivan Lab",
        "affiliation": "Matt Sullivan Lab",
        "username": null
      }
    ],
    
  }
]
```

### The Protocol object

<params>
  <item>
    <parameter>
      id
      <gray>int</gray>
    </parameter>
    <desc>
      unique protocol integer identifier.
    </desc>
  </item>
  <item>
    <parameter>
      title
      <gray>string</gray>
    </parameter>
    <desc>
      protocol title.
    </desc>
  </item>
  <item>
    <parameter>
      uri
      <gray>string</gray>
    </parameter>
    <desc>
      unique protocol text identifier.
    </desc>
  </item>
  <item>
    <parameter>
      created_on
      <gray>string</gray>
    </parameter>
    <desc>
      unix timestamp. date/time of protocol creation.
    </desc>
  </item>
  <item>
    <parameter>
      public
      <gray>int</gray>
    </parameter>
    <desc>
      `1` or `0`. `1` means that this protocol is public and `0` otherwise.
    </desc>
  </item>
  <item>
    <parameter>
      first_name
      <gray>string</gray>
    </parameter>
    <desc>
      first name of user, who created this protocol.
    </desc>
  </item>
  <item>
    <parameter>
      last_name
      <gray>string</gray>
    </parameter>
    <desc>
      last name of user, who created this protocol.
    </desc>
  </item>
  <item>
    <parameter>
      full_name
      <gray>string</gray>
    </parameter>
    <desc>
      full_name of user, who created this protocol.
    </desc>
  </item>
  <item>
    <parameter>
      username
      <gray>string</gray>
    </parameter>
    <desc>
      username of user, who created this protocol.
    </desc>
  </item> 
  <item>
    <parameter>
      user_affiliation
      <gray>string, can be empty</gray>
    </parameter>
    <desc>
      affiliation of user, who created this protocol.
    </desc>
  </item>
  <item>
    <parameter>
      has_versions
      <gray>int</gray>
    </parameter>
    <desc>
      `1` or `0`. `1` means that this protocol has version and `0` otherwise.
    </desc>
  </item>
  <item>
    <parameter>
      version_id
      <gray>int</gray>
    </parameter>
    <desc>
      `1...n`. Version number of this protocol.
    </desc>
  </item>
  <item>
    <parameter>
      doi
      <gray>string, can be empty</gray>
    </parameter>
    <desc>
      DOI of this protocol.
    </desc>
  </item>
  <item>
    <parameter>
      link
      <gray>string, can be empty</gray>
    </parameter>
    <desc>
      outer link to some other resource related to this protocol.
    </desc>
  </item>
  <item>
    <parameter>
      published_on
      <gray>int, can be `null`</gray>
    </parameter>
    <desc>
      unix timestamp. date/time when this protocol was published.
    </desc>
  </item>
  <item>
    <parameter>
      number_of_steps
      <gray>int, can be `null`</gray>
    </parameter>
    <desc>
      number of steps, which this protocol contains.
    </desc>
  </item>
  <item>
    <parameter>
      protocol_img
      <gray>string</gray>
    </parameter>
    <desc>
      link to protocol image.
    </desc>
  </item>
  <item>
    <parameter>
      authors_list
      <gray>array, can be empty</gray>
    </parameter>
    <desc>
      array of protocol authors. Contains `author` objects.
    </desc>
  </item>
</params>

> Example Object

```json
[
  {
    "name": "Matt Sullivan Lab",
    "affiliation": "Matt Sullivan Lab",
    "username": null
  }
]
```

<params>
  <childItem>
    <childLabel>
      author object:
    </childLabel>
    <childList>
      <item>
        <parameter>
          name
          <gray>string</gray>
        </parameter>
        <desc>
          full name of author.
        </desc>
      </item>
      <item>
        <parameter>
          affiliation
          <gray>string</gray>
        </parameter>
        <desc>
          affiliation of author.
        </desc>
      </item>
      <item>
        <parameter>
          username
          <gray>string, can be `null`</gray>
        </parameter>
        <desc>
          username of author.
        </desc>
      </item>
    </childList>
  </childItem>
</params>


## Short protocol item object

> Example Object

```json
[
  {
    "id": 6645,
    "title": "Quick Ligation Protocol (M2200)",
    "protocol_img": "https://www.protocols.io/img/default_protocol.png",
    "doi": "dx.doi.org/10.17504/protocols.io.iqvcdw6",
    "uri": "quick-ligation-protocol-m2200-iqvcdw6",
    "published_on": 1502240985,
    "created_on": 1499033111
  }
]
```

<params>
  <item>
    <parameter>
      id
      <gray>int</gray>
    </parameter>
    <desc>
      unique protocol integer identifier.
    </desc>
  </item>
  <item>
    <parameter>
      title
      <gray>int</gray>
    </parameter>
    <desc>
      protocol title.
    </desc>
  </item>
  <item>
    <parameter>
      uri
      <gray>string</gray>
    </parameter>
    <desc>
      unique protocol text identifier.
    </desc>
  </item>
  <item>
    <parameter>
      created_on
      <gray>string</gray>
    </parameter>
    <desc>
      unix timestamp. date/time of protocol creation.
    </desc>
  </item>
  <item>
    <parameter>
      doi
      <gray>string, can be empty</gray>
    </parameter>
    <desc>
      DOI of this protocol.
    </desc>
  </item>
  <item>
    <parameter>
      published_on
      <gray>int, can be `null`</gray>
    </parameter>
    <desc>
      unix timestamp. date/time when this protocol was published.
    </desc>
  </item>
  <item>
    <parameter>
      protocol_img
      <gray>string</gray>
    </parameter>
    <desc>
      link to protocol image.
    </desc>
  </item>
</params>

## Get List

> Example Request | all public protocols

```curl
curl https://protocols.io/api/v3/protocols?filter="public"
   -H "Authorization: Bearer <CLIENT_ACCESS_TOKEN>"
```

> Example Request | user public protocols

```curl
curl https://protocols.io/api/v3/protocols?filter="user_public"
   -H "Authorization: Bearer <USER_ACCESS_TOKEN>"
```

> Example Response

```json
[
  {
    "items": [
      {
        "id": 6645,
        "title": "Quick Ligation Protocol (M2200)",
        "uri": "quick-ligation-protocol-m2200-iqvcdw6",
        "created_on": 1499033111,
        "public": "1",
        "first_name": "Vladimir",
        "last_name": "Frolov",
        "full_name": "New England Biolabs",
        "username": "vladimir-frolov",
        "user_affiliation": "MAI",
        "has_versions": 1,
        "version_id": 1,
        "doi": "dx.doi.org/10.17504/protocols.io.iqvcdw6",
        "link": "https://www.neb.com/protocols/1/01/01/quick-ligation-protocol",
        "published_on": 1502240985,
        "number_of_steps": 4,
        "protocol_img": "https://s3.amazonaws.com/pr-journal/caybvew.png",
        "authors_list": [
          {
            "name": "Matt Sullivan Lab",
            "affiliation": "Matt Sullivan Lab",
            "username": null
          }
        ],
        
      }
      ...
    ],
    "total": 112,
    "total_pages": 12,
    "status_code": 0
  }
]
```

This method retrieves list of protocols separated by pages.

### HTTP Request

`GET https://protocols.io/api/v3/protocols`

### Header Parameters

<params>
  <item>
    <parameter>
      Authorization 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      Bearer user **access_token**.
    </desc>
  </item>
</params>

### API Parameters

<params>
  <item>
    <parameter>
      filter
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      protocols filter, should one of:<br/>
      1. `public` - list of all public protocols;<br/>
      2. `user_public` - list of public protocols which was publiches by concrete user.
    </desc>
  </item>
  <item>
    <parameter>
      key
      <gray>optional, default is **empty**</gray>
      <type>string</type>
    </parameter>
    <desc>
      Search key. String may contatn any chars, numbers and special symbols. System will seach around protocol name, description, authors.
    </desc>
  </item>
  <item>
    <parameter>
      order_field
      <gray>optional, default is **activity**</gray>
      <type>string</type>
    </parameter>
    <desc>
      one of next fields:<br/>
      `activity` - index of protocol popularity;<br/>
      `date` - date of publication;<br/>
      `name` - protocol name;<br/>
      `id` - id of protocol.<br/>
    </desc>
  </item>
  <item>
    <parameter>
      order_dir
      <gray>optional, default is **desc**</gray>
      <type>string</type>
    </parameter>
    <desc>
      order direction, should be `asc` or `desc`.
    </desc>
  </item>
  <item>
    <parameter>
      fields
      <gray>optional, default is **eveything**</gray>
      <type>string</type>
    </parameter>
    <desc>
      list of fields to return. You can put any fields from `item`. Fields should be comma-separated.
    </desc>
  </item>
  <item>
    <parameter>
      page_size
      <gray>optional, default is **10**</gray>
      <type>string</type>
    </parameter>
    <desc>
      number of items per one page. `1...n`.
    </desc>
  </item>
  <item>
    <parameter>
      page_id
      <gray>optional, default is **1**</gray>
      <type>string</type>
    </parameter>
    <desc>
      id of page. `1...n`.
    </desc>
  </item>
</params>

### Response

<params>
  <item>
    <parameter>
      items 
      <gray>array, can be empty</grat>
    </parameter>
    <desc>
      List of [`protocol`](#protocol-item-object) objects.
    </desc>
  </item>
  <item>
    <parameter>
      total 
      <gray>int</grat>
    </parameter>
    <desc>
      Total number of items
    </desc>
  </item>
  <item>
    <parameter>
      total_pages
      <gray>int</grat>
    </parameter>
    <desc>
      Total number of pages
    </desc>
  </item>
  <item>
    <parameter>
      status_code
      <gray>int</grat>
    </parameter>
    <desc>
      Satus code of request, `0` means OK
    </desc>
  </item>
</params>

### Status Codes `HTTP/1.1 400`

<params>
  <item>
    <parameter>
      1
    </parameter>
    <desc>
      Missing or empty parametrs
    </desc>
  </item>
  <item>
    <parameter>
      1302
    </parameter>
    <desc>
      Wrong order field
    </desc>
  </item>
</params>

# Widgets

Protocol wigets allows you to integrate some interactive protocols.io data representation into your appication.
You can use our `js plugin` or API's to create your own widget. 

By using API's you will get access to data and methods to manipulate with it, with `js plugin` you only need to configurate OAuth authentication and render our widget somewhere, we will care about UI. Also you can use `js plugin` and API's in parallel.

## Widget object

> Example Object

```json
[
  {
    "id": "C52C117AECE84DE1891FFD436F3E0F35",
    "created_on": 1514384304,
    "last_modified": 1514384304,
    "type_id": 1,
    "type": "list",
    "client_id": "pr_live_id_e272a3c012d759981af5b3d967a37539",
    "protocols": [
      {
        "id": 8503,
        "title": "Gene calling with Prodigal",
        "protocol_img": "https://s3.amazonaws.com/pr-journal/pshc2w6.jpg",
        "doi": "dx.doi.org/10.17504/protocols.io.kixcufn",
        "uri": "gene-calling-with-prodigal-kixcufn",
        "published_on": 1509493090
      },
      {
        "id": 8504,
        "title": "sdjkf",
        "protocol_img": "https://www.protocols.io/img/default_protocol.png",
        "doi": "dx.doi.org/10.17504/protocols.io.kiycufw",
        "uri": "sdjkf-kiycufw",
        "published_on": 1509493050
      }
    ]
  }
]
```

<params>
  <item>
    <parameter>
      id
      <gray>string</gray>
    </parameter>
    <desc>
      unique widget text identifier.
    </desc>
  </item>
  <item>
    <parameter>
      created_on
      <gray>int</gray>
    </parameter>
    <desc>
      unix timestamp. date/time of widget creation.
    </desc>
  </item>
  <item>
    <parameter>
      last_modified
      <gray>int</gray>
    </parameter>
    <desc>
      unix timestamp. date/time when widget was modified last time.
    </desc>
  </item>
  <item>
    <parameter>
      client_id
      <gray>string</gray>
    </parameter>
    <desc>
      id of dev client.
    </desc>
  </item>
  <item>
    <parameter>
      protocols
      <gray>array, can be null</gray>
    </parameter>
    <desc>
      list of [`shor protocol objects`](#short-protocol-item-object) 
    </desc>
  </item>
</params>


## JavaScript plugins

JavaScript plugin allows you to integrate protocols.io widgets into your appications. Currently we offer next widgets:

1. List of published protocols. [doc](#javascript-list-widget)

<aside class="notice">
To use any of widgets firstly you need to create protocols.io developers account [here](https::/protocols.io/developers).
</aside>

JavaScript bundle is located on our cdn. To start using it just include it on your website header.

> Widget script

```html
<script type="text/javascript" src="http://je-protocols/js/widgets/js/_protocolsio.min.js"></script>
```

Plugin will be accessible by using `_protocolsio`(for widgets) and `_protocolsio_connect`(for sign in) global variable.

## JavaScript authentication plugin

> sign in button inizialization

```js
  _protocolsio_connect.init({
    "client_id" : "your client id",
    "redirect_url" : "your redirect url",
    "scope": "readwrite",
    "response_type" : "code",
    "state" : "your state",
    "selector" : "id of html tag"
  }); 
```

this method renders `sign in with protocols.io` button. 

### JS Method

`_protocolsio_connect.init(config)`


### Config Parameters

<params>
  <item>
    <parameter>
      client_id 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      your client id.
    </desc>
  </item>
  <item>
    <parameter>
      redirect_url 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      access code will be sent to this url.
    </desc>
  </item>
  <item>
    <parameter>
      scope 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      should be `readwrite`.
    </desc>
  </item>
  <item>
    <parameter>
      response_type 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      should be `code`.
    </desc>
  </item>
  <item>
    <parameter>
      state 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      any string which will be sent to redirect url together with access code.
    </desc>
  </item>
  <item>
    <parameter>
      selector 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      id attribute if html tag where widget will be rendered.
    </desc>
  </item>
</params>

## JavaScript List widget

List widget allows to create list of user published protocols. Widget has two modes: `edit mode` - allows users to see and selecet their public protocols. `view mode` - allows evreyone to see selected protocols.

<aside class="notice">
To use widget in <code>edit mode</code> <code>access token</code> of concrete user is required. You need to authorize your user via OAuth and save/associate received access with your user and then use it in widget config.
</aside>

### JavaScript widget inizialization

> widget inizialization

```js
  let MyWidget = _protocolsio.init({
    "id": "id of widget",
    "type": "list",
    "access_token": "client of user access token",
    "selector": "id of html tag where widget will be rendered",
    "doi": "DOI of your publication",
    "mode": "view or edit",
    "on_create": (widget) => {console.log(widget)},
    "on_save": (widget) => {console.log(widget)},
    "on_sign_out": () => {},
  });
```

This methiod initialize new wiget.

### JS Method

`_protocolsio.init(config)`

### Config Parameters

<params>
  <item>
    <parameter>
      access_token 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      user `access token` for `edit mode` and client or user `access token` for `view mode`.
    </desc>
  </item>
  <item>
    <parameter>
      type 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      type of widget. Only `list` is supported.
    </desc>
  </item>
  <item>
    <parameter>
      selector 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      id attribute if html tag where widget will be rendered.
    </desc>
  </item>
  <item>
    <parameter>
      id 
      <gray>optional, default is **null**</gray>
    </parameter>
    <desc>
      if widget id is **null** new widget will be created. If not **null** plugin will try to use exist wdiget.
    </desc>
  </item>
  <item>
    <parameter>
      doi 
      <gray>optional, default is **null**</gray>
    </parameter>
    <desc>
      DOI of your publication.
    </desc>
  </item>
  <item>
    <parameter>
      mode 
      <gray>optional, default is **view**</gray>
    </parameter>
    <desc>
      View mode of the widget. `view` or `edit`.
    </desc>
  </item>
  <item>
    <parameter>
      on_create(widget)
      <gray>optional, default is **null**</gray>
    </parameter>
    <desc>
      callback function which will be called when new widget was created. Function can receive widget object as first parameter. 
    </desc>
  </item> 
  <item>
    <parameter>
      on_change(widget)
      <gray>optional, default is **null**</gray>
    </parameter>
    <desc>
      callback function which will be called when widget was changed. Function can receive widget object as first parameter.
    </desc>
  </item> 
  <item>
    <parameter>
      on_sign_out
      <gray>optional, default is **null**</gray>
    </parameter>
    <desc>
      callback function which will be called when user click `sign out` button.
    </desc>
  </item>
</params>

### JavaScript widget get data

> get widget data

```js
  let MyWidget = _protocolsio.init(config);
  let data = MyWidget.get();
```

This method return simple [wdiget object](#widget-object)

### JS Method

`widget.get()`

## Get widget

> Example Request | protocols list widget

```curl
curl https://protocols.io/api/v3/widgets/[id]
  -H "Authorization: Bearer [ACCESS_TOKEN]"
```

> Example Response

```json
[
  {
    "widget": {
      "id": "C52C117AECE84DE1891FFD436F3E0F35",
      "created_on": 1514384304,
      "last_modified": 1514384304,
      "type_id": 1,
      "type": "list",
      "client_id": "pr_live_id_e272a3c012d759981af5b3d967a37539",
      "protocols": [
        {
          "id": 8503,
          "title": "Gene calling with Prodigal",
          "protocol_img": "https://s3.amazonaws.com/pr-journal/pshc2w6.jpg",
          "doi": "dx.doi.org/10.17504/protocols.io.kixcufn",
          "uri": "gene-calling-with-prodigal-kixcufn",
          "published_on": 1509493090
        },
        {
          "id": 8504,
          "title": "sdjkf",
          "protocol_img": "https://www.protocols.io/img/default_protocol.png",
          "doi": "dx.doi.org/10.17504/protocols.io.kiycufw",
          "uri": "sdjkf-kiycufw",
          "published_on": 1509493050
        }
      ]
    },
    "status_code": 0
  }
]
```

### HTTP Request

`GET https://protocols.io/api/v3/widgets/[id]`

### Header Parameters

<params>
  <item>
    <parameter>
      Authorization 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      `public` or `private` Bearer **access_token**.
    </desc>
  </item>
</params>

### API Parameters

<params>
  <item>
    <parameter>
      id
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      Unique text id of widget.
    </desc>
  </item>
</params>

### Response

<params>
  <item>
    <parameter>
      widget 
      <gray>object</grat>
    </parameter>
    <desc>
      [`widget`](#widget-object) object
    </desc>
  </item>
  <item>
    <parameter>
      status_code
      <gray>int</grat>
    </parameter>
    <desc>
      Satus code of request, `0` means OK
    </desc>
  </item>
</params>


### Status Codes `HTTP/1.1 400`

<params>
  <item>
    <parameter>
      1402
    </parameter>
    <desc>
      Widget with this id doesn't exists
    </desc>
  </item>
</params>

## Create widget

> Example Request | protocols list widget

```curl
curl https://protocols.io/api/v3/widgets
  -H "Authorization: Bearer [ACCESS_TOKEN]"
  -d type="list"
  -d doi="dx.doi.org/10.17504/protocols.io.kiycufw"
  -d protocols[0]=[id_1]
  -d protocols[1]=[id_2]
```

> Example Response

```json
[
  {
    "widget": {
      "id": "C52C117AECE84DE1891FFD436F3E0F35",
      "created_on": 1514384304,
      "last_modified": 1514384304,
      "type_id": 1,
      "type": "list",
      "client_id": "pr_live_id_e272a3c012d759981af5b3d967a37539",
      "protocols": [
        {
          "id": 8503,
          "title": "Gene calling with Prodigal",
          "protocol_img": "https://s3.amazonaws.com/pr-journal/pshc2w6.jpg",
          "doi": "dx.doi.org/10.17504/protocols.io.kixcufn",
          "uri": "gene-calling-with-prodigal-kixcufn",
          "published_on": 1509493090
        },
        {
          "id": 8504,
          "title": "sdjkf",
          "protocol_img": "https://www.protocols.io/img/default_protocol.png",
          "doi": "dx.doi.org/10.17504/protocols.io.kiycufw",
          "uri": "sdjkf-kiycufw",
          "published_on": 1509493050
        }
      ]
    },
    "status_code": 0
  }
]
```

### HTTP Request

`POST https://protocols.io/api/v3/widgets`

### Header Parameters

<params>
  <item>
    <parameter>
      Authorization 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      `private` Bearer **access_token**.
    </desc>
  </item>
</params>

### API Parameters

<params>
  <item>
    <parameter>
      type
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      type of widget, only `list` is supported.
    </desc>
  </item>
  <item>
    <parameter>
      doi
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      Unique DOI of publication where widget will be implemented.
    </desc>
  </item>
  <item>
    <parameter>
      protocols
      <gray>optional, default is **null**</gray>
      <type>array</type>
    </parameter>
    <desc>
      array of protocol ids which should be associated with widget.
    </desc>
  </item>
  <item>
    <parameter>
      id
      <gray>optional, default is **null**</gray>
      <type>string</type>
    </parameter>
    <desc>
      unique widget text id. If empty guid will be genereated.
    </desc>
  </item> 
</params>

### Response

<params>
  <item>
    <parameter>
      widget 
      <gray>object</grat>
    </parameter>
    <desc>
      [`widget`](#widget-object) object
    </desc>
  </item>
  <item>
    <parameter>
      status_code
      <gray>int</grat>
    </parameter>
    <desc>
      Satus code of request, `0` means OK
    </desc>
  </item>
</params>


### Status Codes `HTTP/1.1 400`

<params>
  <item>
    <parameter>
      1
    </parameter>
    <desc>
      missing or empty parametrs.
    </desc>
  </item>
  <item>
    <parameter>
      1401
    </parameter>
    <desc>
      widget with this id already exists.
    </desc>
  </item>
  <item>
    <parameter>
      1403
    </parameter>
    <desc>
      widget type is not exists.
    </desc>
  </item>
</params>

## Update widget

> Example Request | protocols list widget

```curl
curl https://protocols.io/api/v3/widgets/[id]
  -H "Authorization: Bearer [ACCESS_TOKEN]"
  -d protocols[0]=[id_1]
  -d protocols[1]=[id_2]
```

> Example Response

```json
[
  {
    "widget": {
      "id": "C52C117AECE84DE1891FFD436F3E0F35",
      "created_on": 1514384304,
      "last_modified": 1514384304,
      "type_id": 1,
      "type": "list",
      "client_id": "pr_live_id_e272a3c012d759981af5b3d967a37539",
      "protocols": [
        {
          "id": 8503,
          "title": "Gene calling with Prodigal",
          "protocol_img": "https://s3.amazonaws.com/pr-journal/pshc2w6.jpg",
          "doi": "dx.doi.org/10.17504/protocols.io.kixcufn",
          "uri": "gene-calling-with-prodigal-kixcufn",
          "published_on": 1509493090
        },
        {
          "id": 8504,
          "title": "sdjkf",
          "protocol_img": "https://www.protocols.io/img/default_protocol.png",
          "doi": "dx.doi.org/10.17504/protocols.io.kiycufw",
          "uri": "sdjkf-kiycufw",
          "published_on": 1509493050
        }
      ]
    },
    "status_code": 0
  }
]
```

### HTTP Request

`PUT https://protocols.io/api/v3/widgets/[id]`

### Header Parameters

<params>
  <item>
    <parameter>
      Authorization 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      `private` Bearer **access_token**.
    </desc>
  </item>
</params>

### API Parameters

<params>
  <item>
    <parameter>
      id
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      unique widget text id.
    </desc>
  </item>
  <item>
    <parameter>
      protocols
      <yellow>Required</yellow>
      <type>array</type>
    </parameter>
    <desc>
      array of protocol ids which should be associated with widget. Old list will be removed.
    </desc>
  </item>
</params>

### Response

<params>
  <item>
    <parameter>
      widget 
      <gray>object</grat>
    </parameter>
    <desc>
      [`widget`](#widget-object) object
    </desc>
  </item>
  <item>
    <parameter>
      status_code
      <gray>int</grat>
    </parameter>
    <desc>
      Satus code of request, `0` means OK
    </desc>
  </item>
</params>


### Status Codes `HTTP/1.1 400`

<params>
  <item>
    <parameter>
      1
    </parameter>
    <desc>
      missing or empty parametrs.
    </desc>
  </item>
  <item>
    <parameter>
      1402
    </parameter>
    <desc>
      widget with this id doesn't exists
    </desc>
  </item>
</params>


## Delete widget

> Example Request | protocols list widget

```curl
curl https://protocols.io/api/v3/widgets/[id]
  -H "Authorization: Bearer [ACCESS_TOKEN]"
```

> Example Response

```json
[
  {
    "status_code": 0
  }
]
```

### HTTP Request

`DELETE https://protocols.io/api/v3/widgets/[id]`

### Header Parameters

<params>
  <item>
    <parameter>
      Authorization 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      `private` Bearer **access_token**.
    </desc>
  </item>
</params>

### API Parameters

<params>
  <item>
    <parameter>
      id
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      unique widget text id.
    </desc>
  </item>
</params>

### Response

<params>
  <item>
    <parameter>
      status_code
      <gray>int</grat>
    </parameter>
    <desc>
      Satus code of request, `0` means OK
    </desc>
  </item>
</params>


### Status Codes `HTTP/1.1 400`

<params>
  <item>
    <parameter>
      1402
    </parameter>
    <desc>
      widget with this id doesn't exists
    </desc>
  </item>
</params>
# Authentication
protocols.io API v3 uses OAuth 2.0 authentication standarts.

There are two types of access: **public** and **private**

* **public** - you can get your public token on [`https://www.protocols.io/developers`](https://www.protocols.io/developers). The public token allows you to read all public data.
* **private** - to get private token you need to use OAuth 2.0 authentication. The private token allows you to get acccess to a specific user's public protocols.

<!-- <aside class="notice">
We support 2 scopes under OAuth: <code>read</code> and <code>readwrite</code>. With <code>public</code> token you will be able to use inly <code>read</code> scope, but with <code>private</code> token you will be able to give access to user data;
</aside> -->

Most of the endpoints require Authentication header with Bearer access token. Example:

`Authentication: Bearer b2e9570895ae57efdc495e1ac27feb12e856aec9f354bb12aa0ceaa3b761f11a`

#### Authorize protocols.io user

> Example of **authorize** link

```
https://www.protocols.io/api/v3/oauth/authorize?client_id=[your_client_id]&redirect_url=[your_redirect_url]&response_type=code&scope=readwrite&state=[your_state]
```

1. Open [`http://www.protocols.io/developers`](https://www.protocols.io/developers) and copy your `client_id` and `client_secret`.
2. Provide your redirect url under `private access` block.
3. Put **authorize** link inside your apication or use our [sign-in](#sign-in-button) button.
4. Your requests will be redirected to `[your_redirect_url]?code=[new_code]&scope=[your_scope]`.
5. Use the code to get user access_token by calling [`https://www.protocols.io/api/v3/oauth/token`](#get-access-token) with `grant_type: authorization_code`.

<aside class="notice">
Access token will reset in 1 year. Don't forget to strore refresh_token and renew access_token before it expires.
</aside>

#### Refresh access token
> You will receive a warning 1 month before access_token expires.

```json
"HTTP/1.1 200 Ok"
{
  "status_code": 0,
  ...
  "warning_code": 1,
  "warning_message": "Your access token expires in 24 days"
}
```

> Once access_token expires you will get an error:

```json
"HTTP/1.1 400 Bad Request"
{
  "status_code": 1219,
  "error_message": "token is expired"
}
```

Call [`https://www.protocols.io/api/v3/oauth/token`](#get-access-token) `grant_type: refresh_token` to obtain a new access_token.

<aside class="warning">
Once you refresh the access_token, the old tokens will stop working. 
</aside>


# OAuth

## Get client

> Example Request

```curl

curl https://www.protocols.io/api/v3/oauth/clients/<client_id>
   -H "Authorization: Bearer [ACCESS_TOKEN]"
```

> returns the following JSON:

```json
{
  "status_code": 0,
  "client": {
    "client_id": "pr_live_id_lhk123jlasd",
    "client_secret": "pr_live_sc_d12gasdf12",
    "grant_type": "authorization_code",
    "scope": "readwrite",
    "redirect_url": "http://www.protocols.io/api/v3/oauth/test",
    "token": "8f0f5044f18ebdd0da480b423673ac35"
  }
}
```

This method retrieves client information

### HTTP Request

`GET https://www.protocols.io/api/v3/oauth/clients/<id>`

## Get access code

You can recive access code by calling:

`https://www.protocols.io/api/v3/oauth/authorize?client_id=[your_client_id]&redirect_url=[tour_redirect_url]&response_type=code&scope=readwrite&state=[your_state]`

The users will be presented with protocols.io sign in form. Once authenticated, the users will be redirected to your `redirect_url` with the new access code. Use the access code to obtain access_token.

## Get access token

> Example Request | obtain token by code

```curl
curl https://www.protocols.io/api/v3/oauth/token
   -d client_id=<cleitn_id>
   -d client_secret=<client_secret>
   -d grant_type=authorization_code
   -d code=<code>
```

> Example Request | obtain token by refresh token

```curl
curl https://www.protocols.io/api/v3/oauth/token
   -d client_id=<cleitn_id>
   -d client_secret=<client_secret>
   -d grant_type=refresh_token
   -d refresh_token=<refresh_token>
```

> returns the following JSON:

```json
{
  "access_token": "b3656ef91016d67bfc4bb9f983d4450f2baa99b0fca7f2665d456cc14e5d1441",
  "token_type": "bearer",
  "expires_in": "30681976",
  "scope": "readwrite",
  "refresh_token": "5acce557aebbd287cf371371ead660e44ebc889cb711c67c3b25b9af2beb0184",
  "refresh_expires_in": "62217976",
  "user": {
    "name": "Vladimir Frolov",
    "affiliation": null,
    "username": "vladimir-frolov10",
    "link": null,
    "image": {
      "source": "https://s3.amazonaws.com/pr-journal/djqbjf6.jpg",
      "placeholder": "https://s3.amazonaws.com/pr-journal/djqbjf6.jpg"
    }
  },
  "status_code": 0
}
```


This method retrieves access_token

### HTTP Request

`POST https://www.protocols.io/api/v3/oauth/token`


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

### Response

<params>
  <item>
    <parameter>
      access_token 
      <gray>string</grat>
    </parameter>
    <desc>
      new access code.
    </desc>
  </item>
  <item>
    <parameter>
      token_type 
      <gray>string</grat>
    </parameter>
    <desc>
      type of token.
    </desc>
  </item>
  <item>
    <parameter>
      expires_in 
      <gray>int</grat>
    </parameter>
    <desc>
      time on seconds until token become expired.
    </desc>
  </item>
  <item>
    <parameter>
      scope 
      <gray>string</grat>
    </parameter>
    <desc>
      granted scope type.
    </desc>
  </item> 
  <item>
    <parameter>
      refresh_token 
      <gray>string</grat>
    </parameter>
    <desc>
      new refresh token.
    </desc>
  </item>
  <item>
    <parameter>
      refresh_expires_in 
      <gray>int</grat>
    </parameter>
    <desc>
      time on seconds until refresh token become expired.
    </desc>
  </item>
  <item>
    <parameter>
      user 
      <gray>[`user`](#user-object)</grat>
    </parameter>
    <desc>
      user data.
    </desc>
  </item>
</params>
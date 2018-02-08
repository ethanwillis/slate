## JavaScript plugin

Use the JavaScript plugin to integrate Publisher Widget.

<aside class="notice">
To use the Publisher Widget please create a protocols.io developer account.
</aside>
More here: [`https://www.protocols.io/developers`](https://www.protocols.io/developers)

> JavaScript plugin bundle is located on protocols.io CDN:

```html
<script type="text/javascript" src="https://www.protocols.io/js/widgets/js/protocolsiojs.min.js"></script>
```

JavaScript plugin is accessible by using `_protocolsio`(for widgets) and `_protocolsio_connect`(for sign in) global variables.

## Authentication

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

Use this JavaScript method to render `Sign in with protocols.io` button. 

<aside class="notice">
Once users sign in with protocols.io account, the `access code` will be sent to your redirect url. Get the access_token by calling [`https://www.protocols.io/api/v3/oauth/token`](#get-access-token). After authorization the page will be redirected to your redirect_url.
</aside>

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
      any string which will be sent to redirect_url together with the access code.
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

## Inizialization

The Publisher Widget provides access to user's published protocols. It has two modes: `edit mode` - to selecet public protocols. `view mode` - to view selected protocols.

<aside class="notice">
To use Publisher Widget in <code>edit mode</code> the user's **private** <code>access_token</code> is required.
</aside>

### Publisher Widget inizialization using JavaScript

```js
  let MyWidget = _protocolsio.init({
    "id": "id of widget",
    "type": "list",
    "access_token": "client of user access token",
    "selector": "id of html tag where widget will be rendered",
    "doi": "DOI of your article",
    "mode": "view or edit",
    "on_create": (widget) => {console.log(widget)},
    "on_save": (widget) => {console.log(widget)},
    "on_sign_out": () => {},
  });
```

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
      user's **private** `access_token` for `edit mode` and **private** or **public** `access_token` for `view mode`.
    </desc>
  </item>
  <item>
    <parameter>
      type 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      type of widget. The only supported type at the moment is `list`.
    </desc>
  </item>
  <item>
    <parameter>
      selector 
      <yellow>Required</yellow>
    </parameter>
    <desc>
      id attribute of the html tag where widget will be rendered.
    </desc>
  </item>
  <item>
    <parameter>
      id 
      <gray>optional, default is **null**</gray>
    </parameter>
    <desc>
      if widget id is **null** a new widget is created otherwise plugin will try to use existent widget.
    </desc>
  </item>
  <item>
    <parameter>
      doi 
      <gray>Required</gray>
    </parameter>
    <desc>
      DOI of your article.
    </desc>
  </item>
  <item>
    <parameter>
      mode 
      <gray>optional, default is **view**</gray>
    </parameter>
    <desc>
     Widget mode. `view` or `edit`.
    </desc>
  </item>
  <item>
    <parameter>
      on_create(widget)
      <gray>optional, default is **null**</gray>
    </parameter>
    <desc>
      callback function is called when a new widget is created. The function returns a widget object as first parameter. 
    </desc>
  </item> 
  <item>
    <parameter>
      on_change(widget)
      <gray>optional, default is **null**</gray>
    </parameter>
    <desc>
      callback function is called when a new widget is changed. The function returns a widget object as first parameter.
    </desc>
  </item> 
  <item>
    <parameter>
      on_sign_out
      <gray>optional, default is **null**</gray>
    </parameter>
    <desc>
      callback function is called when the user clicks `sign out` button.
    </desc>
  </item>
</params>


> get widget data

```js
  let MyWidget = _protocolsio.init(config);
  let data = MyWidget.get();
```

returns [wdiget](#widget-object)

### JS Method

`widget.get()`

## Using without sign in
<aside class="notice">
You can request a <code>list of protocols</code> associated with a <code>DOI</code> of the provided article without signing in.
</aside>

### JS Method to initialize

`_protocolsio.init(config);`

```js
    let widget = _protocolsio.init({
        doi           : 'DOI of your article',
        type          : 'list',
        mode          : 'view',
        selector      : 'id of html element where to push widget',
        access_token  : 'client of user access token'
      });
```

> get widget data

```js
  let MyWidget = _protocolsio.init(config);
  let data = MyWidget.get();
```

returns [wdiget](#widget-object)

### JS Method

`widget.get()`

### Config Prameters

<params>
  <item>
    <parameter>
      selector
      <yellow>Required</yellow>
    </parameter>
     <desc>
       id attribute of html tag where widget will be rendered.
     </desc>
  </item>
  <item>
    <parameter>
      access_token
      <yellow>Required</yellow>
    </parameter>
     <desc>
       **public** `access_token` for viewing protocols.
     </desc>
  </item>
  <item>
    <parameter>
      doi
      <yellow>Required</yellow>
    </parameter>
     <desc>
       Digital Object Ideftifier (DOI) of your article
     </desc>
  </item>
  <item>
    <parameter>
      mode
      <yellow>Required</yellow>
    </parameter>
     <desc>
       This parameter must be set to 'view' if only DOI is provided
     </desc>
  </item>
</params>
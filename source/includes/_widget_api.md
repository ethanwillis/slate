## Get widget data

> Example request | published protocols widget

```curl
curl https://www.protocols.io/api/v3/widgets/[id]
  -H "Authorization: Bearer [ACCESS_TOKEN]"
```

> Example response

```json
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
        "image": {
          "source": "https://www.protocols.io/img/default_protocol.png",
          "placeholder": "https://www.protocols.io/img/default_protocol.png"
        },
        "doi": "dx.doi.org/10.17504/protocols.io.kixcufn",
        "uri": "gene-calling-with-prodigal-kixcufn",
        "published_on": 1509493090
      },
      {
        "id": 8504,
        "title": "sdjkf",
        "image": {
          "source": "https://www.protocols.io/img/default_protocol.png",
          "placeholder": "https://www.protocols.io/img/default_protocol.png"
        },
        "doi": "dx.doi.org/10.17504/protocols.io.kiycufw",
        "uri": "sdjkf-kiycufw",
        "published_on": 1509493050
      }
    ]
  },
  "status_code": 0
}
```

### HTTP Request

`GET https://www.protocols.io/api/v3/widgets/[id]`

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
      <gray>[`widget`](#widget-object)</grat>
    </parameter>
    <desc>
      requested widget
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

### Get widgets by DOI

`GET https://www.protocols.io/api/v3/widgets?doi=[DOI]`

> Example request | published protocols widget

```curl
curl https://www.protocols.io/api/v3/widgets?doi=[DOI]
  -H "Authorization: Bearer [ACCESS_TOKEN]"
```

> Example response

```json
{
  "widgets": [
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
          "image": {
            "source": "https://www.protocols.io/img/default_protocol.png",
            "placeholder": "https://www.protocols.io/img/default_protocol.png"
          },
          "doi": "dx.doi.org/10.17504/protocols.io.kixcufn",
          "uri": "gene-calling-with-prodigal-kixcufn",
          "published_on": 1509493090
        },
        {
          "id": 8504,
          "title": "sdjkf",
          "image": {
            "source": "https://www.protocols.io/img/default_protocol.png",
            "placeholder": "https://www.protocols.io/img/default_protocol.png"
          },
          "doi": "dx.doi.org/10.17504/protocols.io.kiycufw",
          "uri": "sdjkf-kiycufw",
          "published_on": 1509493050
        }
      ]
    }
  ],
  "status_code": 0
}
```

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
      doi
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      DOI of your article
    </desc>
  </item>
</params>

### Response

<params>
  <item>
    <parameter>
      widgets 
      <gray>array</grat>
    </parameter>
    <desc>
      list of [`widget`](#widget-object)
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
      1404
    </parameter>
    <desc>
     Widget GET parameter (doi) is not specified
    </desc>
  </item>
</params>

### Get widgets protocols list by DOI

`GET https://www.protocols.io/api/v3/widgets/protocols?doi=[DOI]`

> Example request | published protocols widget

```curl
curl https://www.protocols.io/api/v3/widgets/protocols?doi=[DOI]
  -H "Authorization: Bearer [ACCESS_TOKEN]"
```

> Example Response

```json
{
    "protocols": [
        {
            "id": 7058,
            "title": "test",
            "image": {
              "source": "https://www.protocols.io/img/default_protocol.png",
              "placeholder": "https://www.protocols.io/img/default_protocol.png"
            },
            "doi": "dx.doi.org/10.17504/protocols.io.i5scg6e",
            "uri": "test-i5scg6e",
            "publish_date": 1514311257,
            "widgets": [
                {
                    "id": 1,
                    "created_on": 1516634164,
                    "last_modified": 1516886065,
                    "type_id": 1,
                    "type": "list",
                    "client_id": "pr_live_id_645dc746785d48490676872340059577"
                },
                {
                    "id": 2,
                    "created_on": 1516634164,
                    "last_modified": 1516876208,
                    "type_id": 1,
                    "type": "list",
                    "client_id": "pr_live_id_645dc746785d48490676872340059576"
                }
            ]
        }
    ],
    "status_code": 0
}
```

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
      doi
      <yellow>Required</yellow>
      <type>string</type>
    </parameter>
    <desc>
      DOI of your article
    </desc>
  </item>
</params>

### Response

<params>
  <item>
    <parameter>
      protocols 
      <gray>array</grat>
    </parameter>
    <desc>
      list of [`small protocol`](#small-protocol-object) with extra field `widgets` - list of related [`widget`](#widget-object)
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
      1404
    </parameter>
    <desc>
     Widget GET parameter (doi) is not specified
    </desc>
  </item>
</params>

## Create widget

> Example Request | published protocols widget

```curl
curl https://www.protocols.io/api/v3/widgets
  -H "Authorization: Bearer [ACCESS_TOKEN]"
  -d type="list"
  -d doi="dx.doi.org/10.17504/protocols.io.kiycufw"
  -d protocols[0]=[id_1]
  -d protocols[1]=[id_2]
```

> Example Response

```json
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
        "image": {
          "source": "https://www.protocols.io/img/default_protocol.png",
          "placeholder": "https://www.protocols.io/img/default_protocol.png"
        },
        "doi": "dx.doi.org/10.17504/protocols.io.kixcufn",
        "uri": "gene-calling-with-prodigal-kixcufn",
        "published_on": 1509493090
      },
      {
        "id": 8504,
        "title": "sdjkf",
        "image": {
          "source": "https://www.protocols.io/img/default_protocol.png",
          "placeholder": "https://www.protocols.io/img/default_protocol.png"
        },
        "doi": "dx.doi.org/10.17504/protocols.io.kiycufw",
        "uri": "sdjkf-kiycufw",
        "published_on": 1509493050
      }
    ]
  },
  "status_code": 0
}
```

### HTTP Request

`POST https://www.protocols.io/api/v3/widgets`

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
      <gray>Required</gray>
      <type>string</type>
    </parameter>
    <desc>
      DOI of the article where the widget is implemented.
    </desc>
  </item>
  <item>
    <parameter>
      protocols
      <gray>optional, default is **null**</gray>
      <type>array</type>
    </parameter>
    <desc>
      array of ids of published protocols.
    </desc>
  </item>
  <item>
    <parameter>
      id
      <gray>optional, default is **null**</gray>
      <type>string</type>
    </parameter>
    <desc>
      widget guid. If **null**, a new guid will be genereated.
    </desc>
  </item> 
</params>

### Response

<params>
  <item>
    <parameter>
      widget 
      <gray>[`widget`](#widget-object)</grat>
    </parameter>
    <desc>
      created widget
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
      widget type does not exist.
    </desc>
  </item>
</params>

## Update widget

> Example Request | published protocols widget

```curl
curl https://www.protocols.io/api/v3/widgets/[id]
  -H "Authorization: Bearer [ACCESS_TOKEN]"
  -d protocols[0]=[id_1]
  -d protocols[1]=[id_2]
```

> Example Response

```json
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
        "image": {
          "source": "https://www.protocols.io/img/default_protocol.png",
          "placeholder": "https://www.protocols.io/img/default_protocol.png"
        },
        "doi": "dx.doi.org/10.17504/protocols.io.kixcufn",
        "uri": "gene-calling-with-prodigal-kixcufn",
        "published_on": 1509493090
      },
      {
        "id": 8504,
        "title": "sdjkf",
        "image": {
          "source": "https://www.protocols.io/img/default_protocol.png",
          "placeholder": "https://www.protocols.io/img/default_protocol.png"
        },
        "doi": "dx.doi.org/10.17504/protocols.io.kiycufw",
        "uri": "sdjkf-kiycufw",
        "published_on": 1509493050
      }
    ]
  },
  "status_code": 0
}
```

### HTTP Request

`PUT https://www.protocols.io/api/v3/widgets/[id]`

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
      array of ids of published protocols (will replace existing list)
    </desc>
  </item>
  <item>
    <parameter>
      doi
      <gray>Required</gray>
      <type>string</type>
    </parameter>
    <desc>
      DOI of the article where the widget is implemented.
    </desc>
  </item>
</params>

### Response

<params>
  <item>
    <parameter>
      widget 
      <gray>[`widget`](#widget-object)</grat>
    </parameter>
    <desc>
      changed widget 
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

> Example Request | published protocols widget

```curl
curl https://www.protocols.io/api/v3/widgets/[id]
  -H "Authorization: Bearer [ACCESS_TOKEN]"
```

> Example Response

```json
{
  "status_code": 0
}
```

### HTTP Request

`DELETE https://www.protocols.io/api/v3/widgets/[id]`

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

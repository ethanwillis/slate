## Get List

> Example Request | all public protocols

```curl
curl https://www.protocols.io/api/v3/protocols?filter="public"
   -H "Authorization: Bearer <PUBLIC_ACCESS_TOKEN>"
```

> Example Request | user public protocols

```curl
curl https://www.protocols.io/api/v3/protocols?filter="user_public"
   -H "Authorization: Bearer <PRIVATE_ACCESS_TOKEN>"
```

> Example Response

```json
{
  "id": 872,
  "title": "Lysis Buffer (20 mL)",
  "image": {
    "source": "https://www.protocols.io/img/default_protocol.png",
    "placeholder": "https://www.protocols.io/img/default_protocol.png"
  },
  "doi": "dx.doi.org/10.17504/protocols.io.c4gytv",
  "uri": "lysis-buffer-20-ml-c4gytv",
  "published_on": 1487372466,
  "created_on": 1434670606,
  "creator": {
    "name": "Celina Gomez",
    "affiliation": null,
    "username": "celina-gomez",
    "link": "",
    "image": {
      "source": null,
      "placeholder": null
    }
  },
  "public": 1,
  "versions": [
    {
      "id": 10091,
      "title": "untitled protocol",
      "image": {
        "source": "https://www.protocols.io/img/default_protocol.png",
        "placeholder": "https://www.protocols.io/img/default_protocol.png"
      },
      "doi": null,
      "uri": "untitled-protocol-m4jc8un",
      "published_on": 0,
      "version_id": 1,
      "created_on": 1518089537,
      "categories": null,
      "creator": {
        "name": "Vladimir Frolov",
        "affiliation": "protocols.io",
        "username": "vladimir-frolov10",
        "link": null,
        "image": {
          "source": "https://s3.amazonaws.com/pr-journal/djqbjf6.jpg",
          "placeholder": "https://s3.amazonaws.com/pr-journal/djqbjf6.jpg"
        }
      }
    }
  ],
  "version_id": 0,
  "link": "",
  "number_of_steps": 3,
  "authors": [
    {
      "name": "Matt Sullivan Lab",
      "affiliation": "Matt Sullivan Lab",
      "username": null,
      "link": null,
      "image": {
        "source": null,
        "placeholder": null
      }
    }
  ],
  "steps": [...],
  "materials": [...]
}
```

This method retrieves the list of protocols separated by pages.

### HTTP Request

`GET https://www.protocols.io/api/v3/protocols`

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
      List of [`protocol`](#protocol-object) objects.
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

## Get Protocol

> Example Request

```curl
curl https://www.protocols.io/api/v3/protocols/[id]"
   -H "Authorization: Bearer <ACCESS_TOKEN>"
```

> Example Response

```json
{
  "id": 872,
  "title": "Lysis Buffer (20 mL)",
  "image": {
    "source": "https://www.protocols.io/img/default_protocol.png",
    "placeholder": "https://www.protocols.io/img/default_protocol.png"
  },
  "doi": "dx.doi.org/10.17504/protocols.io.c4gytv",
  "uri": "lysis-buffer-20-ml-c4gytv",
  "published_on": 1487372466,
  "created_on": 1434670606,
  "creator": {
    "name": "Celina Gomez",
    "affiliation": null,
    "username": "celina-gomez",
    "link": "",
    "image": {
      "source": null,
      "placeholder": null
    }
  },
  "public": 1,
  "versions": [
    {
      "id": 10091,
      "title": "untitled protocol",
      "image": {
        "source": "https://www.protocols.io/img/default_protocol.png",
        "placeholder": "https://www.protocols.io/img/default_protocol.png"
      },
      "version_id": 1,
      "doi": null,
      "uri": "untitled-protocol-m4jc8un",
      "published_on": 0
    }
  ],
  "version_id": 0,
  "link": "",
  "number_of_steps": 3,
  "authors": [
    {
      "name": "Matt Sullivan Lab",
      "affiliation": "Matt Sullivan Lab",
      "username": null,
      "link": null,
      "image": {
        "source": null,
        "placeholder": null
      }
    }
  ],
  "steps": [...],
  "materials": [...]
}
```

This method retrieves protocol.

### HTTP Request

`GET https://www.protocols.io/api/v3/protocols/[id]`

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

### Response

<params>
  <item>
    <parameter>
      protocol 
      <gray>[`protocol`](#protocol-object)</grat>
    </parameter>
    <desc>
      protocol object with steps and materials.
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

## Get Steps

> Example Request

```curl
curl https://www.protocols.io/api/v3/protocols/[id]/steps"
   -H "Authorization: Bearer <ACCESS_TOKEN>"
```

> Example Response

```json
{
  "steps": [
    {
      "id": 595209,
      "guid": "E70FDFE632504ADFB0ED519ABB5449B1",
      "previous_id": 0,
      "previous_guid": null,
      "modified_on": 1517933242,
      "components": [...]
    },
    {
      "id": 595210,
      "guid": "1167CDCBFDB64CD4BA50A5016F4474B6",
      "previous_id": 595209,
      "previous_guid": "E70FDFE632504ADFB0ED519ABB5449B1",
      "modified_on": 1517933232,
      "components": [...]
    }
  ],
  "status_code": 0
}
```

This method retrieves protocol steps list.

### HTTP Request

`GET https://www.protocols.io/api/v3/protocols/[id]/steps`

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

### Response

<params>
  <item>
    <parameter>
      steps 
      <gray>array, can be empty</grat>
    </parameter>
    <desc>
      List of [`steps`](#step-object).
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

## Get Materials

> Example Request

```curl
curl https://www.protocols.io/api/v3/protocols/[id]/materials"
   -H "Authorization: Bearer <ACCESS_TOKEN>"
```

> Example Response

```json
{
  "materials": [
    {
      "id": 1144,
      "mol_weight": 0,
      "name": "Quick Ligation Kit - 30 rxns",
      "linfor": "",
      "url": "https://www.neb.com/M2200",
      "sku": "M2200S",
      "vendor": {
        "name": "New England Biolabs",
        "affiliation": null,
        "username": null,
        "link": "https://www.neb.com/",
        "image": {
          "source": "http://je-protocols/img/vendors/2.png",
          "placeholder": "http://je-protocols/img/vendors/2.png"
        }
      }
    },
    {
      "id": 46948,
      "mol_weight": 0,
      "name": "(+) Abscisic acid (Dormin, ABA)",
      "linfor": "",
      "url": "https://www.biobasic.com/us/abscisic-acid-dormin-aba-3945",
      "sku": "AB0001.SIZE.100mg",
      "vendor": {
        "name": "Bio Basic Inc.",
        "affiliation": null,
        "username": null,
        "link": "http://biobasic.com/",
        "image": {
          "source": "http://je-protocols/img/vendors/120.png",
          "placeholder": "http://je-protocols/img/vendors/120.png"
        }
      }
    }
  ],
  "status_code": 0
}
```

This method retrieves protocol materials list.

### HTTP Request

`GET https://www.protocols.io/api/v3/protocols/[id]/materials`

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

### Response

<params>
  <item>
    <parameter>
      materials 
      <gray>array, can be empty</grat>
    </parameter>
    <desc>
      List of [`materials`](#reagent-object).
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
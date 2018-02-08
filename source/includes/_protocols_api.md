## Get List

> Example Request | all public protocols

```curl
curl https://www.protocols.io/api/v3/protocols?filter="public"
   -H "Authorization: Bearer <CLIENT_ACCESS_TOKEN>"
```

> Example Request | user public protocols

```curl
curl https://www.protocols.io/api/v3/protocols?filter="user_public"
   -H "Authorization: Bearer <USER_ACCESS_TOKEN>"
```

> Example Response

```json
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
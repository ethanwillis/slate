# Publisher Widget

Publisher Wiget allows you to access protocols.io user's public and unlisted protocols directly from your publishing system. Use the Publisher Widget to add DOIs of the detailed methods directly into article's Materials and Methods section.

## Widget object

> Example object

```json
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
      list of [`small protocol`](#small-protocol-object) 
    </desc>
  </item>
</params>

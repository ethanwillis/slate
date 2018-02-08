# Protocols

## Small Protocol object

> Example Object

```json
{
  "id": 8503,
  "title": "Gene calling with Prodigal",
  "image": {
    "source": "https://www.protocols.io/img/default_protocol.png",
    "placeholder": "https://www.protocols.io/img/default_protocol.png"
  },
  "version_id": 0,
  "doi": "dx.doi.org/10.17504/protocols.io.kixcufn",
  "uri": "gene-calling-with-prodigal-kixcufn",
  "published_on": 1509493090
}
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
      image
      <gray>[`image`](#image-object)</gray>
    </parameter>
    <desc>
      protocol image.
    </desc>
  </item>
  <item>
    <parameter>
      version_id
      <gray>int</gray>
    </parameter>
    <desc>
      `0...n`. Version number of this protocol.
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
      uri
      <gray>string</gray>
    </parameter>
    <desc>
      unique protocol text identifier.
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
</params>

## Protocol object

> Example Object

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

### Protocol object

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
      image
      <gray>[`image`](#image-object)</gray>
    </parameter>
    <desc>
      protocol image.
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
      uri
      <gray>string</gray>
    </parameter>
    <desc>
      unique protocol text identifier.
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
      created_on
      <gray>int</gray>
    </parameter>
    <desc>
      unix timestamp. date/time of protocol creation.
    </desc>
  </item>
  <item>
    <parameter>
      creator
      <gray>[`user`](#user-object)</gray>
    </parameter>
    <desc>
      protocol creator
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
      versions
      <gray>array</gray>
    </parameter>
    <desc>
      list of [`versions`](#small-protocol-object)
    </desc>
  </item>
  <item>
    <parameter>
      version_id
      <gray>int</gray>
    </parameter>
    <desc>
      `0...n`. Version number of this protocol.
    </desc>
  </item>
  <item>
    <parameter>
      number_of_steps
      <gray>int, can be `null`</gray>
    </parameter>
    <desc>
      number of stepws of this protocol.
    </desc>
  </item>
  <item>
    <parameter>
      authors
      <gray>array</gray>
    </parameter>
    <desc>
      list of [`user`](#user-object) or empty array
    </desc>
  </item>
</params>

<aside class="notice">
If you request a protocol with steps or materials, the protocol object will contain an array of <a href="#step-object">steps</a> or <a href="#reagent-object">materials</a> accrodingly.
</aside>

## Step object

> Example Object

```json
{
  "id": 595209,
  "guid": "E70FDFE632504ADFB0ED519ABB5449B1",
  "previous_id": 0,
  "previous_guid": null,
  "modified_on": 1517933242,
  "components": [...]
}
```

<params>
  <item>
    <parameter>
      id
      <gray>int</gray>
    </parameter>
    <desc>
      unique step integer identifier.
    </desc>
  </item>
  <item>
    <parameter>
      guid
      <gray>string</gray>
    </parameter>
    <desc>
      unique step guid.
    </desc>
  </item>
  <item>
    <parameter>
      previous_id
      <gray>int</gray>
    </parameter>
    <desc>
      id of previous step.
    </desc>
  </item>
  <item>
    <parameter>
      previous_guid
      <gray>string, can be `null`</gray>
    </parameter>
    <desc>
      guid of previous step.
    </desc>
  </item>
  <item>
    <parameter>
      modified_on
      <gray>int</gray>
    </parameter>
    <desc>
      unix timestamp. date/time when step was modified.
    </desc>
  </item>
  <item>
    <parameter>
      components
      <gray>array</gray>
    </parameter>
    <desc>
      list of [`step components`](#step-component-object).
    </desc>
  </item>
</params>

## Step Component object

> Example Object

```json
{
  "id": 1023444,
  "guid": "A38362CBC954458FB069F821B6526B38",
  "previous_id": 1023443,
  "previous_guid": "1EBCBC24EFCF429F8F34D7099EF6211E",
  "type_id": 3,
  "title": "Amount",
  "source": {...}
}
```

<params>
  <item>
    <parameter>
      id
      <gray>int</gray>
    </parameter>
    <desc>
      unique step integer identifier.
    </desc>
  </item>
  <item>
    <parameter>
      guid
      <gray>string</gray>
    </parameter>
    <desc>
      unique step guid.
    </desc>
  </item>
  <item>
    <parameter>
      order_id
      <gray>int</gray>
    </parameter>
    <desc>
      sequence number of component in the list starting from `0`.
    </desc>
  </item>
  <item>
    <parameter>
      type_id
      <gray>int</gray>
    </parameter>
    <desc>
      type of of component, one of [`step component types`](##step-component-types)
    </desc>
  </item>
  <item>
    <parameter>
      title
      <gray>string</gray>
    </parameter>
    <desc>
      name of component
    </desc>
  </item>
  <item>
    <parameter>
      source
      <gray>[`step component`](##step-component-types)</gray>
    </parameter>
    <desc>
      variative object of component, can be determine by `type_id`
    </desc>
  </item>
</params>

## Step Component Types

### Description, type id 1

Description of the step, can contain html tags.

> Example Object

```json
{
  "description": "<p>step to make smth</p>"
}
```

<params>
  <item>
    <parameter>
      description
      <gray>string</gray>
    </parameter>
    <desc>
      html
    </desc>
  </item>
</params>

### Amount, type id 3

A quantity of something, typically the total of a reagent, size, value etc.

> Example Object

```json
{
  "amount": 11,
  "unit": "µl",
  "title": "of MGH"
}
```

<params>
  <item>
    <parameter>
      amount
      <gray>int</gray>
    </parameter>
    <desc>
      amount quantity.
    </desc>
  </item>
  <item>
    <parameter>
      unit
      <gray>string</gray>
    </parameter>
    <desc>
      unit.
    </desc>
  </item>
  <item>
    <parameter>
      title
      <gray>string</gray>
    </parameter>
    <desc>
      title of amount.
    </desc>
  </item>
</params>

### Duration, type id 4

> Example Object

```json
{
  "duration": 11,
  "title": "boil"
}
```

<params>
  <item>
    <parameter>
      duration
      <gray>int</gray>
    </parameter>
    <desc>
      duration in milliseconds.
    </desc>
  </item>
  <item>
    <parameter>
      title
      <gray>string</gray>
    </parameter>
    <desc>
      title of amount.
    </desc>
  </item>
</params>

### Title, type id 6

> Example Object

```json
{
  "title": "boil"
}
```

<params>
  <item>
    <parameter>
      title
      <gray>string</gray>
    </parameter>
    <desc>
      title of step.
    </desc>
  </item>
</params>

### Link, type id 7

> Example Object

```json
{
  "link": "boil"
}
```

<params>
  <item>
    <parameter>
      link
      <gray>string</gray>
    </parameter>
    <desc>
      external url.
    </desc>
  </item>
</params>

### Software package, type id 8

> Example Object

```json
{
  "name": "what",
  "developer": "me",
  "repository": "https://google.com",
  "link": "https://google.com",
  "os_name": "win",
  "os_version": "10"
}
```

<params>
  <item>
    <parameter>
      name
      <gray>string</gray>
    </parameter>
    <desc>
      name of software.
    </desc>
  </item>
  <item>
    <parameter>
      developer
      <gray>string</gray>
    </parameter>
    <desc>
      developer of software.
    </desc>
  </item>
  <item>
    <parameter>
      repository
      <gray>string</gray>
    </parameter>
    <desc>
      url or name of repository.
    </desc>
  </item>
  <item>
    <parameter>
      link
      <gray>string</gray>
    </parameter>
    <desc>
      external url.
    </desc>
  </item>
  <item>
    <parameter>
      os_name
      <gray>string</gray>
    </parameter>
    <desc>
      name of operation system.
    </desc>
  </item>
  <item>
    <parameter>
      os_version
      <gray>string</gray>
    </parameter>
    <desc>
      version of operation system.
    </desc>
  </item>
</params>

### Dataset package, type id 9

> Example Object

```json
{
  "name": "DataTable",
  "link": "https://protocols.io"
}
```

<params>
  <item>
    <parameter>
      name
      <gray>string</gray>
    </parameter>
    <desc>
      name of software.
    </desc>
  </item>
  <item>
    <parameter>
      link
      <gray>string</gray>
    </parameter>
    <desc>
      external url.
    </desc>
  </item>
</params>

### Comment, type id 13

Step comments.

> Example Object

```json
{
  "id": 16620,
  "parent_id": 0,
  "uri": "comment-on-step-1-of-untitled-protocol1",
  "title": "Comment on step 1 of untitled protocol",
  "body": "<p>Make if cool!</p>",
  "created_on": 1517933093,
  "changed_on": 0,
  "creator": {
    "name": "Lenny Teytelman",
    "affiliation": "protocols.io",
    "username": "lenny-teytelman",
    "link": null,
    "image": {
      "source": "/img/avatars/005.png",
      "placeholder": "/img/avatars/005.png"
    }
  },
  "comments": [...]
}
```

<params>
  <item>
    <parameter>
      source object
      <gray>[`comment`](#comment-object)</gray>
    </parameter>
    <desc>
      source object represents usual comment object.
    </desc>
  </item>
</params>

### Command package, type id 15

> Example Object

```json
{
  "name": "Code",
  "command": "echo 'hello world!'",
  "os_name": "windows",
  "os_version": "10"
}
```

<params>
  <item>
    <parameter>
      name
      <gray>string</gray>
    </parameter>
    <desc>
      name of software.
    </desc>
  </item>
  <item>
    <parameter>
      command
      <gray>string</gray>
    </parameter>
    <desc>
      executable command.
    </desc>
  </item>
  <item>
    <parameter>
      os_name
      <gray>string</gray>
    </parameter>
    <desc>
      name of operation system.
    </desc>
  </item>
  <item>
    <parameter>
      os_version
      <gray>string</gray>
    </parameter>
    <desc>
      version of operation system.
    </desc>
  </item>
</params>

### Expected result, type id 17

> Example Object

```json
{
  "body": "<p>should be something</p>"
}
```

<params>
  <item>
    <parameter>
      body
      <gray>string</gray>
    </parameter>
    <desc>
      body can contain html tags.
    </desc>
  </item>
</params>

### Protocol, type id 18

Step can contatin protocols as components.

<params>
  <item>
    <parameter>
      source object
      <gray>[`protocol`](#protocol-object)</gray>
    </parameter>
    <desc>
      source object represents usual protocol object.
    </desc>
  </item>
</params>

### Safety information, type id 19

> Example Object

```json
{
  "body": "<p>dont' do something</p>",
  "link": "https://protocols.io"
}
```

<params>
  <item>
    <parameter>
      body
      <gray>string</gray>
    </parameter>
    <desc>
      body can contain html tags.
    </desc>
  </item>
  <item>
    <parameter>
      link
      <gray>string</gray>
    </parameter>
    <desc>
      external url.
    </desc>
  </item>
</params>

### Reagent, type id 20

> Example Object

```json
{
  "id": 19751,
  "mol_weight": 0,
  "name": "2 mg Gastrin I, human",
  "linfor": "C130H204N38O31S",
  "url": "https://www.biorbyt.com/gastrin-i-human-orb321073",
  "sku": "orb321073",
  "vendor": {
    "name": "biorbyt",
    "affiliation": null,
    "username": null,
    "link": "https://www.biorbyt.com/",
    "image": {
      "source": "http://je-protocols/img/vendors/208.png",
      "placeholder": "http://je-protocols/img/vendors/208.png"
    }
  }
}
```

<params>
  <item>
    <parameter>
      source object
      <gray>[`reagent`](#reagent-object)</gray>
    </parameter>
    <desc>
      source object represents usual reagent object.
    </desc>
  </item>
</params>

### Step cases, type id 21

> Example Object

```json
{
  "cases": [
    {
      "title": "Measurment A",
      "label": "Case 1",
      "step_id": 595210,
      "step_guid": "1167CDCBFDB64CD4BA50A5016F4474B6"
    },
    {
      "title": "MEasurment B",
      "label": "Case 2",
      "step_id": 595211,
      "step_guid": "DE9EA0FAF6E149528A4DAEFCA2DCC927"
    }
  ]
}
```

<params>
  <item>
    <parameter>
      cases
      <gray>array</gray>
    </parameter>
    <desc>
      list of case objects.
    </desc>
  </item>
  <childItem>
    <childLabel>
      case object:
    </childLabel>
    <childList>
      <item>
        <parameter>
          title
          <gray>string</gray>
        </parameter>
        <desc>
          title of a case.
        </desc>
      </item>
      <item>
        <parameter>
          label
          <gray>string</gray>
        </parameter>
        <desc>
          label of a case.
        </desc>
      </item>
      <item>
        <parameter>
          step_id
          <gray>ing</gray>
        </parameter>
        <desc>
          linked step id.
        </desc>
      </item>
      <item>
        <parameter>
          step_guid
          <gray>string</gray>
        </parameter>
        <desc>
          linked step guid.
        </desc>
      </item>
    </childList>
  </childItem>
</params>

### Go to previous step, type id 22

> Example Object

```json
{
  "title": "Reason for repeating the step",
  "step_guid": E70FDFE632504ADFB0ED519ABB5449B1
}
```

<params>
  <item>
    <parameter>
      title
      <gray>string</gray>
    </parameter>
    <desc>
      some text, usually explaining the reason to go to previous step.
    </desc>
  </item>
  <item>
    <parameter>
      step_guid
      <gray>string</gray>
    </parameter>
    <desc>
      linked step guid.
    </desc>
  </item>
</params>

### Temperature, type id 24

> Example Object

```json
{
  "temperature": 12,
  "unit": "°C",
  "title": "boil"
}
```

<params>
  <item>
    <parameter>
      temperature
      <gray>int</gray>
    </parameter>
    <desc>
      temperature value.
    </desc>
  </item>
  <item>
    <parameter>
      unit
      <gray>string</gray>
    </parameter>
    <desc>
      unit.
    </desc>
  </item>
  <item>
    <parameter>
      title
      <gray>string, can be empty</gray>
    </parameter>
    <desc>
      title of component.
    </desc>
  </item>
</params>

### Concentration, type id 25

> Example Object

```json
{
  "concentration": 12,
  "unit": "°C",
  "title": "boil"
}
```

<params>
  <item>
    <parameter>
      concentration
      <gray>int</gray>
    </parameter>
    <desc>
      concentration value.
    </desc>
  </item>
  <item>
    <parameter>
      unit
      <gray>string</gray>
    </parameter>
    <desc>
      unit.
    </desc>
  </item>
  <item>
    <parameter>
      title
      <gray>string</gray>
    </parameter>
    <desc>
      title of concentration.
    </desc>
  </item>
</params>

### Note, type id 26

Author notes.

> Example Object

```json
{
  "id": 16620,
  "parent_id": 0,
  "uri": "comment-on-step-1-of-untitled-protocol1",
  "title": "Comment on step 1 of untitled protocol",
  "body": "<p>Make if cool!</p>",
  "created_on": 1517933093,
  "changed_on": 0,
  "creator": {
    "name": "Lenny Teytelman",
    "affiliation": "protocols.io",
    "username": "lenny-teytelman",
    "link": null,
    "image": {
      "source": "/img/avatars/005.png",
      "placeholder": "/img/avatars/005.png"
    }
  },
  "comments": [...]
}
```

<params>
  <item>
    <parameter>
      source object
      <gray>[`comment`](#comment-object)</gray>
    </parameter>
    <desc>
      source object represents usual comment object.
    </desc>
  </item>
</params>
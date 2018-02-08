# Objects

## User object

> Example Object

```json
{
	"user": {
	  "name": "Vladimir Frolov",
	  "affiliation": null,
	  "username": "vladimir-frolov10",
	  "link": null,
	  "image": {
	    "source": "https://s3.amazonaws.com/pr-journal/djqbjf6.jpg",
	    "placeholder": "https://s3.amazonaws.com/pr-journal/djqbjf6.jpg"
	  }
	}
}
```

<params>
  <item>
    <parameter>
      name
      <gray>string</gray>
    </parameter>
    <desc>
    	user full name
    </desc>
  </item>
  <item>
    <parameter>
      affiliation
      <gray>string, can be `null`</gray>
    </parameter>
    <desc>
      user affiliation
    </desc>
  </item>
  <item>
    <parameter>
      username
      <gray>string, can be `null`</gray>
    </parameter>
    <desc>
    	username
    </desc>
  </item>
  <item>
    <parameter>
      link
      <gray>string, can be `null`</gray>
    </parameter>
    <desc>
      unix timestamp. date/time of protocol creation.
    </desc>
  </item>
  <item>
    <parameter>
      image
      <gray>[`image`](#image-object)</gray>
    </parameter>
    <desc>
    	user profile image
    </desc>
  </item>
</params>

## Image object

> Example Object

```json
{
	"image": {
		"source": "https://www.protocols.io/img/default_protocol.png",
		"placeholder": "https://www.protocols.io/img/default_protocol.png"
	}
}
```

<params>
  <item>
    <parameter>
      source
      <gray>string</gray>
    </parameter>
    <desc>
    	link to the image
    </desc>
  </item>
  <item>
    <parameter>
      placeholder
      <gray>string</gray>
    </parameter>
    <desc>
      link to the image placeholder or original image link of placeholder is not exist
    </desc>
  </item>
</params>

## Reagent object

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
      id
      <gray>int</gray>
    </parameter>
    <desc>
      unique reagent integer identifier.
    </desc>
  </item>
  <item>
    <parameter>
      mol_weight
      <gray>float</gray>
    </parameter>
    <desc>
      molarity weigh.
    </desc>
  </item>
  <item>
    <parameter>
      name
      <gray>string</gray>
    </parameter>
    <desc>
      name of reagent.
    </desc>
  </item>
  <item>
    <parameter>
      linfor
      <gray>string</gray>
    </parameter>
    <desc>
      linar formual.
    </desc>
  </item>
  <item>
    <parameter>
      url
      <gray>string, can be `null`</gray>
    </parameter>
    <desc>
      external url.
    </desc>
  </item>
  <item>
    <parameter>
      sku
      <gray>string</gray>
    </parameter>
    <desc>
      reagent sku.
    </desc>
  </item>
  <item>
    <parameter>
      vendor
      <gray>[`user`](#user-object)</gray>
    </parameter>
    <desc>
      reagent sku.
    </desc>
  </item>
</params>
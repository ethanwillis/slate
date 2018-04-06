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
      external url.
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
      reagent vendor.
    </desc>
  </item>
</params>

## Comment object

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
      id
      <gray>int</gray>
    </parameter>
    <desc>
      unique comment integer identifier.
    </desc>
  </item>
  <item>
    <parameter>
      parent_id
      <gray>int</gray>
    </parameter>
    <desc>
      id of parent comment.
    </desc>
  </item>
  <item>
    <parameter>
      title
      <gray>string</gray>
    </parameter>
    <desc>
      title of comment.
    </desc>
  </item>
  <item>
    <parameter>
      body
      <gray>string</gray>
    </parameter>
    <desc>
      body of comment.
    </desc>
  </item>
  <item>
    <parameter>
      created_on
      <gray>int</gray>
    </parameter>
    <desc>
      unix timestamp. date/time of comment creation.
    </desc>
  </item>
  <item>
    <parameter>
      changed_on
      <gray>int</gray>
    </parameter>
    <desc>
      unix timestamp. date/time when comment was modified last time.
    </desc>
  </item>
  <item>
    <parameter>
      creator
      <gray>[`user`](#user-object)</gray>
    </parameter>
    <desc>
      comment creator.
    </desc>
  </item>
  <item>
    <parameter>
      comments
      <gray>[`comment`](#comment-object)</gray>
    </parameter>
    <desc>
      comment replies.
    </desc>
  </item>
</params>
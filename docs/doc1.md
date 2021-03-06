---
id: doc1
title: Style Guide
sidebar_label: Style Guide
---

You can write content using [GitHub-flavored Markdown syntax](https://github.github.com/gfm/).

## Take-Two Commerce API

The Take-Two Commerce API returns pricing information for content for sale on the store.

## Testing out Commerce API Doc

```
openapi: 3.0.0
servers: 
  - url: https://api.t2gp.take2games.com
    description: Production server (uses live data)
  - url: https://api-int.t2gp.take2games.com
    description: Integration Server (uses staged data)
info:
  description: T2GP Commerce API
  version: "1.0.0"
  title: Commerce API
  contact:
    email: ml.leong@take2games.com
tags:
  - name: public
    description: available for public use
  
paths:
  #/skus/items/a,b,c,d,e,f
  /skus/items/{itemid}:
    get:
      tags:
        - public
      summary: Get Sku(s) by Item Id(s)
      operationId: getSkus
      description: |
        Query for available Sku(s) for sale by Item Id. This API supports bulk queries of up to 10 items at a time, using comma to seperate the item ids.
      parameters:
        - in: path
          name: itemid
          description: a list of item Id(s) to search for
          required: true
          schema:
            type: array
            items:
              type: string
            minItems: 1
            maxItems: 10
      responses:
        '200':
          description: 
            Returns an array of SkuPrice(s) matching the item Id(s) requested. Note that if the item requested does not exist, the query would just omit them from the result set, hence the returned values could be a subset of the requested items. Consequently, if all item(s) requested could not be found, the response is an empty array.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/SkuPrice'
    
components:
  schemas:
    SkuPrice:
      type: object
      required:
        - itemId
        - itemTitle
        - releaseDate
        - preorderDate
        - preloadDate
      properties:
        itemId:
          type: string
          format: byte
          example: '5Cb4zz06AmALbklUyfPyD'
        itemTitle:
          type: string
          example: 'Kerbal Space Program (Steam)'
        itemSkuId:
          type: string
          example: '123456'
          description: 'Mdm short item number'
        xsollaProjectId:
          type: string
          example: '654321'
          description: 'Xsolla Project Id'
        currency:
          type: string
          example: 'USD'
          description: 'ISO 4217 Currency Code'
        originalPrice:
          type: number
          format: double
          example: 59.99
        salePrice:
          type: number
          format: double
          example: 39.99
          description: 'If there is no discount, salePrice == originalPrice'
        drm:
          type: string
          enum: 
            - 'Steam' 
            - 'DRM Free'
            - 'Epic'
            - 'Playstation'
            - 'Xbox'
            - 'Nintendo Switch'
            - 'Rockstar Games Launcher'
        promotion:
          $ref: '#/components/schemas/SkuPromotion'
        externalSiteLink:
          type: string
          format: url
          example: 'https://store.playstation.com/en-us/product/UP4581-CUSA15719_00-DISINTEGRATION01'
          description: 'link to first party store for non direct sales'
        releaseDate:
          type: number
          format: int64
          example: 1592280000
          description: 'unix epoch time in seconds. 0 if released, non-zero if its a release date in future'
        preorderDate:
          type: number
          format: int64
          example: 0
          description: 'unix epoch time in seconds. 0 if no pre-order date'
        preloadDate:
          type: number
          format: int64
          example: 0
          description: 'unix epoch time in seconds. 0 if no preload date'
    SkuPromotion:
      required:
        - percent
        - amt
        - reason
        - start
        - end
      properties:
        percent:
          type: number
          format: double
          example: 15.00
          description: 'percentage of discount off'
        amt:
          type: number
          format: double
          example: 20.00
          description: 'discounted amount off'
        reason:
          type: string
          example: 'Kerbal Spring Sale'
          description: 'reason code for promotion, can be used as a key into a localized text'
        start:
          type: number
          format: int64
          example: 1592280000
          description: 'unix epoch time in seconds. When promotion starts. SkuPromotion object will only exists if there is a promotion and the start date is in the past, and the end date is still in the future'
        end:
          type: number
          format: int64
          example: 1602280000
          description: 'unix epoch time in seconds. When promotion ends. If the current time is past end, then the SkuPromotion object will be null'
```

## Markdown Syntax

To serve as an example page when styling markdown based Docusaurus sites.

## Headers

# H1 - Create the best documentation

## H2 - Create the best documentation

### H3 - Create the best documentation

#### H4 - Create the best documentation

##### H5 - Create the best documentation

###### H6 - Create the best documentation

---

## Emphasis

Emphasis, aka italics, with *asterisks* or _underscores_.

Strong emphasis, aka bold, with **asterisks** or __underscores__.

Combined emphasis with **asterisks and _underscores_**.

Strikethrough uses two tildes. ~~Scratch this.~~

---

## Lists

1. First ordered list item
1. Another item
   - Unordered sub-list.
1. Actual numbers don't matter, just that it's a number
   1. Ordered sub-list
1. And another item.

* Unordered list can use asterisks

- Or minuses

+ Or pluses

---

## Links

[I'm an inline-style link](https://www.google.com/)

[I'm an inline-style link with title](https://www.google.com/ "Google's Homepage")

[I'm a reference-style link][arbitrary case-insensitive reference text]

[You can use numbers for reference-style link definitions][1]

Or leave it empty and use the [link text itself].

URLs and URLs in angle brackets will automatically get turned into links. http://www.example.com/ or <http://www.example.com/> and sometimes example.com (but not on GitHub, for example).

Some text to show that the reference links can follow later.

[arbitrary case-insensitive reference text]: https://www.mozilla.org/
[1]: http://slashdot.org/
[link text itself]: http://www.reddit.com/

---

## Images

Here's our logo (hover to see the title text):

Inline-style: ![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png 'Logo Title Text 1')

Reference-style: ![alt text][logo]

[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png 'Logo Title Text 2'

Images from any folder can be used by providing path to file. Path should be relative to markdown file.

![img](../static/img/logo.svg)

---

## Code

```javascript
var s = 'JavaScript syntax highlighting';
alert(s);
```

```python
s = "Python syntax highlighting"
print(s)
```

```
No language indicated, so no syntax highlighting.
But let's throw in a <b>tag</b>.
```

```js {2}
function highlightMe() {
  console.log('This line can be highlighted!');
}
```

---

## Tables

Colons can be used to align columns.

| Tables        |      Are      |   Cool |
| ------------- | :-----------: | -----: |
| col 3 is      | right-aligned | \$1600 |
| col 2 is      |   centered    |   \$12 |
| zebra stripes |   are neat    |    \$1 |

There must be at least 3 dashes separating each header cell. The outer pipes (|) are optional, and you don't need to make the raw Markdown line up prettily. You can also use inline Markdown.

| Markdown | Less      | Pretty     |
| -------- | --------- | ---------- |
| _Still_  | `renders` | **nicely** |
| 1        | 2         | 3          |

---

## Blockquotes

> Blockquotes are very handy in email to emulate reply text. This line is part of the same quote.

Quote break.

> This is a very long line that will still be quoted properly when it wraps. Oh boy let's keep writing to make sure this is long enough to actually wrap for everyone. Oh, you can _put_ **Markdown** into a blockquote.

---

## Inline HTML

<dl>
  <dt>Definition list</dt>
  <dd>Is something people use sometimes.</dd>

  <dt>Markdown in HTML</dt>
  <dd>Does *not* work **very** well. Use HTML <em>tags</em>.</dd>
</dl>

---

## Line Breaks

Here's a line for us to start with.

This line is separated from the one above by two newlines, so it will be a _separate paragraph_.

This line is also a separate paragraph, but... This line is only separated by a single newline, so it's a separate line in the _same paragraph_.

---

## Admonitions

:::note

This is a note

:::

:::tip

This is a tip

:::

:::important

This is important

:::

:::caution

This is a caution

:::

:::warning

This is a warning

:::

---
id: doc1
title: Latin-ish
sidebar_label: API Doc
---

Check the [documentation](https://docusaurus.io) for how to use Docusaurus.

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

## Nulla

Nulla facilisi. Maecenas sodales nec purus eget posuere. Sed sapien quam, pretium a risus in, porttitor dapibus erat. Sed sit amet fringilla ipsum, eget iaculis augue. Integer sollicitudin tortor quis ultricies aliquam. Suspendisse fringilla nunc in tellus cursus, at placerat tellus scelerisque. Sed tempus elit a sollicitudin rhoncus. Nulla facilisi. Morbi nec dolor dolor. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Cras et aliquet lectus. Pellentesque sit amet eros nisi. Quisque ac sapien in sapien congue accumsan. Nullam in posuere ante. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Proin lacinia leo a nibh fringilla pharetra.

## Orci

Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Proin venenatis lectus dui, vel ultrices ante bibendum hendrerit. Aenean egestas feugiat dui id hendrerit. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Curabitur in tellus laoreet, eleifend nunc id, viverra leo. Proin vulputate non dolor vel vulputate. Curabitur pretium lobortis felis, sit amet finibus lorem suscipit ut. Sed non mollis risus. Duis sagittis, mi in euismod tincidunt, nunc mauris vestibulum urna, at euismod est elit quis erat. Phasellus accumsan vitae neque eu placerat. In elementum arcu nec tellus imperdiet, eget maximus nulla sodales. Curabitur eu sapien eget nisl sodales fermentum.

## Phasellus

Phasellus pulvinar ex id commodo imperdiet. Praesent odio nibh, sollicitudin sit amet faucibus id, placerat at metus. Donec vitae eros vitae tortor hendrerit finibus. Interdum et malesuada fames ac ante ipsum primis in faucibus. Quisque vitae purus dolor. Duis suscipit ac nulla et finibus. Phasellus ac sem sed dui dictum gravida. Phasellus eleifend vestibulum facilisis. Integer pharetra nec enim vitae mattis. Duis auctor, lectus quis condimentum bibendum, nunc dolor aliquam massa, id bibendum orci velit quis magna. Ut volutpat nulla nunc, sed interdum magna condimentum non. Sed urna metus, scelerisque vitae consectetur a, feugiat quis magna. Donec dignissim ornare nisl, eget tempor risus malesuada quis.

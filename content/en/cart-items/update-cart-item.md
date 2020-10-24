---
title: Update Item
description: ""
position: 21
category: Cart Items
---

Use the `updateItem` mutation to update any existing items.

## Mutation

`updateItem(input: UpdateCartItemInput!): Cart!`

| Arguments | Type                   |
| --------- | ---------------------- |
| `input`   | `UpdateCartItemInput!` |

The `updateItem` mutation will always return the updated [`Cart`](/graphql-types#cart) object.

## `UpdateCartItemInput!`

You can update items in the cart at any time.

| Argument      | Type           | Description                                  |
| ------------- | -------------- | -------------------------------------------- |
| `cartId`      | `ID!`          | The `id` of the cart you the item belongs to |
| `id`          | `ID!`          | The `id` of the item you are updating        |
| `name`        | `String`       | Set a new item name                          |
| `description` | `String`       | Set a new item description                   |
| `type`        | `CartItemType` | `SKU`, `TAX`, `SHIPPING`                     |
| `images`      | `[String]`     | Update any image URLs                        |
| `price`       | `Int`          | Set a new unit price                         |
| `quantity`    | `Int`          | Set a new quantity                           |

<alert type="info">

If no item exists with the `id` provided, a `BAD_USER_INPUT` error will be returned.

</alert>

## Example

<code-group>
  <code-block label="Mutation" active>

```graphql
mutation {
  updateItem(
    input: {
      cartId: "ck5r8d5b500003f5o2aif0v2b"
      id: "5e3293a3462051"
      quantity: 2
    }
  ) {
    id
    isEmpty
    abandoned
    totalItems
    totalUniqueItems
    subTotal {
      formatted
    }
  }
}
```

  </code-block>
  <code-block label="Response">

```json
{
  "data": {
    "updateItem": {
      "id": "ck5r8d5b500003f5o2aif0v2b",
      "isEmpty": false,
      "abandoned": false,
      "totalItems": 2,
      "totalUniqueItems": 1,
      "subTotal": {
        "formatted": "$40.00"
      }
    }
  }
}
```

  </code-block>
</code-group>

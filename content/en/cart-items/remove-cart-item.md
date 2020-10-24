---
title: Remove Item
description: ""
position: 22
category: Cart Items
---

Use the `removeItem` mutation to remove any items from the cart.

## Mutation

`removeItem(input: RemoveCartItemInput!): Cart!`

| Arguments | Type                   |
| --------- | ---------------------- |
| `input`   | `RemoveCartItemInput!` |

The `removeItem` mutation will always return the updated [`Cart`](/graphql-types#cart) object.

## `RemoveCartItemInput!`

You can remove items from the cart at any time.

| Argument | Type  | Description                                  |
| -------- | ----- | -------------------------------------------- |
| `cartId` | `ID!` | The `id` of the cart you the item belongs to |
| `id`     | `ID!` | The `id` of the item you want to remove      |

<alert type="info">

If no item exists with the `id` provided, a `BAD_USER_INPUT` error will be returned.

</alert>

## Example

<code-group>
  <code-block label="Mutation" active>

```graphql
mutation {
  removeItem(
    input: { cartId: "ck5r8d5b500003f5o2aif0v2b", id: "5e3293a3462051" }
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
    "removeItem": {
      "id": "ck5r8d5b500003f5o2aif0v2b",
      "isEmpty": true,
      "abandoned": false,
      "totalItems": 0,
      "totalUniqueItems": 0,
      "subTotal": {
        "formatted": "$0.00"
      }
    }
  }
}
```

  </code-block>
</code-group>

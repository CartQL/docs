---
title: Decrement Item Quantity
description: ""
position: 24
category: Cart Items
---

Use the `decrementItemQuantity` mutation to increment only the cart item quantity.

## Mutation

`decrementItemQuantity(input: UpdateItemQuantityInput!): Cart!`

| Arguments | Type                       |
| --------- | -------------------------- |
| `input`   | `UpdateItemQuantityInput!` |

The `decrementItemQuantity` mutation will always return the updated [`Cart`](/graphql-types#cart) object.

## `UpdateItemQuantityInput!`

| Argument | Type   | Description                                                 |
| -------- | ------ | ----------------------------------------------------------- |
| `cartId` | `ID!`  | The `id` of the cart you are working with.                  |
| `id`     | `ID!`  | The `id` of the item you are decrementing the quantity of.  |
| `by`     | `Int!` | The amount you wish to decrement the cart item quantity by. |

<alert type="info">

If no cart item exists with the `id` provided, an error will be returned.

</alert>

## Example

<code-group>
  <code-block label="Mutation" active>

```graphql
mutation {
  decrementItemQuantity(
    input: { cartId: "ck5r8d5b500003f5o2aif0v2b", id: "5e3293a3462051", by: 10 }
  ) {
    id
    items {
      id
      quantity
    }
  }
}
```

  </code-block>
  <code-block label="Response">

```json
{
  "data": {
    "decrementItemQuantity": {
      "id": "ck5r8d5b500003f5o2aif0v2b",
      "items": [
        {
          "id": "ck5r8d5b500003f5o2aif0v2b",
          "quantity": 1
        }
      ]
    }
  }
}
```

  </code-block>
</code-group>

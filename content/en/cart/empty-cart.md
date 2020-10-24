---
title: Empty Cart
description: ""
position: 12
category: Cart
---

Use the `emptyCart` mutation to delete a cart, and all items associated to it.

## Mutation

`emptyCart(input: EmptyCartInput!): Cart!`

| Arguments | Type              |
| --------- | ----------------- |
| `input`   | `EmptyCartInput!` |

The `emptyCart` mutation will always return the emptied [`Cart`](/graphql-types#cart).

## `EmptyCartInput!`

| Argument | Type  | Description                             |
| -------- | ----- | --------------------------------------- |
| `id`     | `ID!` | The `id` of the Cart you wish to empty. |

<alert type="info">

If no cart item exists with the `id` provided, an error will be returned.

</alert>

## Example

<code-group>
  <code-block label="Mutation" active>

```graphql
mutation {
  emptyCart(input: { id: "ck5r8d5b500003f5o2aif0v2b" }) {
    id
    totalItems
    totalUniqueItems
  }
}
```

  </code-block>
  <code-block label="Response">

```json
{
  "data": {
    "emptyCart": {
      "id": "ck5r8d5b500003f5o2aif0v2b",
      "totalItems": 0,
      "totalUniqueItems": 0
    }
  }
}
```

  </code-block>
</code-group>

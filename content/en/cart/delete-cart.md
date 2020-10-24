---
title: Delete Cart
description: ""
position: 13
category: Cart
---

Use the `deleteCart` mutation to delete a cart, and all items associated to it.

## Mutation

`deleteCart(input: DeleteCartInput!): DeletePayload!`

| Arguments | Type               |
| --------- | ------------------ |
| `input`   | `DeleteCartInput!` |

The `deleteCart` mutation will always return the [`DeletePayload`](#deletepayload) object.

## `DeleteCartInput!`

| Argument | Type  | Description                              |
| -------- | ----- | ---------------------------------------- |
| `id`     | `ID!` | The `id` of the Cart you wish to delete. |

<alert type="info">

If no cart exists with the `id` provided, the `DeletePayload` response will tell you.

</alert>

## `DeletePayload`

| Field     | Type       | Description                                                                        |
| --------- | ---------- | ---------------------------------------------------------------------------------- |
| `success` | `Boolean!` | Either `true` or `false`. If an error occurs, it will be `false` with a `message`. |
| `message` | `String`   | A success or failure message will be returned.                                     |

## Example

<code-group>
  <code-block label="Mutation" active>

```graphql
mutation {
  deleteCart(input: { id: "ck5r8d5b500003f5o2aif0v2b" }) {
    success
    message
  }
}
```

  </code-block>
  <code-block label="Successful response">

```json
{
  "data": {
    "deleteCart": {
      "success": true,
      "message": "Cart successfully deleted"
    }
  }
}
```

  </code-block>
  <code-block label="Unsuccessful response">

```json
{
  "data": {
    "deleteCart": {
      "success": false,
      "message": "Cart does not exist"
    }
  }
}
```

  </code-block>
</code-group>

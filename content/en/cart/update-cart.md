---
title: Update Cart
description: ""
position: 11
category: Cart
---

Use the `updateCart` mutation to delete a cart, and all items associated to it.

## Mutation

`updateCart(input: UpdateCartInput!): Cart!`

| Arguments | Type               |
| --------- | ------------------ |
| `input`   | `UpdateCartInput!` |

The `updateCart` mutation will always return the updated [`Cart`](/graphql-types#cart).

## `UpdateCartInput!`

| Argument   | Type                                            | Description                                |
| ---------- | ----------------------------------------------- | ------------------------------------------ |
| `id`       | `ID!`                                           | The `id` of the Cart you want to update.   |
| `currency` | [`CurrencyInput`](/cart/get-cart#currencyinput) | Update the cart currency.                  |
| `email`    | `String`                                        | Update the email associated with the cart. |
| `notes`    | `String`                                        | Let customer save notes for the cart.      |
| `metadata` | [`Json`](/metadata)                             | Custom meta object array for the cart.     |

<alert type="info">

If no cart item exists with the `id` provided, an error will be returned.

</alert>

## Example

<code-group>
  <code-block label="Mutation" active>

```graphql
mutation {
  updateCart(
    input: {
      id: "ck5r8d5b500003f5o2aif0v2b"
      currency: { code: USD }
      email: "hi@cartql.com"
      notes: "These are my order notes"
      metadata: {
        subscribeToUpdates: "hi@cartql.com"
        referredBy: "@notrab"
        acceptsMarketing: true
      }
    }
  ) {
    id
    currency {
      code
    }
    email
    notes
    metadata
  }
}
```

  </code-block>
  <code-block label="Response">

```json
{
  "data": {
    "updateCart": {
      "id": "ck5r8d5b500003f5o2aif0v2b",
      "currency": {
        "code": "USD"
      },
      "email": "hi@cartql.com",
      "notes": "These are my order notes",
      "metadata": {
        "subscribeToUpdates": "hi@cartql.com"
        "referredBy": "@notrab"
        "acceptsMarketing": true
      }
    }
  }
}
```

  </code-block>
</code-group>

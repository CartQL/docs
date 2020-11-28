---
title: Set Cart Items
description: ""
position: 14
category: Cart
---

Use the `setItems` mutation to set, or overwrite all cart items.

## Mutation

`setItems(input: SetCartItemsInput!): Cart!`

| Arguments | Type                 |
| --------- | -------------------- |
| `input`   | `SetCartItemsInput!` |

The `setItems` mutation will always return the [`Cart`](/graphql-types#cart) object.

## `SetCartItemsInput!`

You can set all cart items at any time.

<alert type="warning">

The `setItems` mutation will replace all existing items.

</alert>

| Argument | Type                                        | Description                                          |
| -------- | ------------------------------------------- | ---------------------------------------------------- |
| `cartId` | `ID!`                                       | The `id` of the cart you are adding items to         |
| `items`  | [`[SetCartItemInput!]!`](#setcartiteminput) | The same as `AddToCartInput`, just without `cartId`. |

## `[SetCartItemInput!]!`

| Argument      | Type                 | Description                            |
| ------------- | -------------------- | -------------------------------------- |
| `id`          | `ID!`                | The `id` of the item you are adding.   |
| `name`        | `String`             | Give items a name.                     |
| `description` | `String`             | Give items a description.              |
| `type`        | `CartItemType = SKU` | `SKU` _(default)_, `TAX`, `SHIPPING`.  |
| `images`      | `[String]`           | Any URLs to images for the item.       |
| `price`       | `Int!`               | The item price in cents.               |
| `quantity`    | `Int = 1`            | Quantity of items to add.              |
| `metadata`    | [`Json`](/metadata)  | Custom meta object array for the cart. |

## Example

<code-group>
  <code-block label="Mutation" active>

```graphql
mutation {
  setItems(
    input: {
      cartId: "ck5r8d5b500003f5o2aif0v2b"
      items: [
        {
          id: "5e3293a3462051"
          name: "Full Logo Tee"
          description: "Purple Triblend / L"
          images: ["full-logo-tee.png"]
          price: 2000
          quantity: 10
          metadata: { customEngraving: "GraphQL" }
        }
        {
          id: "5e3293a3462051"
          name: "Cap"
          description: "Blue Cap / L"
          images: ["cap.png"]
          price: 1000
          quantity: 1
        }
      ]
    }
  ) {
    id
    totalItems
    items {
      id
      name
      lineTotal {
        amount
      }
      metadata
    }
  }
}
```

  </code-block>
  <code-block label="Response">

```json
{
  "data": {
    "setItems": {
      "id": "ck5r8d5b500003f5o2aif0v2b",
      "totalItems": 11,
      "items": [
        {
          "id": "ck5r8d5b500003f5o2aif0v2b",
          "name": "Full Logo Tee",
          "lineTotal": {
            "amount": 20000
          },
          "metadata": {
            "customEngraving": "GraphQL"
          }
        },
        {
          "id": "ck5r8d5b500003f5o2aif0v2b",
          "name": "Cap",
          "lineTotal": {
            "amount": 1000
          }
        }
      ]
    }
  }
}
```

  </code-block>
</code-group>

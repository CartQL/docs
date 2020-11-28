---
title: Add Item
description: ""
position: 20
category: Cart Items
---

Use the `addItem` mutation to add new items to the cart.

## Mutation

`addItem(input: AddToCartInput!): Cart!`

| Arguments | Type              |
| --------- | ----------------- |
| `input`   | `AddToCartInput!` |

The `addItem` mutation will always return the updated [`Cart`](/graphql-types#cart) object.

## `AddToCartInput!`

You can add items to the cart at any time.

<alert type="warning">

You must provide a unique `id` for cart items, otherwise you will overwrite any existing data, and increment existing quantities.

</alert>

| Argument      | Type                                       | Description                                   |
| ------------- | ------------------------------------------ | --------------------------------------------- |
| `cartId`      | `ID!`                                      | The `id` of the cart you are adding items to. |
| `id`          | `ID!`                                      | The `id` of the item you are adding.          |
| `name`        | `String`                                   | Give items a name.                            |
| `description` | `String`                                   | Give items a description.                     |
| `type`        | [`CartItemType = SKU`](#cartitemtype--sku) | `SKU` _(default)_, `TAX`, `SHIPPING`.         |
| `images`      | `[String]`                                 | Any URLs to images for the item.              |
| `price`       | `Int!`                                     | The item price in cents.                      |
| `quantity`    | `Int = 1`                                  | Quantity of items to add.                     |
| `metadata`    | `Json`                                     | Custom meta object array for the cart.        |

<alert type="info">

If no cart exists with the `id` provided, one will be created for you.

</alert>

## Example

<code-group>
  <code-block label="Mutation" active>

```graphql
mutation {
  addItem(
    input: {
      cartId: "ck5r8d5b500003f5o2aif0v2b"
      id: "5e3293a3462051"
      name: "Full Logo Tee"
      description: "Purple Triblend / L"
      images: ["full-logo-tee.png"]
      price: 2000
      quantity: 10
      metadata: { customEngraving: "GraphQL" }
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
    items {
      id
      name
      description
      images
      unitTotal {
        amount
        formatted
      }
      lineTotal {
        amount
        formatted
      }
      quantity
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
    "addItem": {
      "id": "ck5r8d5b500003f5o2aif0v2b",
      "isEmpty": false,
      "abandoned": false,
      "totalItems": 10,
      "totalUniqueItems": 1,
      "subTotal": {
        "formatted": "$200.00"
      },
      "items": [
        {
          "id": "5e3293a3462051",
          "name": "Full Logo Tee",
          "description": "Purple Triblend / L",
          "images": ["full-logo-tee.png"],
          "unitTotal": {
            "amount": 2000,
            "formatted": "$20.00"
          },
          "lineTotal": {
            "amount": 20000,
            "formatted": "$200.00"
          },
          "quantity": 10,
          "metadata": {
            "customEngraving": "GraphQL"
          }
        }
      ]
    }
  }
}
```

  </code-block>
</code-group>

## `CartItemType = SKU`

The `type` value will change how cart totals are calculated.

### `SKU`

...

### `TAX`

...

### `SHIPPING`

...

---
title: Get or Create Cart
description: ""
position: 10
category: Cart
---

Carts are public, shared by all, and retrievable by `id`. Carts contain all of the basic meta you need to build a cart + checkout, including totals with tax, shipping, and cart item line, and sub totals.

<alert type="info">

Carts persist for 14 days. Make sure you update the cart if to keep it alive if you are sending customers recovery/abandoned emails.

</alert>

## Query

`cart(id: ID!, currency: CurrencyInput): Cart!`

| Arguments  | Type                              | Description                            |
| ---------- | --------------------------------- | -------------------------------------- |
| `id`       | [`ID!`](#id)                      | The `id` of the cart you want to fetch |
| `currency` | [`CurrencyInput`](#currencyinput) | The cart currency properties           |

The `cart` query will always return the [`Cart`](/graphql-types#cart) object.

### `ID!`

You must provide an `id` for the cart you want to fetch. If no cart exists, CartQL will create one for you with the `id` provided.

<alert type="warning">

Carts are public. Make sure to set a unique complex cart `id`.

</alert>

<code-group>
  <code-block label="Request" active>

```graphql
{
  cart(id: "ck5r8d5b500003f5o2aif0v2b") {
    id
    isEmpty
    totalItems
    items {
      id
    }
  }
}
```

  </code-block>
  <code-block label="Response">

```json
{
  "data": {
    "cart": {
      "id": "ck5r8d5b500003f5o2aif0v2b",
      "isEmpty": true,
      "totalItems": 0,
      "items": []
    }
  }
}
```

  </code-block>
</code-group>

### `CurrencyInput`

When fetching a cart that does not exist, the values you provide here will set the cart currency.

| Field                | Type           | Default value |
| -------------------- | -------------- | ------------- |
| `code`               | `CurrencyCode` | `USD`         |
| `symbol`             | `String`       | `$`           |
| `thousandsSeparator` | `String`       | `,`           |
| `decimalSeparator`   | `String`       | `.`           |
| `decimalDigits`      | `Int`          | `2`           |

<code-group>
  <code-block label="Request" active>

```graphql
query {
  cart(id: "ck5r8d5b500003f5o2aif0v2b", currency: { code: GBP }) {
    id
    currency {
      code
      symbol
    }
  }
}
```

  </code-block>
  <code-block label="Response">

```json
{
  "data": {
    "cart": {
      "id": "ck5r8d5b500003f5o2aif0v2b",
      "currency": {
        "code": "GBP",
        "symbol": "£"
      }
    }
  }
}
```

  </code-block>
</code-group>

Learn more about managing [currencies](/currency).

## The `Cart` object

Carts are the core concept of CartQL. Bring your own PIM, and use CartQL to manage cart metadata.

| Field              | Type                              | Description                                                                                                           |
| ------------------ | --------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `id`               | `ID!`                             | A custom unique identifer for the cart provided by you.                                                               |
| `currency`         | [`Currency!`](/currency#currency) | The current currency details of the cart.                                                                             |
| `email`            | `String`                          | The customer email who the cart belongs to.                                                                           |
| `totalItems`       | `Int`                             | The number of total items in the cart.                                                                                |
| `totalUniqueItems` | `Int`                             | The number of total unique items in the cart.                                                                         |
| `items`            | [`[CartItem!]!`](#cartitem)       | The items in the cart.                                                                                                |
| `subTotal`         | [`Money!`](/currency#money)       | Sum of all SKU items, excluding discounts, taxes, shipping, including the raw/formatted amounts and currency details. |
| `shippingTotal`    | [`Money!`](/currency#money)       | The cart total for all items with type `SHIPPING`, including the raw/formatted amounts and currency details.          |
| `taxTotal`         | [`Money!`](/currency#money)       | The cart total for all items with type `TAX`, including the raw/formatted amounts and currency details.               |
| `grandTotal`       | [`Money!`](/currency#money)       | The grand total for all items, including shipping, including the raw/formatted amounts and currency details.          |  | `isEmpty` | `Boolean` | A simple helper method to check if the cart is empty. |
| `abandoned`        | `Boolean`                         | A simple helper method to check if the cart hasn't been updated in the last 2 hours.                                  |
| `metadata`         | [`Json`](/metadata)               | Custom metadata for the cart.                                                                                         |
| `notes`            | `String`                          | Any notes related to the cart/checkout.                                                                               |
| `createdAt`        | `Date!`                           | The date and time the cart was created.                                                                               |
| `updatedAt`        | `Date!`                           | The date and time the cart was created.                                                                               |

## `[CartItem!]!`

Each `CartItem` is made up of the values you provide when adding to cart. These items are provided by you, and only an `id`, and `price` is required for items to be added.

There are also a handful of other fields you can define for capturing more details about your items.

| Field         | Type                                               | Description                                              |
| ------------- | -------------------------------------------------- | -------------------------------------------------------- |
| `id`          | `ID!`                                              | A custom unique identifier for the item provided by you. |
| `name`        | `String`                                           | The items name.                                          |
| `description` | `String`                                           | The items description.                                   |
| `type`        | [`CartItemType`](/add-cart-item#cartitemtype--sku) | The type of item this is, `SKU`, `TAX`, or `SHIPPING`.   |
| `images`      | `[String]`                                         | An array of image URLs for the item.                     |
| `unitTotal`   | [`Money!`](/currency#money)                        | The unit total for the individual item.                  |
| `lineTotal`   | [`Money!`](/currency#money)                        | The line total (quantity `*` price).                     |
| `quantity`    | `Int!`                                             | The number of items.                                     |
| `attributes`  | [`[CustomCartAttribute!]!`](#customcartattribute)  | Custom key/value attributes array for the item.          |
| `createdAt`   | `Date!`                                            | The date and time the item was added.                    |
| `updatedAt`   | `Date!`                                            | The date and time the item was last updated.             |

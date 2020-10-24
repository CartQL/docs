---
title: Checkout
description: ""
position: 25
category: Checkout
---

Use the `checkout` mutation to convert carts to an unpaid order. You can also capture billing and shipping addresses, as well as customer email, and notes.

## Mutation

`checkout(input: CheckoutInput!): Order!`

| Arguments | Type             |
| --------- | ---------------- |
| `input`   | `CheckoutInput!` |

The `checkout` mutation will always return an unpaid [`Order`](#order) object.

## `CheckoutInput!`

<alert type="warning">

A cart must have items in order to checkout. If the `cartId` does not exist, an error will be returned.

</alert>

| Argument   | Type                             | Description                                                  |
| ---------- | -------------------------------- | ------------------------------------------------------------ |
| `cartId`   | `ID!`                            | The `id` of the cart you are adding items to.                |
| `email`    | `String`                         | Set the email associated with the order.                     |
| `notes`    | `String`                         | Let customer save notes for the order.                       |
| `shipping` | [`AddressInput!`](#addressinput) | The customer shipping address.                               |
| `billing`  | [`AddressInput`](#addressinput)  | The customer billing address, will be shipping if not given. |

<alert type="info">

If you already set the `email` and `notes` on a cart, they will be used.

</alert>

## `AddressInput!`

| Field        | Type                                    | Description                                    |
| ------------ | --------------------------------------- | ---------------------------------------------- |
| `company`    | `String`                                | A company name, if applicable for the address. |
| `name`       | `String!`                               | The recipient name.                            |
| `line1`      | `String!`                               | The address line 1.                            |
| `line2`      | `String`                                | The address line 2.                            |
| `city`       | `String!`                               | The address city.                              |
| `state`      | `String`                                | The address state.                             |
| `postalCode` | `String!` The addess post, or zip code. |
| `country`    | `String!`                               | The address country.                           |

## Example

<code-group>
  <code-block label="Mutation" active>

```graphql
mutation {
  checkout(
    input: {
      cartId: "ck5r8d5b500003f5o2aif0v2b"
      email: "jamie@cartql.com"
      shipping: {
        name: "Jamie Barton"
        line1: "123 Cart Lane"
        city: "Newcastle upon Tyne"
        postalCode: "NE14 CQL"
        country: "England"
      }
    }
  ) {
    id
    email
    billing {
      name
      line1
      city
      postalCode
      country
    }
    shippingTotal {
      amount
      formatted
    }
    taxTotal {
      amount
      formatted
    }
    subTotal {
      amount
      formatted
    }
    grandTotal {
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
    "checkout": {
      "id": "5f9461ba9d48bb00170b00c5",
      "email": "jamie@cartql.com",
      "billing": {
        "name": "Jamie Barton",
        "line1": "123 Cart Lane",
        "city": "Newcastle upon Tyne",
        "postalCode": "NE14 CQL",
        "country": "England"
      },
      "shippingTotal": {
        "amount": 0,
        "formatted": "$0.00"
      },
      "taxTotal": {
        "amount": 0,
        "formatted": "$0.00"
      },
      "subTotal": {
        "amount": 21000,
        "formatted": "$210.00"
      },
      "grandTotal": {
        "formatted": "$210.00"
      }
    }
  }
}
```

  </code-block>
</code-group>

## `Order`

The `checkout` mutation returns an `Order` that cannot be updated. It is recommended to use webhooks to send this onto another service to persist orders.

Orders are immutable cart objects, which also have `status`, `shipping`, and `billing` values.

Cart items are converted to order items.

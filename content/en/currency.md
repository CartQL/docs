---
title: Currency
description: ""
position: 3
category: ""
---

CartQL will automatically format cart, and item totals based on the set currency. You can set the currency when creating a cart, or by updating it later.

Whether you're fetching the cart, or cart item totals, the [`Money`](#money) object will contain some helpful fields you can query.

These can be set by you when creating, or updating carts, but are automatically updated based on the provided cart currency `code`.

## `Currency`

| Field                | Type                            | Description                                            |
| -------------------- | ------------------------------- | ------------------------------------------------------ |
| `code`               | [`CurrencyCode`](#currencycode) | The currency code enum, e.g. `USD`, `GBP`, `EUR`, etc. |
| `symbol`             | `String`                        | The currency symbol, e.g. `$`, `£`, `€`, etc.          |
| `thousandsSeparator` | `String`                        | The thousand separator, e.g. `,`, `.`                  |
| `decimalSeparator`   | `String`                        | The decimal separator, e.g. `.`                        |
| `decimalDigits`      | `Int`                           | The number of decimal places for the currency.         |

## Update cart currency

```graphql
mutation {
  updateCart(
    input: { id: "ck5r8d5b500003f5o2aif0v2b", currency: { code: USD } }
  ) {
    id
    currency {
      code
      symbol
      thousandsSeparator
      decimalSeparator
      decimalDigits
    }
  }
}
```

## `CurrencyCode`

The `code` for `currency` is one of the below enums.

`AED`,
`AFN`,
`ALL`,
`AMD`,
`ANG`,
`AOA`,
`ARS`,
`AUD`,
`AWG`,
`AZN`,
`BAM`,
`BBD`,
`BDT`,
`BGN`,
`BHD`,
`BIF`,
`BMD`,
`BND`,
`BOB`,
`BRL`,
`BSD`,
`BTC`,
`BTN`,
`BWP`,
`BYR`,
`BZD`,
`CAD`,
`CDF`,
`CHF`,
`CLP`,
`CNY`,
`COP`,
`CRC`,
`CUC`,
`CUP`,
`CVE`,
`CZK`,
`DJF`,
`DKK`,
`DOP`,
`DZD`,
`EGP`,
`ERN`,
`ETB`,
`EUR`,
`FJD`,
`FKP`,
`GBP`,
`GEL`,
`GHS`,
`GIP`,
`GMD`,
`GNF`,
`GTQ`,
`GYD`,
`HKD`,
`HNL`,
`HRK`,
`HTG`,
`HUF`,
`IDR`,
`ILS`,
`INR`,
`IQD`,
`IRR`,
`ISK`,
`JMD`,
`JOD`,
`JPY`,
`KES`,
`KGS`,
`KHR`,
`KMF`,
`KPW`,
`KRW`,
`KWD`,
`KYD`,
`KZT`,
`LAK`,
`LBP`,
`LKR`,
`LRD`,
`LSL`,
`LYD`,
`MAD`,
`MDL`,
`MGA`,
`MKD`,
`MMK`,
`MNT`,
`MOP`,
`MRO`,
`MTL`,
`MUR`,
`MVR`,
`MWK`,
`MXN`,
`MYR`,
`MZN`,
`NAD`,
`NGN`,
`NIO`,
`NOK`,
`NPR`,
`NZD`,
`OMR`,
`PAB`,
`PEN`,
`PGK`,
`PHP`,
`PKR`,
`PLN`,
`PYG`,
`QAR`,
`RON`,
`RSD`,
`RUB`,
`RWF`,
`SAR`,
`SBD`,
`SCR`,
`SDD`,
`SDG`,
`SEK`,
`SGD`,
`SHP`,
`SLL`,
`SOS`,
`SRD`,
`STD`,
`SVC`,
`SYP`,
`SZL`,
`THB`,
`TJS`,
`TMT`,
`TND`,
`TOP`,
`TRY`,
`TTD`,
`TVD`,
`TWD`,
`TZS`,
`UAH`,
`UGX`,
`USD`,
`UYU`,
`UZS`,
`VEB`,
`VEF`,
`VND`,
`VUV`,
`WST`,
`XAF`,
`XCD`,
`XBT`,
`XOF`,
`XPF`,
`YER`,
`ZAR`,
`ZMW`,
`WON`

## `Money`

The Money type is used when describing the Cart and Cart Item unit/line totals.

| Field       | Type        | Description                                              |
| ----------- | ----------- | -------------------------------------------------------- |
| `amount`    | `Int`       | The raw amount in cents/pence, e.g. `1000`.              |
| `currency`  | `Currency!` | The currency of the money amount.                        |
| `formatted` | `String!`   | The formatted amount with the cart currency. E.g. `$10`. |

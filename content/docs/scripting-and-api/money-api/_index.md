---
date: 2025-05-15T08:02:32+10:00
title: Money API
draft: true
---
# Overview


When scripting, calculating decimals can often be problematic on certain coding languages.  However, to remediate this, we have implemented a library within the platform, to allow you to easily and accurately calculate decimal values.  This is known as “BigDecimal” and for those who have a Java background, may have prior exposure to how this operates.  This is often used for money fields within Servicely, due to the fact when you get a Money value from a Money field, it will be a BigDecimal object.


# Creation of a BigDecimal Object


When creating a BigDecimal object, you can pass in a variety of “types” and then calculate them together.  An example of this is as per below:


```javascript
// BigDecimal can be build
// from a number
BigDecimal(0.1)

// from string
BigDecimal("0.1")

//or another BigDecimal
let dot2 = BigDecimal("0.2")
BigDecimal(BigDecimal(0.1).multiply(BigDecimal(3)))
```


# Available API options


| Function                                                                                              | Returns    | Description                                                                                                |
| ----------------------------------------------------------------------------------------------------- | ---------- | ---------------------------------------------------------------------------------------------------------- |
| ```compareTo(arg: BigDecimal)```                                                                      | number     | Compare this BigDecimal with another BigDecimal                                                            |
| ```add(arg: BigDecimal)```                                                                            | BigDecimal | Add a BigDecimal to this BigDecimal                                                                        |
| ```remainder(divisor: BigDecimal)```                                                                  | BigDecimal | Return the remainder of dividing this BigDecimal by the specified BigDecimal                               |
| ```multiply(arg: BigDecimal)```                                                                       | BigDecimal | Multiply this BigDecimal by the specified BigDecimal                                                       |
| ```round()```                                                                                         | BigDecimal | Round this BigDecimal to the nearest whole number                                                          |
| ```divide(arg: BigDecimal)```                                                                         | BigDecimal | Divide this BigDecimal by the specified BigDecimal                                                         |
| ```subtract(arg: BigDecimal)```                                                                       | BigDecimal | Subtract the specified BigDecimal from this BigDecimal                                                     |
| ```stripTrailingZeros()```                                                                            | BigDecimal | Remove any trailing zeros from the decimal part of this BigDecimal                                         |
| ```plus()```                                                                                          | BigDecimal | Returns a BigDecimal whose value is (+this), and whose scale is this.scale()                               |
| ```format(arg: BigDecimal, currency: 3-letter international (ISO 4217) currency code, locale code)``` | string     | Format this BigDecimal to a specific locale. Such as: ```Money.format(someRec.C_Rate(), “EUR”, “de_DE”)``` |
| ```format()```                                                                                        | string     | Format this BigDecimal using the default pattern                                                           |
| ```withLang(locale: string)```                                                                        | BigDecimal | Return a copy of this BigDecimal with the specified locale, Such as de_DE                                  |



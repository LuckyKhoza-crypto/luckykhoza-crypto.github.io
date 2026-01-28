---
title: "| vs || Operator in Java"
categories: [java, operators ]
tags: [java, operators]    # TAG names should always be lowercase
layout: page
permalink: /posts/:path
---
This is a straightforward explanation of how `|` and `||` work in Java.

# dive in
`|` and `||`  both signify the **OR** operator in Java, used to evaluate boolean expressions.

## the | Operator
in the example below, `firstError(String s1)` and `secondError(Strign s2)` are methods that do some computation and return a boolean.

```Java
boolean isError = firstError(string1) | secondError(string2);
```
using `|` means both methods are always evaluated
 `firstError(string1)`, then `secondError(string2)`. 
This is useful when you must run both methods, even if the first one already returns true or false.
This behavior contrasts with ||, which may skip the second evaluation.


## the || Operator
this operator is crucial for situations where you don't want to continue computation if there is an earlier failure.
Below, if `fn1(v1)` returns `true`, then the OR condition is already `true`, `fn2(v1)` is not executed.
If `fn1(v1)` returns `false`, then `fn2(v)` is evaluated.

```java
boolean isError = fn1(v1) || fn2(v1);
```
`||` short-circuts the computation we are doing, thus, stopping early if `true` is returned.

# conclusion

each of these operators can be used for different situations. Understanding the intention behind your logic will help you choose the right operator for your scenario.

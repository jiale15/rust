# Floating-point Numbers

Floating-point numbers are real numbers: they may have a fractional part. They are represented in the machine as a pattern of binary bits, using the [IEEE-754 specification](https://en.wikipedia.org/wiki/IEEE_754).
People refer to floating-point numbers as floats.

Floating point numbers are always signed. Signedness means reserving one of the bits of the number to indicate
whether or not that number is negative.

Floating point numbers have a **bit width**, which is just the number of bits making up that number. This impacts
the range and precision of values which can be represented by that type.

Rust has 2 floating-point primitive types: `f32` and `f64`. The number after the `f` indicates the bit width. In other languages,`f32` is sometimes referred to as "single-precision", and `f64` is sometimes referred to as "double-precision".

浮点数是实数：它们可能有小数部分。 它们在机器中表示为二进制位的模式，使用 [IEEE-754 规范](https://en.wikipedia.org/wiki/IEEE_754)。
人们将浮点数称为浮点数。

浮点数总是有符号的。 有符号性意味着保留数字的一位来指示该数字是否为负。

浮点数有一个**位宽**，它只是构成该数字的位数。 这会影响可以由该类型表示的值的范围和精度。

Rust 有 2 种浮点原始类型：`f32` 和 `f64`。 `f` 后面的数字表示位宽。 在其他语言中，`f32` 有时被称为“单精度”，而 `f64` 有时被称为“双精度”。

## Which should I use?

In general, use `f64`: it's as fast as `f32` on most modern consumer hardware, and significantly reduces the incidence of [floating-point inaccuracy](https://0.30000000000000004.com/).

If you need infinite-precision rational numbers, you might use the [`num-rational` crate](https://crates.io/crates/num-rational), which provides a `BigRational` type. If you need fixed-precision decimal numbers, you might use the [`rust_decimal` crate](https://crates.io/crates/rust_decimal), which provides a `Decimal` type.

一般来说，使用`f64`：它在大多数现代消费类硬件上与`f32`一样快，并且显着降低了[浮点不准确]的发生率（https://0.30000000000000004.com/）。

如果你需要无限精度的有理数，你可以使用 [`num-rational` crate](https://crates.io/crates/num-rational)，它提供了 `BigRational` 类型。 如果您需要固定精度的十进制数，您可以使用 [`rust_decimal` crate](https://crates.io/crates/rust_decimal)，它提供了 `Decimal` 类型。

## Converting between floating-point numbers

Rust has no implicit numeric conversions. If you need to cast between float types, there are two basic strategies: the `as` keyword, and the `From` and `TryFrom` traits.

Using the `as` keyword is simple: `expr as Type`. However, there are a number of [caveats and subtleties](https://doc.rust-lang.org/nomicon/casts.html) that you need to keep in mind when using `as` casts.

Trait-based casting is slightly more involved, but safer: conversion traits are only implemented where they are safe. For example, [`f32`](https://doc.rust-lang.org/std/primitive.f32.html) implements `From<u8>`, `From<u16>`, `From<i8>`, and `From<i16>`: any value representable by any of these types is guaranteed to be representable in an `f32`. It can be used like `f32::from(expr)`, or `expr.into()`, where `expr` resolves to one of those types.

When converting floating-point values `as`-casting is often preferred simply because of the relative scarcity of trait-based cast implementations. As of Oct 2020, `TryFrom` is not implemented for floating-point numbers. `as`-casting from `f32` to `f64` is lossless. The reverse is lossy, but has a defined casting protocol intended to minimize loss.

Rust 没有隐式的数字转换。如果需要在浮点类型之间进行转换，有两种基本策略：`as` 关键字，以及 `From` 和 `TryFrom` 特征。

使用 `as` 关键字很简单：`expr as Type`。但是，在使用 `as` 强制转换时，您需要牢记一些 [警告和微妙之处](https://doc.rust-lang.org/nomicon/casts.html)。

基于特征的转换稍微复杂一些，但更安全：转换特征只在安全的地方实现。例如，[`f32`](https://doc.rust-lang.org/std/primitive.f32.html) 实现了 `From<u8>`、`From<u16>`、`From<i8>` , 和 `From<i16>`：任何可以由这些类型表示的值都保证可以在 `f32` 中表示。它可以像 `f32::from(expr)` 或 `expr.into()` 一样使用，其中 `expr` 解析为其中一种类型。

当转换浮点值时，`as` 转换通常是首选，因为基于特征的转换未完全实现。截至 2020 年 10 月，浮点数未实现“TryFrom”。从 `f32` 到 `f64` 的 `as` 转换是无损的。反过来是有损的，但有一个明确的转换协议，旨在最大限度地减少损失。
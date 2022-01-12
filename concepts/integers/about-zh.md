# Integers

Integers are whole numbers. They have no factional or decimal part. They are represented in the machine as a pattern of binary bits.

Integers may or may not be signed. Signedness means reserving one of the bits of the number to indicate
whether or not that number is negative.

Integers all have a **bit width**, which is just the number of bits making up that number. This impacts
the maximum value which can be represented by that integer type.

For example, one of the most common integer types is a `u8`: an unsigned, 8-bit integer. You may
recognize this type as a single byte. This has a minimum value of 0 and a maximum value of 256.

Rust has 12 integer primitive types, broken out by bit width and signedness:

Integers是整数。他们没有派系或小数部分。它们在机器中表示为二进制位的模式。

整数可以有符号（Signed）也可以无符号（Unsigned）。有符号性意味着保留数字的一位以指示该数字是否为负。

整数都有一个**位宽**，这只是构成该数字的位数。这会影响该整数类型可以表示的最大值。

例如，最常见的整数类型之一是“u8”：一个无符号的 8 位整数。您可以将此类型识别为单个字节。最小值为 0，最大值为 256。

Rust 有 12 种整数原始类型，按位宽和符号划分：

| Unsigned | Signed  |
| -------- | ------- |
| `u8`     | `i8`    |
| `u16`    | `i16`   |
| `u32`    | `i32`   |
| `u64`    | `i64`   |
| `u128`   | `i128`  |
| `usize`  | `isize` |

An integer's bit width is always indicated by the number after the `u` or `i`. `usize` and `isize` are special: they have the same width as a pointer on the target machine. This means that on a 64-bit architecture, `usize` and `isize` are 64 bits wide, but on a 32-bit architecture, they are 32 bits wide.

整数的位宽总是由 `u` 或 `i` 后面的数字表示。`usize` 和 `isize` 是特殊的：它们与目标机器上的指针具有相同的宽度。这意味着在 64 位架构上，`usize` 和 `isize` 是 64 位宽，但在 32 位架构上，它们是 32 位宽。

## Which should I use?

In general, if you just need to represent some number, use an `i32`: 32 bits has a wide enough range that it's relatively unlikely to overflow, and signed numbers have fewer surprises than unsigned numbers. `i32` is equivalent to a `long` in C, or an `int` in Java. If you use a numeric literal and don't explicitly annotate the type, it will default to `i32`.

If you're working with binary data, it's easiest to work with bytes: `&[u8]` or `Vec<u8>`.

Rust uses `usize` for size and indexing of collections. This is because a computer can only theoretically address `usize::MAX` bytes of memory, so no larger in-memory collections are possible. Therefore, `usize` can be useful if you're doing a lot of work with collections.

If your data doesn't fit into a 32-bit integer, consider broadening to a 64 or 128 bit integer. If your data doesn't fit into a 128-bit integer, then you can use a big integer type such as is provided by [`num-bigint`](https://github.com/rust-num/num-bigint).

16 bit integers are not very common, but can be useful when targeting certain microcontrollers.

If you know that there are no valid negative cases for your application, it is better to use an unsigned integer instead of a signed integer. Counting is a good example of this.

通常，如果您只需要表示某个数字，请使用 `i32`：32 位的范围足够宽，相对不太可能溢出，并且有符号数字比无符号数字有更少的意外。`i32` 相当于 C 中的 `long` 或 Java 中的 `int`。如果您使用数字文字并且没有显式注释类型，它将默认为 `i32`。

如果你正在处理二进制数据，使用字节是最简单的：`&[u8]` 或 `Vec<u8>`。

Rust 使用 `usize` 来确定集合的大小和索引。这是因为计算机理论上只能寻址 `usize::MAX` 字节的内存，因此不可能有更大的内存集合。因此，如果您对集合进行大量工作，`usize` 会很有用。

如果您的数据不适合 32 位整数，请考虑扩展为 64 或 128 位整数。如果您的数据不适合 128 位整数，那么您可以使用 [`num-bigint`](https://github.com/rust-num/num-bigint) 提供的大整数类型）。

16 位整数不是很常见，但在针对某些微控制器时很有用。

如果您知道您的应用程序没有有效的负值情况，最好使用无符号整数而不是有符号整数。计数就是一个很好的例子。

## Converting between integers

Rust has no implicit numeric conversions. If you need to cast between integer types, there are two basic strategies: the `as` keyword, and the `From` and `TryFrom` traits.

Using the `as` keyword is simple: `expr as Type`. However, there are a number of [caveats and subtleties](https://doc.rust-lang.org/nomicon/casts.html) that you need to keep in mind when using `as` casts.

Trait-based casting is slightly more involved, but safer: conversion traits are only implemented where they are safe. For example, [`i32`](https://doc.rust-lang.org/std/primitive.i32.html) implements `From<u8>`, `From<u16>`, `From<i8>`, and `From<i16>`: any value representable by any of these types is guaranteed to be representable in an `i32`. It can be used like `i32::from(expr)`, or `expr.into()`, where `expr` resolves to one of those types. `i32` also implements `TryFrom<u32>`, `TryFrom<u64>`, `TryFrom<u128>`, `TryFrom<usize>`, `TryFrom<i64>`, `TryFrom<i128>`, and `TryFrom<isize>`. These conversions will explicitly either succeed or overflow, depending on the value. To use these, you will need to import the `std::convert::TryFrom` or `std::convert::TryInto` traits as appropriate, and then use `i32::try_from(expr)` or `expr.try_into()`, where `expr` resolves to an appropriate type.

Using trait-based casting instead of `as` casting is generally preferred, particularly when converting from a wider to a narrower type. Trait-based casting is inconsequentially more expensive than `as` casting: using `as` for performance reasons is not worth it unless in an extremely hot loop.

Rust 没有隐式的数字转换。如果需要在整数类型之间进行转换，有两种基本策略：`as` 关键字，以及 `From` 和 `TryFrom` 特征。

使用 `as` 关键字很简单：`expr as Type`。但是，在使用 `as` 强制转换时，您需要牢记一些 [警告和微妙之处](https://doc.rust-lang.org/nomicon/casts.html)。

基于特征的转换稍微复杂一些，但更安全：转换特征只在安全的地方实现。例如，[`i32`](https://doc.rust-lang.org/std/primitive.i32.html) 实现了`From<u8>`、`From<u16>`、`From<i8>` , 和 `From<i16>`：任何可以由这些类型表示的值都保证可以在 `i32` 中表示。它可以像 `i32::from(expr)` 或 `expr.into()` 一样使用，其中 `expr` 解析为其中一种类型。`i32` 还实现了 `TryFrom<u32>`、`TryFrom<u64>`、`TryFrom<u128>`、`TryFrom<usize>`、`TryFrom<i64>`、`TryFrom<i128>` 和 `TryFrom <大小>`。这些转换将显式成功或溢出，具体取决于值。要使用这些，您需要根据需要导入 `std::convert::TryFrom` 或 `std::convert::TryInto` 特征，然后使用 `i32::try_from(expr)` 或 `expr.try_into ()`，其中 `expr` 解析为适当的类型。

通常首选使用基于特征的转换而不是 `as` 转换，特别是在从较宽类型转换为较窄类型时。基于特征的强制转换比 `as` 强制转换更昂贵：出于性能原因使用 `as` 是不值得的，除非在非常热的循环中。
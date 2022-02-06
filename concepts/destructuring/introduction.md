# Introduction

Destructuring is a way to break apart compound values in Rust. It is often used to extract fields from tuples or structs.
解构是一种在 Rust 中分解复合值的方法。 它通常用于从元组或结构体中提取字段。

For example, the below snippet extracts two values from a tuple:
例如，下面的代码片段从一个元组中提取两个值：
```rust
let (first, second) = (1, 2);
```

The value `1` is bound to the variable `first`.
The value `2` is bound to the variable `second`.

值 `1` 绑定到变量 `first`。
值 `2` 绑定到变量 `second`。
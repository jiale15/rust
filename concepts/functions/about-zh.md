# About

Functions are bodies of code containing one or more [statements or expressions][statements or expressions]. A function may optionally
[return an value][return value].

Rust style is to use [snake case][snake case] for a function name, which is prefaced by the `fn` keyword for a function definition. For example

函数是包含一个或多个[语句或表达式][语句或表达式]的代码体。函数可以选择[返回一个值][返回值]。

Rust风格是使用[蛇形命名法][蛇形命名法]来命名函数，在函数定义中以 `fn` 关键字开头。

例如
```rust
fn do_nothing() {}
```

The parentheses surround zero or more parameters, separated by commas. A parameter is a binding to a value of a particular type which is passed into the function.
Even if there are no parameters the parentheses are still required in the function definition. The actual value passed to a parameter is called
an argument.

The combination of parameters and return value is known as the function's signature. A function's signature requires that each parameter must
have its type annotated.

The curly braces enclose the body of the function: its statements and expressions. Even if the function contains no statements or expressions the
curly braces are still required for the function definition.

In the following example the function takes in one parameter of type `i32`, binds it to the name `value`, and prints it.

括号包围零个或多个参数，用逗号分隔。参数是对传递给函数的特定类型的值的绑定。
即使没有参数，函数定义中仍然需要括号。传递给参数的实际值称为实参。

参数和返回值的组合称为函数的签名。函数的签名要求每个参数都必须对其类型进行注释。

花括号包围了函数的主体：它的语句和表达式。即使函数不包含任何语句或表达式，函数定义仍然需要花括号。

在以下示例中，该函数接收一个类型为 `i32` 的参数，将其绑定到名称 `value`，并打印它。

```rust
fn print_integer(value: i32) {
    println!("{:?}", value);
}
```

Note the parameter's definition. Each parameter is defined in the format `name: Type`.

A function can also return a value. By default, the output of the final expression is returned.
In the following example the function has one `i32` parameter and returns its double.

注意参数的定义。每个参数都以`名称：类型`的格式定义。

函数也可以返回一个值。默认情况下，返回最终表达式的输出。
在以下示例中，该函数有一个 `i32` 类型的参数并返回其二倍。

```rust
fn double_integer(value: i32) -> i32 {
    value * 2
}
```

The `-> i32` indicates that the function returns an `i32`. Unlike parameters, the returned value is not named.

It is possible to exit from a function early with the `return` keyword, like so:

`-> i32` 表示该函数返回一个 `i32`。与参数不同，返回值没有命名。

可以使用 `return` 关键字提前退出函数，如下所示：

```rust
fn long_function() -> i32 {
    let some_condition = false;
    // code snipped
    if (some_condition) {
        return 0;
    }
    // more code snipped
    42
}
```

`const fn` is used to define a [constant function][constant function], which can be evaluated at compile time.

`const fn` 用于定义一个 [常量函数][常量函数]，可以在编译时计算。

```rust
const fn compute_data_checksum() -> u128 {
  const DATA: &[u8] = include_bytes!("my_big_data_file");
  // checksum implementation is left as an exercise for the reader
}

/// This checksum is used to validate that the user has not tampered with proprietary configuration.
pub const DATA_CHECKSUM: u128 = compute_data_checksum();
```

Because constant functions may be evaluated at compile time, they have some restrictions that normal functions do not.
In particular, a `const fn` can only call other functions also marked as `const`. Failure to abide by that restriction will result in a
compile error.

因为常量函数可以在编译时求值，所以它们有一些普通函数没有的限制。
特别是，`常量函数` 只能调用也标记为 `const` 的其他函数。不遵守该限制将导致编译错误。

```rust
const fn multiply_integer(value: i32) -> i32 {
    use std::time::SystemTime;
    if SystemTime::now().elapsed().unwrap().as_nanos() == 0 { // this line errors
        value * 2
    } else {
        value * 3
    }
}
```

There are anonymous functions which are covered in the `closures` topic.

`closures` (`闭包`)主题中涵盖了一些匿名函数。

[statements or expressions]: https://doc.rust-lang.org/book/ch03-03-how-functions-work.html#function-bodies-contain-statements-and-expressions
[return value]: https://doc.rust-lang.org/book/ch03-03-how-functions-work.html#functions-with-return-values
[snake case]: https://en.wikipedia.org/wiki/Snake_case
[constant function]: https://doc.rust-lang.org/reference/const_eval.html#const-functions
[语句或表达式]: https://doc.rust-lang.org/book/ch03-03-how-functions-work.html#function-bodies-contain-statements-and-expressions
[返回值]: https://doc.rust-lang.org/book/ch03-03-how-functions-work.html#functions-with-return-values
[蛇形命名法]: https://en.wikipedia.org/wiki/Snake_case
[常量函数]: https://doc.rust-lang.org/reference/const_eval.html#const-functions
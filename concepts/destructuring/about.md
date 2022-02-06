# Destructuring

Destructuring is the process of breaking down items into their component parts, binding each to smaller variables.

解构是将项目分解为其组成部分的过程，将每个部分绑定到较小的变量。

## Destructuring Tuples

Destructuring tuples is simple: just assign new variable names to each field of the tuple:

解构元组很简单：只需为元组的每个字段分配新的变量名：

```rust
let (first, second) = (1, 2);
```

## Destructuring Tuple Structs

Destructuring tuple structs is identical to destructuring tuples, but with the struct name added:

解构元组结构体与解构元组相同，但添加了结构体名称：

```rust
struct (&'static str, i32);
let my_tuple_struct = TupleStruct("foo", 123);
let TupleStruct(foo, num) = my_tuple_struct;TupleStruct
```

## Destructuring Structs

Destructuring structs is similar to destructuring tuple structs. Just use the field names:

解构结构体类似于解构元组结构体。 只需使用字段名称：

```rust
struct ArabianNights {
    name: String,
    stories: usize,
}
let teller = ArabianNights { name: "Scheherazade".into(), stories: 1001 };
{
    let ArabianNights { name, stories } = teller;
    println!("{} told {} stories", name, stories);
}
```

## Partial Destructuring

The `..` operator can be used to ignore some fields when destructuring:

`..` 运算符可用于在解构时忽略某些字段：

```rust
let ArabianNights { name, .. } = teller;
println!("{} survived by her wits", name);
```

## Conditional Destructuring

Destructuring structs and tuples is infallible. However, enums can also be destructured, using the `if let`, `while let`, and `match` language constructs.

解构结构和元组是万无一失的。 然而，枚举也可以被解构，使用 `if let`、`while let` 和 `match` 语言结构。

```rust
if let Some(foo) = foo {
    println!("{:?}", foo);
}
```

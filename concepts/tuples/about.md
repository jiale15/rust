# Tuples

Tuples are a lightweight way to group a fixed set of arbitrary types of data together. A tuple doesn't have
a particular name; naming a data structure turns it into a `struct`. A tuple's fields don't have names;
they are accessed by means of destructuring or by position.

元组是一种将一组固定的任意类型数据组合在一起的轻量级方法。 元组没有
特定名称； 命名数据结构会将其转换为“结构”。 元组的字段没有名称；
它们是通过解构或位置访问的。

## Syntax

Tuples are a list of fields surrounded by parentheses:

元组是用括号括起来的字段列表：

- `()` is the `unit type`, which is a [special case](https://doc.rust-lang.org/std/primitive.unit.html)
- **(** _expression_ **,)** is a single-element tuple expression
- **(** _Type_ **,)** is a single-element tuple type
- **(** _expression_ **,** ... **)** is a general tuple expression
- **(** _Type_ **,** ... **)** is a general tuple type

- `()` 是`unit type`，是一个[特例](https://doc.rust-lang.org/std/primitive.unit.html)
- **(** 表达式 **,)** 是一个单元素元组表达式
- **(** 类型 **,)** 是单元素元组类型
- **(** 表达式 **,** ... **)** 是一个通用元组表达式
- **(** 类型 **,** ... **)** 是一个通用的元组类型

### Creation

Tuples are always created with a tuple expression:

元组总是用元组表达式创建的：

```rust
// pointless but legal 无意义但是合法
let unit = ();
// single element 一个元素
let single_element = ("note the comma",);
// two element 两个元素
let two_element = (123, "elements can be of differing types");
```

Tuples can have an arbitrary number of elements.

### Access by destructuring

It is possible to access the elements of a tuple by destructuring. This just means assigning variable
names to the individual elements of the tuple, consuming it.

可以通过解构访问元组的元素。 这只是意味着将变量名称分配给元组的各个元素并使用它。

```rust
let (elem1, _elem2) = two_element;
assert_eq!(elem1, 123);
```

### Access by position

It is also possible to access the elements of a tuple by numeric positional index. Indexing, as always,
begins at 0.

也可以通过数字位置索引访问元组的元素。 索引一如既往的从 0 开始。

```rust
let notation = single_element.0;
assert_eq!(notation, "note the comma");
```

## Tuple Structs

You will also be asked to work with tuple structs. Like normal structs, these are named types; unlike
normal structs, they have anonymous fields. Their syntax is very similar to normal tuple syntax. It is
legal to use both destructuring and positional access.

您还将被要求使用元组结构体。 和普通结构体一样的是，这些都是命名类型； 和普通结构体不同的是，它们有匿名字段。 它们的语法与普通的元组语法非常相似。 它是合法地使用解构和位置访问。

```rust
struct TupleStruct(u8, i32);
let my_tuple_struct = TupleStruct(123, -321);
let borrowed_neg = &my_tuple_struct.1;
let TupleStruct(borrowed_byte, _) = &my_tuple_struct;
assert_eq!(borrowed_neg, &-321);
assert_eq!(borrowed_byte, &123);
```

### Field Visibility

All fields of anonymous tuples are always public. However, fields of tuple structs have individual
visibility which defaults to private, just like fields of standard structs. You can make the fields
public with the `pub` modifier, just as in a standard struct.

匿名元组的所有字段始终是公开的。 但是，元组结构体的字段具有单独的可见性，默认为私有，就像标准结构体的字段一样。 您可以使用 `pub` 修饰符将字段公开，就像在标准结构体中一样。

```rust
// fails due to private fields 因为是私有字段没所以阿黑白
mod tuple { pub struct TupleStruct(u8, i32); }
fn main() { let _my_tuple_struct = tuple::TupleStruct(123, -321); }
```

```rust
// succeeds: fields are public 成功：字段是公开的
mod tuple { pub struct TupleStruct(pub u8, pub i32); }
fn main() { let _my_tuple_struct = tuple::TupleStruct(123, -321); }
```

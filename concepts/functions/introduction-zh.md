# Introduction

Sometimes a certain piece of code needs to be used more than once. If that's the case, it might be convenient to put the code into a function. A function generally only performs one specific action. In Rust, the ```fn``` keyword is used to define functions. The code belonging to the function is always between brackets. The function named `main` is special because it is the entry point for programs. From that function you can call other functions.

有时某段代码需要多次使用。如果是这种情况，将代码放入函数中可能会很方便。一个函数通常只执行一个特定的动作。在 Rust 中，```fn``` 关键字用于定义函数。属于函数的代码总是在括号之间。名为 `main` 的函数很特别，因为它是程序的入口点。您可以从该函数调用其他函数。
```rust
fn say_my_name(name: &str) -> &str {
    name
}
```

Functions can also take parameters, like ```name: &str``` in ```say_my_name()```. Functions can also return values, like `-> &str` above.
函数也可以接受参数，例如 ```say_my_name()``` 中的 ```name: &str```。函数也可以返回值，例如上面的 `-> &str`。
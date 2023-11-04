# 第二周作业
在Rust语言中，所有权（ownership）、不可变引用（immutable references）、可变引用（mutable references）是其最核心的特性之一，用于确保内存安全和避免数据竞争。下面是它们的总结及相关的代码示例：

## 所有权

首先，让我们看一下所有权的规则。当我们通过举例说明时，请谨记这些规则：
- Rust 中的每一个值都有一个 所有者（owner）。
- 值在任一时刻有且只有一个所有者。
- 当所有者（变量）离开作用域，这个值将被丢弃。

```rust
fn main() {
    let s = String::from("Hello, Rust!"); // s拥有String类型的所有权
	println!("{ }" , s)
	
    // 当s离开作用域时，相关的String值将会被销毁
} // 这里s离开了作用域，String的所有权被销毁
```

### 2. 不可变引用（Immutable References）：
- 允许多个引用指向同一内存位置。
- 不可变引用不允许修改所引用的值。

```rust
fn main() {
    let s = String::from("Hello, Rust!");

    let len = calculate_length(&s); // &s 是对s的不可变引用
    println!("Length of '{}' is {}.", s, len);
}

fn calculate_length(s: &String) -> usize { // s是String的不可变引用
    s.len() // 不可变引用允许调用只读方法
} // 这里s离开了作用域，但因为是不可变引用，所以不影响s的所有权
```

### 3. 可变引用（Mutable References）：
- 允许一个可变引用存在的同时，没有其他引用。
- 可变引用允许修改所引用的值，但在特定作用域中只能有一个可变引用。

```rust
fn main() {
    let mut s = String::from("Hello, Rust!"); // 使用mut关键字创建可变变量

    change_string(&mut s); // &mut s 是对s的可变引用
    println!("Modified string: {}", s);
}

fn change_string(s: &mut String) {
    s.push_str(", World!"); // 可变引用允许修改所引用的值
} // 这里s离开了作用域，但因为是可变引用，所以不影响s的所有权

```

以上示例中，不可变引用和可变引用的使用遵循Rust的借用规则，确保了在编译时避免了数据竞争和内存安全问题。

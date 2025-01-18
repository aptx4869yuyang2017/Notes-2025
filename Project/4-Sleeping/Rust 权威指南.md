---
up: 
related: 
created: 2024-03-03
tags:
  - domain/code
type: "[[Course]]"
finished:
---
- Rust
	- [Rust 程序设计语言 简体中文版](https://kaisery.github.io/trpl-zh-cn/ch02-00-guessing-game-tutorial.html)
	- [Rust语言/Rust权威指南配套](https://www.bilibili.com/video/BV1hp4y1k7SV/?spm_id_from=333.337.search-card.all.click&vd_source=6d4ef5f8b8b73d69ea854cb9321a50ac)


- [x] CH03 基础类型与流程控制 24-03-09
- [x] CH04 所有权 24-03-09
- [x] CH05 Struct  使用结构体组织相关联的数据 24-03-10
- [x] CH06 枚举和模式匹配 24-03-10
- [x] CH07 包 Crate 模块 管理项目 24-03-10
- [x] CH08 集合 24-03-10


# CH03-编程概念

### 3.1变量与可变性


**隐藏**
- 隐藏可以改变数据类型
- 会收到作用域影响


### 3.2数据类型

原生复合类型

- 元组 tuple
- 数组 array

### 3.3 函数

**没有分号的是返回值**

### 3.4 控制流

#### 条件控制



#### 循环

- loop
	- 多层循环 使用循环标签语法 `'counting_up: loop { break 'counting_up}`
- while
- for 循环

# CH04 - 所有权


## 所有权

- **所有权的主要目的就是管理堆数据**
- 内存分配与释放
	- 回收过早，变量变得无效
	- 重复回收，触发bug


### 移动

```rust
    let s1 = String::from("hello");
    let s2 = s1;

    println!("{}, world!", s1);

```

### 克隆

```rust
    let s1 = String::from("hello");
    let s2 = s1.clone();

    println!("s1 = {}, s2 = {}", s1, s2);

```


### 函数

- 普通函数会获取变量的所有权

### 借用

- 引用& 
- 创建引用的行为叫做借用 borrowing

### 可变引用

- **不能对可变变量创建多个可变引用**
	- 可以通过增加作用域来分割
- 不能同时创建比**可变引用**与**不可变引用**

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

### 悬垂引用 Dangling Reference

编译阶段会检查悬垂引用

```rust
fn dangle() -> &String { // dangle 返回一个字符串的引用

    let s = String::from("hello"); // s 是一个新字符串

    &s // 返回字符串 s 的引用
} // 这里 s 离开作用域并被丢弃。其内存被释放。
  // 危险！
```


## Slice 切片

- 引用集合中的一段连续的元素序列
- 是引用 没有所有权

```rust
    let s = String::from("hello world");

    let hello = &s[0..5];
    let world = &s[6..11];

```





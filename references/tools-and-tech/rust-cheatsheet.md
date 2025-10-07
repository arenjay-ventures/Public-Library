---
layout: default
title: Rust Cheatsheet
parent: Tools & Technology
grand_parent: References
nav_order: 9
---

# Rust Cheatsheet

## **What is Rust?**

Rust is a systems programming language that focuses on safety, speed, and concurrency. It's essential for:
- **Systems Programming**: Operating systems, embedded systems
- **Web Assembly**: High-performance web applications
- **Blockchain**: Cryptocurrency and smart contracts
- **Game Development**: High-performance game engines
- **Career Growth**: Growing demand for Rust developers

## **Installation & Setup**

### **Install Rust**
```bash
# Install Rust (all platforms)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Verify installation
rustc --version
cargo --version

# Update Rust
rustup update
```

### **Cargo (Package Manager)**
```bash
# Create new project
cargo new my_project
cargo new --lib my_library

# Build project
cargo build
cargo build --release

# Run project
cargo run

# Test project
cargo test

# Check code
cargo check
```

## **Basic Syntax**

### **Variables & Mutability**
```rust
// Immutable by default
let x = 5;
let name = "John";

// Mutable variables
let mut y = 10;
y = 20;

// Constants
const MAX_POINTS: u32 = 100_000;

// Shadowing
let x = 5;
let x = x + 1;  // x is now 6
let x = "hello"; // x is now a string
```

### **Data Types**
```rust
// Integers
let a: i32 = 42;        // 32-bit signed integer
let b: u64 = 100;       // 64-bit unsigned integer

// Floating point
let c: f64 = 3.14;      // 64-bit float

// Boolean
let flag: bool = true;

// Character
let letter: char = 'A';

// String types
let s: &str = "hello";           // String slice
let owned: String = String::from("world"); // Owned string
```

### **Functions**
```rust
// Basic function
fn add(a: i32, b: i32) -> i32 {
    a + b
}

// Function with multiple statements
fn greet(name: &str) {
    println!("Hello, {}!", name);
}

// Function with early return
fn divide(a: f64, b: f64) -> Option<f64> {
    if b == 0.0 {
        None
    } else {
        Some(a / b)
    }
}
```

## **Control Flow**

### **Conditional Statements**
```rust
let number = 6;

if number % 4 == 0 {
    println!("number is divisible by 4");
} else if number % 3 == 0 {
    println!("number is divisible by 3");
} else {
    println!("number is not divisible by 4 or 3");
}

// If as expression
let condition = true;
let number = if condition { 5 } else { 6 };
```

### **Loops**
```rust
// Loop
let mut counter = 0;
loop {
    counter += 1;
    if counter == 10 {
        break;
    }
}

// While loop
let mut number = 3;
while number != 0 {
    println!("{}!", number);
    number -= 1;
}

// For loop
for i in 1..4 {
    println!("{}", i);
}

// For loop with iterator
let a = [10, 20, 30, 40, 50];
for element in a.iter() {
    println!("the value is: {}", element);
}
```

## **Ownership & Borrowing**

### **Ownership Rules**
```rust
// Each value has an owner
let s1 = String::from("hello");
let s2 = s1; // s1 is moved to s2, s1 is no longer valid

// Clone for deep copy
let s1 = String::from("hello");
let s2 = s1.clone(); // s1 is still valid

// Ownership transfer
fn take_ownership(s: String) {
    println!("{}", s);
} // s goes out of scope and is dropped

let s = String::from("hello");
take_ownership(s); // s is moved into the function
```

### **Borrowing**
```rust
// Immutable borrow
fn calculate_length(s: &String) -> usize {
    s.len()
} // s goes out of scope, but doesn't drop the value

let s1 = String::from("hello");
let len = calculate_length(&s1);
println!("The length of '{}' is {}.", s1, len);

// Mutable borrow
fn change(s: &mut String) {
    s.push_str(", world");
}

let mut s = String::from("hello");
change(&mut s);
println!("{}", s);
```

### **References**
```rust
// Immutable references
let s1 = String::from("hello");
let len = calculate_length(&s1);

// Mutable references
let mut s = String::from("hello");
let r1 = &mut s;
// let r2 = &mut s; // Error: can't have multiple mutable references

// Dangling references (prevented by compiler)
// fn dangle() -> &String {
//     let s = String::from("hello");
//     &s // Error: s goes out of scope
// }
```

## **Structs & Enums**

### **Structs**
```rust
// Define struct
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}

// Create instance
let user1 = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
    active: true,
    sign_in_count: 1,
};

// Access fields
println!("{}", user1.email);

// Mutable struct
let mut user1 = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
    active: true,
    sign_in_count: 1,
};
user1.email = String::from("anotheremail@example.com");
```

### **Methods**
```rust
impl User {
    // Associated function (like static method)
    fn new(username: String, email: String) -> User {
        User {
            username,
            email,
            sign_in_count: 1,
            active: true,
        }
    }
    
    // Method
    fn greet(&self) {
        println!("Hello, {}!", self.username);
    }
    
    // Mutable method
    fn increment_sign_in(&mut self) {
        self.sign_in_count += 1;
    }
}

// Usage
let mut user = User::new(String::from("john"), String::from("john@example.com"));
user.greet();
user.increment_sign_in();
```

### **Enums**
```rust
// Define enum
enum IpAddrKind {
    V4,
    V6,
}

// Enum with data
enum IpAddr {
    V4(String),
    V6(String),
}

// Usage
let home = IpAddr::V4(String::from("127.0.0.1"));
let loopback = IpAddr::V6(String::from("::1"));

// Option enum (built-in)
let some_number = Some(5);
let some_string = Some("a string");
let absent_number: Option<i32> = None;
```

## **Pattern Matching**

### **Match Statements**
```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}

// Match with data
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

fn process_message(msg: Message) {
    match msg {
        Message::Quit => println!("Quit"),
        Message::Move { x, y } => println!("Move to ({}, {})", x, y),
        Message::Write(text) => println!("Write: {}", text),
        Message::ChangeColor(r, g, b) => println!("Change color to RGB({}, {}, {})", r, g, b),
    }
}
```

### **If Let**
```rust
let some_value = Some(3);

match some_value {
    Some(3) => println!("three"),
    _ => (),
}

// Equivalent with if let
if let Some(3) = some_value {
    println!("three");
}
```

## **Error Handling**

### **Result Type**
```rust
use std::fs::File;
use std::io::ErrorKind;

fn open_file(filename: &str) -> Result<File, std::io::Error> {
    let f = File::open(filename);
    
    match f {
        Ok(file) => Ok(file),
        Err(error) => match error.kind() {
            ErrorKind::NotFound => match File::create(filename) {
                Ok(fc) => Ok(fc),
                Err(e) => Err(e),
            },
            other_error => Err(other_error),
        },
    }
}

// Using ? operator
fn read_username_from_file() -> Result<String, std::io::Error> {
    let mut f = File::open("hello.txt")?;
    let mut s = String::new();
    f.read_to_string(&mut s)?;
    Ok(s)
}
```

### **Panic**
```rust
// Panic macro
panic!("crash and burn");

// Unwrap (panics on error)
let f = File::open("hello.txt").unwrap();

// Expect (panics with custom message)
let f = File::open("hello.txt").expect("Failed to open hello.txt");
```

## **Collections**

### **Vectors**
```rust
// Create vector
let v: Vec<i32> = Vec::new();
let v = vec![1, 2, 3];

// Add elements
let mut v = Vec::new();
v.push(5);
v.push(6);
v.push(7);

// Access elements
let third: &i32 = &v[2];
let third: Option<&i32> = v.get(2);

// Iterate
for i in &v {
    println!("{}", i);
}

// Mutable iteration
for i in &mut v {
    *i += 50;
}
```

### **Strings**
```rust
// String creation
let mut s = String::new();
let s = String::from("initial contents");

// String operations
let mut s = String::from("foo");
s.push_str("bar");
s.push('l');

// String concatenation
let s1 = String::from("Hello, ");
let s2 = String::from("world!");
let s3 = s1 + &s2; // s1 is moved here

// Format macro
let s1 = String::from("tic");
let s2 = String::from("tac");
let s3 = String::from("toe");
let s = format!("{}-{}-{}", s1, s2, s3);
```

### **Hash Maps**
```rust
use std::collections::HashMap;

// Create hash map
let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

// Access values
let team_name = String::from("Blue");
let score = scores.get(&team_name);

// Iterate
for (key, value) in &scores {
    println!("{}: {}", key, value);
}

// Update values
scores.insert(String::from("Blue"), 25); // Overwrite
scores.entry(String::from("Yellow")).or_insert(50); // Insert if not exists
```

## **Modules & Packages**

### **Modules**
```rust
// Define module
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

// Use module
use front_of_house::hosting;
hosting::add_to_waitlist();

// Re-export
pub use front_of_house::hosting;
```

### **Cargo.toml**
```toml
[package]
name = "my_project"
version = "0.1.0"
edition = "2021"

[dependencies]
serde = "1.0"
tokio = { version = "1.0", features = ["full"] }
```

## **Concurrency**

### **Threads**
```rust
use std::thread;
use std::time::Duration;

let handle = thread::spawn(|| {
    for i in 1..10 {
        println!("hi number {} from the spawned thread!", i);
        thread::sleep(Duration::from_millis(1));
    }
});

for i in 1..5 {
    println!("hi number {} from the main thread!", i);
    thread::sleep(Duration::from_millis(1));
}

handle.join().unwrap();
```

### **Channels**
```rust
use std::sync::mpsc;
use std::thread;

let (tx, rx) = mpsc::channel();

thread::spawn(move || {
    let val = String::from("hi");
    tx.send(val).unwrap();
});

let received = rx.recv().unwrap();
println!("Got: {}", received);
```

## **Testing**

### **Unit Tests**
```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn it_works() {
        assert_eq!(2 + 2, 4);
    }

    #[test]
    fn larger_can_hold_smaller() {
        let larger = Rectangle { width: 8, height: 7 };
        let smaller = Rectangle { width: 5, height: 1 };
        assert!(larger.can_hold(&smaller));
    }
}
```

### **Running Tests**
```bash
# Run all tests
cargo test

# Run specific test
cargo test it_works

# Run tests with output
cargo test -- --nocapture
```

## **Learning Resources**

### **Documentation**
- **[Rust Book](https://doc.rust-lang.org/book/)** - Official comprehensive guide
- **[Rust by Example](https://doc.rust-lang.org/rust-by-example/)** - Learn by example
- **[Rust API Documentation](https://doc.rust-lang.org/std/)** - Standard library docs

### **Tutorials**
- **[Rustlings](https://github.com/rust-lang/rustlings)** - Interactive exercises
- **[Rust Tutorial](https://tutorial.rust-lang.org/)** - Step-by-step tutorial
- **[Rust Cookbook](https://rust-lang-nursery.github.io/rust-cookbook/)** - Common patterns

### **Practice**
- **[Exercism Rust Track](https://exercism.org/tracks/rust)** - Coding exercises
- **[LeetCode Rust](https://leetcode.com/)** - Algorithm problems
- **[Advent of Code](https://adventofcode.com/)** - Annual programming challenges

### **Popular Crates**
- **Tokio**: Async runtime
- **Serde**: Serialization/deserialization
- **Clap**: Command line argument parsing
- **Reqwest**: HTTP client
- **Actix-web**: Web framework
- **Diesel**: ORM
- **Rocket**: Web framework

## **Best Practices**

### **Code Organization**
```rust
// Use modules to organize code
mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}
    }
}

// Use enums for multiple variants
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```

### **Error Handling**
```rust
// Prefer Result over panic
fn divide(a: f64, b: f64) -> Result<f64, String> {
    if b == 0.0 {
        Err(String::from("Cannot divide by zero"))
    } else {
        Ok(a / b)
    }
}

// Use ? operator for error propagation
fn read_file() -> Result<String, std::io::Error> {
    let mut f = File::open("hello.txt")?;
    let mut s = String::new();
    f.read_to_string(&mut s)?;
    Ok(s)
}
```

Remember: **Rust is about safety and performance**. The ownership system prevents many common bugs at compile time. Start with the basics, understand ownership and borrowing, then move to more advanced topics like async programming and unsafe code. The Rust community is welcoming and helpful!
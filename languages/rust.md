# Rust 


Lets get rusty bootcamp 
<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Rust](#rust)
- [Beginner](#beginner)
    - [Variables](#variables)
        - [Mutatbility](#mutatbility)
    - [Data types](#data-types)
    - [Const and Static](#const-and-static)
    - [Functions](#functions)
    - [Control flow](#control-flow)
    - [Memory](#memory)
        - [ownership](#ownership)
        - [borrowing](#borrowing)
        - [slices](#slices)
    - [Custom Data Types](#custom-data-types)
        - [Structs](#structs)
        - [Implementaion blocks](#implementaion-blocks)
        - [Tuple structs](#tuple-structs)
        - [Enumns](#enumns)
        - [Matching](#matching)
        - [Option](#option)
        - [Result](#result)
        - [Vectors](#vectors)
    - [Projects](#projects)
        - [Structure](#structure)
        - [modules](#modules)
        - [External dependencies](#external-dependencies)
        - [publishing your package](#publishing-your-package)
    - [Structuring larger projects](#structuring-larger-projects)
        - [Cargo features](#cargo-features)
        - [Cargo Workspaces](#cargo-workspaces)
    - [Testing and documentation](#testing-and-documentation)
        - [Unit Tests](#unit-tests)
        - [Integration test](#integration-test)
        - [Documentation](#documentation)
        - [Benchmark Testing](#benchmark-testing)
- [Intermediate](#intermediate)
    - [Generics and traits](#generics-and-traits)
        - [Generics](#generics)
        - [Traits](#traits)
        - [Trait Bounds](#trait-bounds)
        - [Supertraits](#supertraits)
        - [Trait Objects](#trait-objects)
        - [Deriving Traits](#deriving-traits)
        - [The Orphan Rule](#the-orphan-rule)
        - [Traits in the standard library](#traits-in-the-standard-library)
    - [Advanced memory management](#advanced-memory-management)
        - [Concrete Lifetimes](#concrete-lifetimes)
        - [Generic Lifetimes](#generic-lifetimes)
        - [Structs and Lifetime Elision](#structs-and-lifetime-elision)
        - [Box smart pointer](#box-smart-pointer)
        - [`Rc` smart pointer](#rc-smart-pointer)
        - [RefCel Smart pointer](#refcel-smart-pointer)
        - [Deref coercion](#deref-coercion)
    - [Error handling](#error-handling)
        - [Unrecoverable Errors](#unrecoverable-errors)
        - [Recoverable Errors](#recoverable-errors)
        - [Propograting Errors](#propograting-errors)
        - [Result and Option](#result-and-option)
        - [Multiple Error Types](#multiple-error-types)
        - [anyhow and thiserror](#anyhow-and-thiserror)
    - [Advanced Error Handling](#advanced-error-handling)
        - [Basics](#basics)
        - [Custom Errors](#custom-errors)
        - [thiserror and anyhow](#thiserror-and-anyhow)
    - [Functional Features](#functional-features)
        - [Closures](#closures)
        - [function pointers](#function-pointers)
        - [Iterator Pattern](#iterator-pattern)
        - [Combinators](#combinators)
    - [Concurrency and async/.await](#concurrency-and-asyncawait)
        - [Intro to concerrency](#intro-to-concerrency)
        - [Creating threads](#creating-threads)
        - [Moving values into threads](#moving-values-into-threads)
        - [Message passing between threads](#message-passing-between-threads)
        - [Sharing state between threads](#sharing-state-between-threads)
        - [Send & Sync Traits](#send--sync-traits)
        - [async/.await basics](#asyncawait-basics)
        - [Tokio tasks](#tokio-tasks)
        - [CPU Intensive code](#cpu-intensive-code)
        - [Streams](#streams)
    - [Macro System](#macro-system)
        - [Intro](#intro)
        - [Declarative Macros](#declarative-macros)
        - [Procedural macro](#procedural-macro)
        - [Function like](#function-like)
        - [Custom Derive](#custom-derive)
        - [Atrribute like](#atrribute-like)
    - [Unsafe Rust and FFI](#unsafe-rust-and-ffi)
        - [Unsafe basics](#unsafe-basics)
        - [1. Dereference raw pointer](#1-dereference-raw-pointer)

<!-- markdown-toc end -->

# Beginner 
## Variables

* rust infers type but type can be specified with `:<type> = `

### Mutatbility 
* Varaibles are immutable by  default 
* they can be shadowed by creating another variable with the same name. 

## Data types 
* String types 
   * `&str` string slice 
   * `String` dyanmic string 
* arrays 
  * `a[<type>, <size>]`
* tuples can be off all sorts of types and can be destructured


## Const and Static 
* `const MAX_PLAYERS: u8 = 10` 
* can never be mutated 
* screeming snake case 
* can be declared in every scope 
* value has to be computed at compile time 

* `static CASINO_NAME: &str = "Casino"`
* can be marked mutable 

* constants do not occupy a specific place in memory
* default to using constants

## Functions 
* naming convention: snake_case 

## Control flow

* can use single line statements 
  ` let b: i32 = if a > 5 { 1 } else { -1 }`
  
* labeling loops 
  ```rust
  `outer: loop {
      loop {
      break `outer;
      }
  }
  ```
  
## Memory 

### ownership
* Each value is owned by a binding 
* There can ony be one owner at a time 
* when the owner goes out of scope, the value will be dropped

These three rules are checked at compile time to make sure that the program is memory safe.

* values are moved by default (can only have one owner)
* cloning values?
`val.clone()`=> does not move the value 

* primitives that are stored on the stack are cloned by defualt this is because they are stored entirely on the stack so the operation to clone them is cheap 

* passing a variable to a function is the same as moving it 

### borrowing 
* The act of creating a reference
* references are pointers with rules/restrictions 

Why borrow? 
* performance --> types that take up a lot of memory 

Rules
* one mutable ref or any # of immutable refs 
* refs must always be valid 

* think about when something (a function or statement) needs ownership of the values passed in


### slices
* ref to contiguous seq of elements in a collection 
`let trimmed_str: &str = &string[..30]`



## Custom Data Types

### Structs
```rust
struct Product {
    name: String, 
    price: f32, 
    in_stock: bool
}
```

### Implementaion blocks 
implement functionality for a given type 

```rust
impl <Type> {
    fn (&self) {
        ...
    }
}
```
can take ownership of the instance and drop after function 
```rust
impl Product {
    fn buy(self){
        ...
    } // Product instance is dropped here
}
```

Associative methods (static)
```rust
impl Product {
    fn name(){
       ... 
    }
}

Product::name();

```
There is only one true constructure so you can use a `::new` method to implement some defaults

### Tuple structs
eg
```rust
struct RGB(i32, i32, i32);
```
 
### Enumns
```rust
struct Product {
    category: ProductCategory
    ...
}

enum ProductCategory {
    Books, 
    Clothing,
    Electronics
}

let category = ProductCategory::Books;

```

```rust
enum Command {
    AddText(String),
    MoveCursor(i32, i32),
    Replace {
        from: String, 
        to: String
    }
}
```

can also add `impl` blocks to enums 

### Matching
* expressions are exhaustive so we have to handle every case in the expression 

### Option 
```rust
emum Option<T> {
    None,
    Some(T)
}
```
return `Some(T)` or `None`

### Result
* Similar to options but for function execution

```rust
emun Result<T, E> {
    Ok(T),
    Error(E)
}
```

`result.ok()` turns a result into an option

### Vectors
* growable
* allocate memory on the heap 
```rust
let v: Vec<String> = Vec::new();
//or 
let mut v = Vec::new();
v.push(String::from("one"))

//or 

let v3 = vec![1, 2, 3];

```
* vector has ownership of the elements 
* cannot move element out of vector because then the index is pointing at invalid memory 
  * can be removed with `v.remove()`
* `v.get(index)` returns and Option
* Iterating 
  ```rust
  for s in &mut v {
      s.push_str("!")
  }
  ```
  
## Projects
### Structure
* Packages
  * Contain one or more crates
  * must have one crate 
  
* Crates
  * produces library or executable
* Modules
  * control organization and scope 
  
* `cargo new` --> creates new pkg
* `main.rs` -> root of bin crate 
* `lib.rs` -> root or lib crate 

* create `src/bin` to make more binary crates 

### modules 
Organize code for readability and scope 

* explicitly defined with mod keyword 


`cargo install cargo-modules`
`cargo modules generate tree`
`cargo modules generate tree --with-types`


```rust
mod database {
    ...
}
```

* use brings items into scope 

Defining modules in other files 

1. `mod filename;` 
   - must be declared within the parent module
   - will automatically look for for file with the name of the module 
2. Sub modules 
   - define folder with name of module. 
   - `mod.rs` is similar to an index file 
   - rust will look for the mod file inside the module_name directory 
   
   











### External dependencies
* adding a dependency
  * add to `cargo.toml`
  `use rand::prelude::*;`

### publishing your package
* generate token from crates.io 
`cargo login <token>`

`cargo publish`
* must commit changes to git first 
* must have description and license in `cargo.toml`


## Structuring larger projects
### Cargo features 
1. Parts of code conditionally compiled 
   - add `features` section in `cargo.toml` 
2. Include code at compile time 
   - `#[cfg(feature = "color")]`
   - only adds code if the features are turned on
   
Using features 
* in `cargo.toml` -> `default-features: false, features = ["feature-name"]`

### Cargo Workspaces 
* similar to yarn workspaces
* share a cargo toml 
* multiple related packages 
* monolithic packages 
  - e.g. blog site with API, front-end, and shared code 
* in `cargo.toml`
  ```rust
  // virtual manifest
  [workspace]
  
  members = [
      'blog_api',
      ...
  ]
  ```
  use `cargo new --vcs none pkg_name` to make sure no git directory is added

* target a specific package with `-p`
* add the local dependencies to the package cargo.toml 


## Testing and documentation 
### Unit Tests
* ` cargo test` 
* create a mod named tests that holds all the testing code 
  ```rust
  #[cfg(test)]
  mod tests {
      // all parent mods
      use super::*;
      
      #[test]
      fn should_do_something() {
        let account = SavingsAccount::new();
        assert_eq!(account.get_balance(), 0)
      }
      
      
  }
  ```

* `assert_ne!`
* `assert!`

will panic on failed assertion

tests that return Result 
```rust
#[test]
fn should_transfer_money() -> Result<(), String> {
    ...
    Ok(())
}
```

```rust
#[test]
#[should_panic]
fn should_panic() {
   ... 
}
```

* convention is to have the tests module with the source code.
  - inline or seperate file

### Integration test 
* public interface 
* stored in top level dir in `/tests`
* each file will be compiled as a seperate crate for isolation
* hard to share code 
 - every file is treated as a test 
 - use a mod in `utils/mod.rs`--> not a top level file in the tests dir 
 
* integration tests cannot import functionality from binary crates

### Documentation 
* Doc comments 
```rust
/// Doc comment
/// # written in markdown
```
 - cargo will execute code blocks in doc comments as tests 
 
 - `cargo doc --open` opens the package docs in a webapage
 
### Benchmark Testing 
TODO: add notes after learning larger concepts


# Intermediate 

## Generics and traits

### Generics
```
struct BrowserCommand {
    name: String, 
    payload: String,
}
// if we want to make this more generic... 

struct BrowserCommand<T>{
    name: String,
    payload: T,
}
```

Impl Blocks 
```rust
impl<T> BrowserCommand<T> {

    fn new(name: String, payload: T) -> Self {
        BrowserCommand {
            name,
            payload
        }
    }
}
```
* This makes the impl block for the generic type

Impl block for a concrete type 

```rust
impl BrowserCommand<String> {
    fn print_payload(&self) {
        println!("{}", self.payload)
    }
}
```

Method that returns a Generic 
```rust
fn get_payload(&self) -> &T {
    &self.payload
}
```
* no runtime performance cost 
* creates concrete functions, structs, and impl blocks at compile time and updates the call sites to call the concrete versions

### Traits
Rust does not support classical inheritance. Instead, traits are use. 

Only functionality can be shared with traits

```rust
// needs to be implemented by an impl block
trait Park {
    // can have body for a default implementation
    fn park(&self);
}

impl Park for Car {
    fn park(&self) {
    
    }
}
```

### Trait Bounds
1. `fn paint_red<T: Paint>(object: &T){}`
2. `fn paint_red(object: &impl Paint)`
3. `fn paint_red<T>(object: &T) where T: Paint {}`

Can also be used in returns 
```rust
//only if returning one concrete type
fn create_paint_object() -> impl Paint() {}
```

### Supertraits
Traits can rely on other traits. Traits relied on are called supertraits. 

```rust
trait Vehicle: Paint  + Park {
    fn park(&self);
}
```
### Trait Objects
Generic must be substituted with one concrete type at compile time. 

Eg: `Box<dyn Pain>`
use "box smart pointer" and dynamic dispatch 
**dynamic dispatch** - concrete methods are not known at compile time but figured out at runtime. Runtime performance cost. 


### Deriving Traits 

```rust
#[derive(Debug)]
struct Point{}
```
Partial equality
```rust
#[derive(Debug, PartialEq)]
struct Point{}
```

### The Orphan Rule
In order to implement a trait on a type, trait or type needs to be defined in the scope. 

Can create a wrapper type:
```rust
struct PointWrapper(Point);

impl PartialEq for PointWrapper {
    fn eq(...)
}
```

### Traits in the standard library
TODO: Add notes when video comes out


## Advanced memory management
### Concrete Lifetimes
* borrow checker checks the lifetime of values 
* lifetime starts when a value is created or moved 
* lifetime ends when the value gets dropped 

* checks that a reference does not outlive it's borrow 
* "non-lexical" lifetimes are not defined by scope and are inferred by the compiler

### Generic Lifetimes 
* the borrow checker needs to be able to determine the lifetimes of every value so that 
* describe the relationship between concrete lifetimes

failing code
```rust
fn first_turn(p1: &str, p2: &str) -> &str {
    if rand::random() {
        p1
    } else {
        p2
    }
}
```
In this example the compiler is unable to determine which reference is going to be returned at compile time. Since p1 and p2 might have different concrete lifetimes. 
We have to turn the code into using generic lifetime `<'a>` 
```rust
fn first_turn<'a>(p1: &'a str, p2: &'a str) -> &'a str {
    if rand::random() {
        p1
    } else {
        p2
    }
}
```
Describes the *relationship* between concrete lifetimes

**takes the shortest lifetime out of the possible concrete lifetimes**
* i.e. if p1 lives for longer than p2 then the return value will have the same lifetime as p2 and vice versa. 
` `static lifetime `
* lives for the entire life of the program 
```rust
let s: &'static str = "Lets get rusty!"
s
```

### Structs and Lifetime Elision
```rust
struct Tweet {
    content: &str;
}
```
Must add a generic lifetime to store references in structs 

```rust
struct Tweet<'a> {
    content: &'a str, 
}

impl<'a> Tweet<'a> {
    fn replace_content(&mut self, content: &'a str) -> &str {
        let old_content = self.content;
        self.content = content;
        old_content
    }
}

```

Lifetime Elision Rules
1. Each parameter that is a ref gets its own lifetime parameter
2. If there is exactly one input lifetime param, that lifetime is asssigned to all output lifetime parameters 
3. (applies to methods) If there are multiple, but one of them is &self or &mut self, the lifetime of self is assigned to all output lifetime params. 

### Box smart pointer
If we want something to be stored on the heap
```rust
let button = Box::new(Button {text: "name".to_owned()})
```
single ownership of something on the heap 

use cases: 
* avoid copying large ammounts of data when transferring ownership 
* similar to getting a heap pointer from `malloc` in C

[SO Thread on malloc and Box smart pointers](https://stackoverflow.com/questions/48485454/rust-manual-memory-management)

Recursive types 

We cannot make a struct with recursive size like 
```rust
struct Container {
    name: String,
    child: Container // won't compile
}
```

we instead have to use *indirection*-> use a reference to the recursive type
```rust
struct Container {
    name: String,
    child: Box<Container>
} 
```


### `Rc` smart pointer 
* Shared ownership 
** NOT** included in the Rust prelude 
```rust
use std::Rc::rc;
```

Pass around RC
```rust
let rc = Rc::new(P{})
Rc::clone(&rc)
```

* When the Reference count gets to 0, the RC pointer will drop the value it is referencing 
* can only be used in single-threaded apps

### RefCel Smart pointer
* Cannot assign to data in Rc smart pointer 
* Must use a RefCell smart pointer 
`borrow_mut()` uses the interior mutability pattern 
* in combination with Rc provides mutability and shared ownership 

Unsafe code!
```rust
let mut r1 = db.borrow_mut();
let r2 = db.borrow_mut();

r1.max_connections = 200; // will panic at runtime 
```

### Deref coercion
* when types do not match 
* rust compiler coerces a val of one type into another
* eg: `&Box -> &String -> &str`
* only works on types that impl `Deref` and `DerefMut` trait. 

```rust
use std::ops::{Deref, DerefMut};

struct MySmartPointer<T> {
    value: T
}

impl<T> MySmartPointer<T> {
    fn new(value: T) -> MySmartPointer<T> {
        MySmartPointer {
            value
        }
    }
}

impl<T> Deref for MySmartPointer<T> {
    type Target = T;
    
    fn deref(&self) -> &Self::Target {
        &self.value
    }
}

impl<T> DerefMut for MySmartPointer<T> {
    type Target = T;
    
    fn deref_mut(&mut self) -> &mut Self::Target {
        &mut self.value
    }
}
```
* should only be implemented on smart pointer types

## Error handling 
### Unrecoverable Errors
* panic causes an error to be printed out and the program to exit abruptly
* `RUST_BACKTRACE=1` allows for debug output

### Recoverable Errors
* Use the Result enum
```rust
let file = File::open("example.txt")

let file = match file {
    Ok(file) => file,
    Err(error) => {
        panic!("Failed to open file {:?}", error)
    }
}
// or for faster 

let file = File::open("example.txt").unwrap();

let file = File::open("example.txt").expect("Failed to open file");
```

### Propograting Errors
* `?` unwraps Ok() and Some() values or propogates the error or None
* This will return early in funtions

### Result and Option
* `and_then` takes a closure (callback fn)
* `ok()` method takes result and turns to option 

### Multiple Error Types 
* Used when functions may return multiple types of errors 
* can use trait object `Box<dyn error::Error>` --> can't handle specific error types
* custom error erum 
    ```rust
    enum ParseFileError {
        File, 
        Parse(ParseIntError)
    }
    ```
    - map using `map_err` method


### anyhow and thiserror
TODO: coming soon!

## Advanced Error Handling

### Basics 
* watch out for `unwrap()` methods!

### Custom Errors
* use enum with variants to differentiate between errors
```rust
enum CreditCardError {
    InvalidInput(String),
    ...
}
```
* `From` trait
 - can use this to convert from one error type to another without using `map_error`

### thiserror and anyhow 
* provides derive macros for error trait 
* reduces the ammount of code you have to write 
* `anyhow` allows context on errors
* 


## Functional Features 
### Closures 
* can store as variables or pass as args

```rust
let validator = |username: &str, password: &str|{
    !username.is_empty() && !password.is_empty()
}
```

* can store closures in stuct 
```rust
struct Example<T> where T: Fn(&str, &str) -> bool{
    ...
    validator: T
}
```
* validators can access binding within the scope it is defined 
* `move` keyword takes ownership of the values references 
* passing into function 
```rust
fn get_default_creds<T>(f: T) -> Credentials<T> where T: Fn(&str, &str) -> bool {
...
}
```
* have to use dynamic dispatch if you are returning two+ closures because no two closures have the same type. 

### function pointers
* dont capture variables in their environment 
* closures can be converted into function pointers if they do not capture any values in their environment. 
* use closures as function arguments!

### Iterator Pattern 
* allows different types to have similar iterating logic 
* any type can implement the iterator trait 
* must implement the `next()` method 

### Combinators
* `.flatten()` combinator will extract from Some and get rid of None
* `.collect()` will turn iterator into collection 
* not called until `next()` is called 
* a zero cost abstraction 

## Concurrency and async/.await

### Intro to concerrency 
* when a process executes, the kernel makes a process for it
* process has it's own heap, and address space 
* each process has one or more threads
* thread -> instructions to execute sequentially 
* Scheduler (part of the OS) takes threads and passes them to the CPU 
* programmer has no control of when the schedule decides to execute 
* concurrency -> parts of the program excuting at the same independently
* Concurrency can be achieved through time-slicing (one core) or parallel execution (multi-core) 
* OS threads and Async tasks are the main ways to achieve concurrency in rust 

### Creating threads
```rs
use std::thread;

fn main() {
    thread::spawn(|| {
        ... new thread
    })

}
``` 
spawn takes a closure that will be executed in the new thread
* as soon as the main thread is finished the program exits, need to wait on the new thread using a join handle

```rust
let handle: JoinHandle<()> ... thread::spawn();




// end of main thrad 

handle.join().unwrap()
```
* developer has little control over how threads are executed. 

### Moving values into threads
* can use the `move` keyword in the closure to take ownership 

### Message passing between threads 
```rust
let (tx, rx) = mpsc::channel();

tx.send().unwrap();
```
* can treat the reciever like an iterator

### Sharing state between threads
* neee to use a mutex *mutual exclusion*
```rust
Mutex::new(..resource..)
```
* must first get a lock 
* locks wil get dropped when out of scope 
* might need to use shared ownership with something like an ARC smart pointer 
```rust
let db = Arc::new(...)
```


### Send & Sync Traits
* a label on types  
* unsafe traits, cannot verify that these properties are enforced 
* Send ->  ownership can be transfered between threads 
* Sync -> reference can be transfered between threads

### async/.await basics 
```rust
fn main() {

}

async fn my_function() {
    println!("THis is async")
}
```
* write async code that looks sync

* async keyword is syntactic sugar for a function that returns something that impl `Future<Output>`
* futures are similar to promises in JS 
* have to be driven to completion (awaited)
* `.await` tries to run the future to completion 
* For top most features, we need a runtime to poll the top level futures and polling them until completion 
* The std library does not provide and async runtime --> the most popular one is `tokio`
```rust
#[tokio::main]
```

### Tokio tasks
* a task is a non-blocking piece of code 
```rust
let mut handles = vec![]

let handle = tokio::spawn()
```
* very similar API to spawning threads 
* don't want to put CPU intensive operations inside an async funtion 

### CPU Intensive code 
* blocks all async functions on that thread 
* can wrap cpu intensive code in `spawn_blocking` which will place it in a seperate thread pool 

### Streams 
* like async iterators 
* a good use case is TCP servers that accept connections as a stream 


## Macro System
### Intro 
* *writing code that writes other code*
* reduce the ammount of code you have to write 
* processed during compile time 
* lexical analysis turns text into tokens that the language understands (identifiers, literals, keywords)
  * then turned into token trees 
* Syntax analysis turns token tree into syntax tree 
* macros are constructed after syntax analysis 
* semantic analysis works after macros has been expanded 
* *after AST is created but before it is validated by sematic analysis*

### Declarative Macros
```rust

// (matches) => {expansion aka transcriber}

#[macro_export]
macro_rules! hello {
    // rule 0
    () => {
        println!("hello world")
    };
}
``` 
* match against the root node of syntax tree
* meta variables
  * format: `$[identifier] : [fragment-specifier]`
```rust
macro_rules! map {
    ($key:ty, $val:ty) => {
        {
            let map: HashMap<$key, $val> = HashMap::new();
            map
        }
    };
    // $( ... ) sep rep
    ($($key:expr => $val:expr ),*) => {
    
    }

}
```
### Procedural macro
* takes token stream as input and returns token stream 
```toml
//Cargo.toml

[lib]
proc-macro = true
```

```rust
extern crate proc_macro;

use proc_macro::{TokenStream};
```
### Function like
```rust
#[proc_macro]
pub fn log_info(input: TokenStream) -> TokenStream {
    input
}
```
```toml
//cargo.toml

[dependencies]
quote 
crono
```

* `quote!` macro turns rust code into TokenStream

### Custom Derive
* automatically implement traits for custom types! 
```rust
#[proc_macro_derive(Trait)]
pub fn log_derive(input: TokenStream) -> TokenStream {
    TokenStream::new()
}
```
`syn` crate parses into syntax tree that is easier to work with

### Atrribute like 
* like adding an attribute to annotate functions
  * `#[log_call(verbose)]`
  * like a decorator


## Unsafe Rust and FFI
### Unsafe basics 
* `unsafe {}` 
1. Dereference a raw pointer 
2. Call an unsafe function 
3. Implement an unsafe trait
4. Access/Modify a mutable static variable
5. Access fields of a union 

### 1. Dereference raw pointer 
`let raw = &mut s as *mut String`--> creating a raw pointer 
```rust
unsafe {
    (*raw)...
}
```
* to achieve greater performance, interface with C, interface with hardware, safe abstractions



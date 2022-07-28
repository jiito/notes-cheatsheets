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
  ```
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
```
struct Product {
    name: String, 
    price: f32, 
    in_stock: bool
}
```

### Implementaion blocks 
implement functionality for a given type 

```
impl <Type> {
    fn (&self) {
        ...
    }
}
```
can take ownership of the instance and drop after function 
```
impl Product {
    fn buy(self){
        ...
    } // Product instance is dropped here
}
```

Associative methods (static)
```
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
```
struct RGB(i32, i32, i32);
```
 
### Enumns
```
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

```
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
```
emum Option<T> {
    None,
    Some(T)
}
```
return `Some(T)` or `None`

### Result
* Similar to options but for function execution

```
emun Result<T, E> {
    Ok(T),
    Error(E)
}
```

`result.ok()` turns a result into an option

### Vectors
* growable
* allocate memory on the heap 
```
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
  ```
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


```
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
  ```
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
  ```
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
```
#[test]
fn should_transfer_money() -> Result<(), String> {
    ...
    Ok(())
}
```

```
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
```
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
```
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

```
impl BrowserCommand<String> {
    fn print_payload(&self) {
        println!("{}", self.payload)
    }
}
```

Method that returns a Generic 
```
fn get_payload(&self) -> &T {
    &self.payload
}
```
* no runtime performance cost 
* creates concrete functions, structs, and impl blocks at compile time and updates the call sites to call the concrete versions

### Traits
Rust does not support classical inheritance. Instead, traits are use. 

Only functionality can be shared with traits

```
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
```
//only if returning one concrete type
fn create_paint_object() -> impl Paint() {}
```

### Supertraits
Traits can rely on other traits. Traits relied on are called supertraits. 

```
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

```
#[derive(Debug)]
struct Point{}
```
Partial equality
```
#[derive(Debug, PartialEq)]
struct Point{}
```

### The Orphan Rule
In order to implement a trait on a type, trait or type needs to be defined in the scope. 

Can create a wrapper type:
```
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
```
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
```
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
```
let s: &'static str = "Lets get rusty!"
s
```

### Structs and Lifetime Elision
```
struct Tweet {
    content: &str;
}
```
Must add a generic lifetime to store references in structs 

```
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
```
let button = Box::new(Button {text: "name".to_owned()})
```
single ownership of something on the heap 

use cases: 
* avoid copying large ammounts of data when transferring ownership 
* similar to getting a heap pointer from `malloc` in C

[SO Thread on malloc and Box smart pointers](https://stackoverflow.com/questions/48485454/rust-manual-memory-management)

Recursive types 

We cannot make a struct with recursive size like 
```
struct Container {
    name: String,
    child: Container // won't compile
}
```

we instead have to use *indirection*-> use a reference to the recursive type
```
struct Container {
    name: String,
    child: Box<Container>
} 
```


### `Rc` smart pointer 
* Shared ownership 
** NOT** included in the Rust prelude 
```
use std::Rc::rc;
```

Pass around RC
```
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
```
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
```
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
    ```
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
* 

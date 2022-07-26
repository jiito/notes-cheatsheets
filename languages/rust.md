# Rust 

Lets get rusty bootcamp 

## variables

* rust infers type but type can be specified with `:<type> = `

### mutatbility 
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

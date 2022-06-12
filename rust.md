# Rust

## Cargo

- New rust project: `cargo new <project_name>`
- Build rust project: `cargo build` -> executable in `target/debug`
- Build and run: `cargo run`
- Can check if compile is possible: `cargo check`

## Rust Formatting

- `rustfmt <source_file>`

## Variables

- Variables have types, can manually assign these or let the compiler decide
  - `let x = 4;`: Compiler will make x and integer type
  - `let x: u32 = 4;`: Manually assign to 32 bit unsigned int

- By default variables in rust are immuatable -> cannot reassign a value to it
  - `let mut x = 4;`: Variable is mutable so x can be ressigned another value

- It is also possible to re-declare varaible if it is immuatable

```rust
let x = 4;
println!("Value of x is {}", x);
// let x = x + 1; also works
// Can also make a x a different type from before
let x = 5;
println!("Value of x is {}", x);
```

## Data Types

- Signed integer types: `i8, i16, i32, i64, i128`
- Unsigned integer types: `u8, u16, u32, u64, u128`
- Floating point: `f32, f64`
- Boolean: `true/false` -> `bool`
- Character: `char`
  - `let letter: char = 'a';` -> Should use single quaotations

- Tuple: Fixed length sequence of elements
  - `let my_var = (1, true, 's');`
  - `let my_var: (i32, bool, char) = (1, true, 's');`
  - Access elements:
    - `my_var.0 my_var.1 my_var.2`

- Arrays: Have to have the same type
  - `let arr = [1, 2, 3, 4, 5];`
  - `let arr: [u32;5] = [1, 2, 3, 4, 5];`
  - Accessing: `arr[1]`

## Console input

- User input not included in default rust prelude
- Crate == Package/Library, containing a module

```rust
use std::io; // io module from std package/crate

fn main(){
    let mut input = String::new();

    io::stdin().read_line(&mut input).expect("Failed to read line");

    println!("User input {}", input);
}
```

## Constants

- Convention is to use upper case
- Have to specifiy type
- `const SECONDS_IN_MINUTE: u32 = 60;`

## Printing

- String formatting

```rust
let x = 4;
println!("x is: {}", x);
```

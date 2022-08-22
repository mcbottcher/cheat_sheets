# Rust

## Cargo

- New rust project: `cargo new <project_name>`
- Build rust project: `cargo build` -> executable in `target/debug`
- Build and run: `cargo run`
- Can check if compile is possible: `cargo check`
- By default a rust project is built in debug mode
  - This includes extra info for debug
  - To create an optimised release: `cargo build --release`

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

## Comments

- Inline `//`

## Arithmetic

- Data types should be the same to perform arithmetic together
- Result will be the same type as operands

```rust
let x:u8 = 255;
let x:u8 = 1;

let z = x + y;
```

- Note, this generates an overflow error!

## Type Casting

- Can indicate variable type after use: `let x = 255u8;`
  - Different syntax: `let x = 255_u8;`
  - Different syntax: `let x = 255 as u8;`

```rust
let x = 3 as u8;
let y = 4 as u16;

// Z will be 7 of type u16
let z = (x as u16) + y;
```
- Better to convert smaller type to larger to avoid overflow
  - RUST still doesn't catch all overflows!

## Conditions

- Can use `< > <= >= == !=` (like C)
- Can use logical operators: `&& || !` (like C)
- Can use `if, else if, else` (like C)

## Functions

- Snake Case convention for function naming: `fn my_func()`
- Doesn't matter where function is defined, i.e. above or below usage
- Arguments: `fn add_numbers(x: i32, y: i32)`
- Returning values from function:
  - `-> <return type>`
  - Use expression to return -> no `;`!
  - Can also use `return` keyword -> then you can use the semicolon

```rust
fn add_numbers(x: i32, y: i32) -> i32 {
  x + y
}

fn add_numbers2(x: i32, y: i32) -> i32 {
  return x + y;
}
```

## Expression

```rust
let number = {
  let x = 3;
  x + 1 // Note no ;
};

println!("{}", number); // prints 4
```

## Rust naming conventions

[Naming conventions](https://rust-lang.github.io/api-guidelines/naming.html)

## Print formatting

- Print floating point value to 3 decimal places: `println!("c is {:.3}", c)`
- Print with only a certain number of characters: `println!("c is {:8.3}", c)` (pads with spaces)
  - Pad with zeros: `println!("c is {:08.3}", c)`
- No automatic newline: `print!("This does not have a newline at the end")`
- Can reference variables more than once in the print macro:

```rust
println!("a is {0}, c is {1}, a is {0}", a, c)
```

[Rust formatting standards](https://doc.rust-lang.org/std/fmt/)

- Can also use argurments from the local scope:

```rust
let x = 8;
println!("x is {x}");
```

- Output binary representation: `println!("{:08b}", a)`

# Bitwise operators

- NOT: `x = !x` -> flips the bits (like ~ in C)
- AND: `&`
- OR: `|`
- XOR: `^`
- Shifts: `<<` or `>>`

## Boolean operators

- Use `! & | ^` for evaluating boolean types: `let c = true & false;`
- Short circuit operators: `!! && || ^^`
  - If first expression is evaluated and next does not need to be it is not: `if (true) || (expression1)` -> expression1 not needed to be evaluated, since it will always be true...
    - proof: `if true || panic!()` -> panic! not evaluated, causes an error and exits program
- Can use comparison operators with booleans too: `==, !=, <, >`

## Char Data Type

- Takes up 4 bytes of memory: Unicode scalar value

```rust
let finger = '\u{261D}'; // Display unicode character 0x261D
```

## Arrays

```rust
let letters = ['a', 'b', 'c'];

// Uninitialised array
let numbers: [i32; 5]; // type i32, 5 elements

// initalise array with zeros using repeat expression
numbers = [0; 5]; // five copies of zero
```

- Arrays must have the same data type
- To index an array in rust, need to use the `usize` type
- Multi-dimensional arrays also possible

```rust
let garage : [[[i32; 100]; 20]; 5]; // uninitialised array of 100x20x5

// initalised array with zeros
let garage = [[[0; 100]; 20]; 5];
```

## Tuples

- Group multiple elements of mixed data types
- Elements are ordered
- Stored in fixed-length, contiguous section of memory
- Data types of items must be known at compile time

```rust
let my_tuple = (10, 3.14, 'x');
println!("{stuff.0}"); // Notice zero indexed

let mut my_tuple: (u8, f32, char) = (10, 3.14, 'x');
my_tuple.0 += 2; // now my_tuple.0 is 12

let (a, b, c) = my_tuple;
// Now a == 12
```

## Functions

- Declare functions: `fn my_function(){}`
- Function doesn't need to be declared before it is called
- Function parameters:

```rust
fn say_number(number: i32){
    println!("Number is {number}");
}
```

- Function return types:

```rust
// Input parameter x is i32, function returns an i32
fn square(x: i32) -> i32 {
    println!("Value of x is {x}");
    x * x // Notice no semicolon. This makes this an expression, and x*x is returned

    // Can also use: return x*x;
}
```

- Can also return tuples

```rust 
fn square(x: i32) -> (i32, i32) {
    return (x, x*x); // Returns x and x squared
}

fn main(){
    // :? allows us to print the tuple -> debug formatting
    println!("Result is {:?}", sqaure(13));
}
```

- Unit data type: returned when no return type is specified
  - Represented with `()`
  - `fn my_function(x: i32) -> (){}`

## Statements vs expressions

- Statement
  - Performs an action without returning a value
  - End with a semicolon
- Expression
  - Evaluates to a resulting value
  - Does not end with a semicolon
    - `1 + 2` returns 3
    - `1 + 2;` returns nothing

## Conditional execution

```rust
if x == 3 {
    println!("X is 3");
}
```

- Cannot use integer value as boolean, must cast to boolean:

```rust
let x = 3;

// This will NOT work
if x {
  println!("If worked");
}

// This will work
if x != 0 {
  println!("It worked);
}
```

- Can use `else` and `else if` as in C
- Can use `if` in assignment:

```rust
let x = if my_bool {1} else {2};
```

## Loops

- `loop`
  - Infinite loop, until broken with `break` or `return`
  - Can pass out a variable when the loop finishes

```rust
let mut count = 0;
let result = loop{
    count += 1;
    println!("Count is {count}");
    if count == 10 {
        break count * 10;
    }
}
```

- `while` loop
  - Cannot return a value with the `break` statement

```rust
while count < 10 {
    count += 1;
}
```

- `for` loop
  - Converts message array into an iterator
    - Has a function called `next()` to go to the next iteration
    - `iter()` is a more recent rust addition

```rust
let message = ['h', 'e', 'l', 'l', 'o'];

for (index, &item) in message.iter().enumerate() {
    println!("Item {index} is {item}");
}
```

```rust
// This will print 0, 1, 2, 3, 4 -> NOT 5
for number in 0..5 {
    println!("{number}");
}
```

## Nested Loops

- Need to use the `iter_mut()` method to change the values of the array

```rust
let mut matrix = [[1,2,3], [4,5,6], [7,8,9]];

for row in matrix.iter_mut() {
    for num in row.iter_mut() {
        *num += 10;
        print!("{num}\t");
    }
    println!();
}

```

## Variable Shadowing

- Can declare a variable with the same name as an existing one
- The new variable "shadows" the previous one, as long as the new one is in scope
- Could lead to bugs if you are not careful with naming of variables...

```rust
let planet = "Earth";
let planet = "Mars";
println!("Planet is {planet}");

// Can change type and mutability
let mut planet = 4;
println!("Planet is {planet}");

{
    let planet = 6;
}

// This will still be 4 since the shadowed 6 is out of scope
println!("Planet is {planet}");
```

## String Data Type

- String literal, e.g.: `let my_var = "Hello";`
  - Immutable
- String Type:
  - Allocated on the heap
  - Mutable
  - Dynamically generated at runtime
  - Stack has pointer data type, size (how much is used) and capacity (how much is allocated)

```rust
let mut message = String::from("Earth");
message.push_str(" is home"); // Appends to the string

println!("{message");
```

## Ownership

- Every value is "owned" by one, and only one, variable at a time
- When the owning variable goes out of scope, the value is dropped
- Variables are responsible for freeing their own resources

```rust
let outer_planet: String;
{
    let inner_planet = String:from("Earth");
    outer_planet = inner_planet; // Pointer to data of inner_planet is moved to outer_planet, so now inner_planet is invalid, since data can only have one owner
}
```

```rust
let outer_planet: String;
{
    let inner_planet = String:from("Earth");
    outer_planet = inner_planet.clone(); // Allocates memory on the heap and copies the contents of inner_planet to outer_planet, so we have two copies of the string "Earth" on the heap
}
```

- When using data types that are of a known size, e.g. integers, that are stored on the stack, data is copied from one variable to a new one and the old one does NOT go invalid like we see in the above example. In short, stack vairable is copied and heap variable is moved...

- Arguments
  - Passing a stack varibale to function creates a copy, so that can be modified in the new function without affecting the old value
  - Passing heap based variable like a String, then the variable is moved like we saw above, so the function parameter is the new owner of the heap data. The original variable is invalid. At the end of the function the data will be thrown away with the variable local the function
    - Can tranfer ownership back from function with a return value...
  
## Borrowing

- Access data without taking ownership of it
- Use the borrow operator: `&`
- Need to use mutable borrow operator when we want to change the value: `&mut`
  - Cannot create other references when using a mutable reference, to prevent data races, in threads for example...

## Slice

- Reference a contiguous section of a collection, e.g. an array or string
- String slice data type: `&str`
  - String slice is done in bytes, so if using more complex characters which span more than one byte you need to be careful with your slice indexes

```rust
let message = String::from("Greetings from Earth!");
let last_word = &message[15..20]; // To go to the end use &message[15..]
println!("{last_word}"); // Should print "Earth"
```


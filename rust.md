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

## Rust Standard Library

- [Standard Modules](https://doc.rust-lang.org/std/#modules)
- Need to use the `use` keyword to use a module (not in the prelude): `use std::thread`
- The Prelude: List of things automatically imported into every rust project

## Standard Input

- `use std::io;`

```rust
let mut buffer = String::new();
println!("Enter your message");
io::stdin().read_line(&mut buffer);
println!("buffer is {buffer}");

// parse this string into an i32
// parse returns a result enum, i.e. could be an error, if you used an invalid character (not a number)
// unwrap extracts the integer from the enum
let number = buffer.trim().parse::<i32>().unwrap();
println!("You gave {number}");
```

## Crates

- Collection of rust source code files
  - Binary crates compile to produce an executable program
  - Library crate contain code for other programs to use
- Crates.io is the registry for libraries e.g. random number crate
- Add a crate to project by adding it to Cargo.toml


## Command Line Arguments

- Can be read using `std::env::args` module
  - This returns an iterator over the arguments passed to the program
- First argument is traditionally the executable path (Not always though)

```rust
use std::env;

fn main() {

  if env::args().len() <=2{
    println!("Not enough arguments");
    return;
  }

  for(index, argument) in env::args().enumerate() {
    println!("Argument {index} is {argument}");
  }
}
```

## Reading and Writing Files

- `use std::fs;`: Standard filesystem

```rust
use std::fs;

fn main(){
  let contents = fs::read_to_string("planets.txt").unwrap();
  println!("Contents is {contents}");

  for line in contents.lines() {
    println!("line is {}", line);
  }

  // For files not using plain text, we read it as bytes (u8) and not as a string
  let contents = fs::read("planets.txt").unwrap();
  println!("contents is {:?}", contents);
}
```

- Use standard library paths module to work with and minipulate file paths

- Writing to file:

```rust
let mut speech = String::new();
speech.push_str("Hello my name is Mikkel\n");

fs::write("speech.txt", speech);
```

- Appending data to a file:

```rust
use std::io::prelude::*;

fn main(){
  // Sets options for file writing
  // Unwrap at the end converts from result enum to file type
  let mut file = fs::OpenOptions::new().append(true).open("planets.txt").unwrap();
  
  // Can only write arrays of bytes so use the `b` to indicate that this string should be interpreted as a byte array
  file.write(b"\npluto");
}
```

## Structs

- Elements are named so don't need to worry about the order they are stored like a tuple

```rust
struct Shuttle {
    name: String,
    crew_size: u8,
    propellant: f64
}

fn main(){
    let vehicle = Shuttle {
      name : String::from("Endeavour"),
      crew_size: 7,
      propellant: 8675.0
    };

    println!("name is {}", vehicle.name);

    // Can copy elements from another struct of the same type to a new one
    // ..vehicle copies all uninitialised struct members in vehicle2 from vehicle
    let vehicle2 = Shuttle {
        name: String::from("Discovery"),
        ..vehicle
    }

    // to copy all elements including those stored on the stack e.g. String, use the clone method
    let vehicle3 = Shuttle {
       ..vehicle.clone()
    }
}
```

- As well as storing data, structs can also be used for calling functions: methods
- First parameter in method is always a reference to the struct to be able to access the struct data

```rust
// Following from the shuttle struct above
impl Shuttle {
    fn get_name(&self) -> &str{
        &self.name
    }

    fn add_fuel(&mut self, gallons: f64){
        self.propellant += gallons;
    }

    // Associated function
    fn new(name: &str) -> Shuttle {
        Shuttle {
            name: String:from(name),
            crew_size: 7,
            propellant: 0.0,
        }
    }
}
```

- Can also use Associated functions, but the difference here is they do not have the `&self` parameter, so cannot access the data of the struct itself. This is like a class function whereas the methods are object functions.

## Tuple Structs

- Use this when you want a name for a type of tuple but don't want to name the elements of that tuple... e.g. a colour tuple with rgb fields

```rust
struct Colour(u8, u8, u8);

fn main() {
    let red = Colour(255, 0 ,0);

    println!("Red component is {red.0}");
}
```

## Struct with generic types

```rust
// List of distinct types goes here
struct Rectangle<T, T2> {
    width: T,
    height: T2,
}
```

## Generic method

```rust
impl<T, U> Rectangle<T, U> {
    // Need &T since we don't know if it will be a heap based or stack based data type
    fn get_width(&self) -> &T {
        &self.width
    }
}

// One specific for u8, u8 type rectangle
impl Rectangle<u8, u8> {
    fn get_perimeter(&self) -> u8 {
       2 * (self.height + self.width)
    }
}
```

## Generic functions

```rust
fn get_biggest<T: PartialOrd>(a: T, b: T) -> T {
    if a > b {
        a
    } else {
        b
    }
}
```

- This will only work with datatypes that can be compared, so we add the `PartialOrd trait`. So only datatypes that can be compared with the `>` operator

## Box<T> Data Type

- Allows you to store data on the heap, even if it is a data type that would normally be stored on the stack
- It is pointer on the stack
- Smart pointer: Box has ownership of data it points to, and when it goes out of scope, it will atomatically deallocate the memory.
- Box::new -> Calling this allocates the correct amount of memory on the heap, and moves the data, becoming the new owner and the old variable becomes invalid..


```rust
// Continuing above example of shuttle struct
let boxed_vehicle: Box<Shuttle> = Box::new(vehicle);

// dereference operator -> *
println!("Size of pointer {}", &boxed_vehicle);
println!("Size of memory on the heap {}", &*boxed_vehicle);

// move heap data back to stack, passing ownership to unboxed_vehicle
let unboxed_vehicle: Shuttle = *boxed_vehicle;
```

- Uses
  - Store a type whose size cannot be known at compile time
  - Transfer ownership of data to heap where it can more easily transfered, i.e. don't need to do large amounts of copying on the stack

## Traits

- A collection of methods
- A data type can implement a trait
- Generics use traits to specify the capabilities of unknown data types
- There are common traits, but you can also implement your own custom traits to specify capabilities

```rust
// Any struct which implements the Description trait will have a function called describe
trait Description {
    fn describe(&self) -> String;
}

impl Description for Satellite {
    fn describe(&self) -> String {
        // create formatting string to print the struct
        format!{"The {self.name} is flying at {self.velocity}m/s"}
    }
} 
```

- Default implementation for trait methods

```rust
trait Description {
    // If describe is not implemented, it will use this method
    fn describe(&self) -> String {
        format!("This is a default describe method")
    }
}

impl Description for Satellite {

}
```

- New structs have no traits by default, need to add them yourself. eg. Partial Equality trait
- Derivable traits: Provide default implementations for several common traits

```rust
#[derive(PartialEq, PartialOrd)]
struct Satellite {
    name: String,
    velocity: f64
}

fn main (){
    // now we can compare two Satellite types in our code
    if sat1 == sat2 {
        ...
    }

    // can do this now with partialord
    if sat1 > sat2 {
        ...
    }
}
```

- Multiple trait bounds on a generic type:
  - Separated by `+`: `fn my_func<T: trait_one + trait_two>`
  - Converting types:
    - `if a == T::from(b)`, type of b need to implement trait that it can be converted to type T. This trait is the `From<U>`. Also need to be able to move U type to T type, so U needs the `Copy` trait

- Can also use the `where` keyword to describe which traits to use

```rust
fn compare_and_print<T, U>(a: T, b: U)
    where T: fmt::Display + PartialEq + From<U>
          U: fmt::Display + PartialEq + Copy
    { ...
```

- Return types with implemented traits:

```rust
// Can only return a type that implements the display type
fn get_displayable() -> impl fmt::Display {
    ...
}
```

## The Borrow Checker

- Compares the scopes of variables to determine if all borrows are valid
- Can annotate the lifetime of variables:
  - Name must begin with `'` symbol
  - Convention is to use a single, lowercase letter for the lifetime: `'a`


```rust
// Tells rust compiler how the lifetimes of the inputs and outputs relate to each other
// Here lifetime of inputs and outputs are the same
// If lifetimes of inputs are different, shorter lifetime is used
fn best_fuel<'a>(x: &'a str, y: &'a str) -> &'a str{
    ...
}

or

fn best_fuel<'a, 'b>(x: &'a str, y: &'b str) -> &'a str{
    ...
}
```

- Struct lifetimes and methods:

```rust
struct Shuttle<'a> {
    name: &'a str
}

// Here we need a second lifetime indicator 'b to show that output will
// not match lifetime of the shuttle struct
impl<'a, 'b> Shuttle<'a> {
    fn send_transmission(&'a self, msg: &'b str) -> &'b str {
        println!("Transmitting message: {}", msg);
        msg
    }
}
```

- `'static` is a reserved lifetime keyword
  - Indicates references available for entire duration of the program
  - e.g. a string literal is stored in the program's binary, so never is lost
    - `let s: &'static = "Greetings";`
  - Can also be used in traits for generic types: `T: Display + 'static`
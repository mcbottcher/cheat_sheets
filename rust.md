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

## Printing

- String formatting

```rust
let x = 4;
println!("x is: {}", x);
```

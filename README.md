# RAM Emulator

![Version 0.1.7](https://img.shields.io/badge/version-0.1.7-blue.svg)
[![License](https://img.shields.io/badge/license-GNU3-blue.svg)](./LICENSE)
[![Oleksandr Babak](https://img.shields.io/badge/Author-Oleksandr%20Babak-blue.svg?style=flat)](mailto:alexanderbabak@proton.me)
[![Ddystopia](https://img.shields.io/badge/Github-Ddystopia-green.svg?style=flat)](https://github.com/Ddystopia/)

A Rust-based library for emulating a Random Access Machine (RAM). This library
provides parsing, interpretation, and execution of RAM assembly code, as well as
support for mathematical operations, labels, jumps, and I/O operations.

## Features

- Parsing of RAM assembly code
- Mathematical operations: `ADD`, `SUB`, `MULT` (`MUL`), `DIV`
- Labels and jumps: `JMP` (`JUMP`), `JZ` (`JZERO`), `JGZ` (`JGTZ`)
- Move operations: `LOAD`, `STORE`
- I/O operations: `READ` (`INPUT`), `WRITE` (`OUTPUT`)
- Error handling and reporting: `ParseError`, `InterpretError`

## Installation and Usage

Add the library as a dependency to your Rust project by including the following
in your `Cargo.toml` file:

```toml
ramemu = { git = "https://github.com/AVO-cado-team/ramemu.git", tag = "0.1.7"}
```

## Examples

Here's an example of how to use the library to create a RAM program and run it:

```rust

use std::io::{stdin, stdout, BufReader};

use ramemu::{program::Program, ram::Ram};

fn main() {
  let source = r#"
      # Your RAM assembly code here 
      HALT
    "#;

  let program = Program::from_source(source).unwrap();
  let mut ram = Ram::new(
    program,
    Box::new(BufReader::new(stdin())),
    Box::new(stdout()),
  );

  match ram.run() {
    Ok(_) => println!("Program executed successfully"),
    Err(e) => println!("Error during execution: {:?}", e),
  }
}

```

## Supported Syntax

The parser supports the following syntax:

- Comments: Start with `#`
- Labels: End with `:`
- Links: Types include explicit (`{usize}`), without link (`={usize}`), and
  double link (`*{usize}`)

## Limitations and Future Improvements

This library is a work in progress and may have limitations. Future improvements
may include better error handling, performance optimizations, and additional
features.

## Contributing

Contributions to the project are welcome. You can report bugs, request features,
or submit pull requests. Before submitting a pull request, make sure your
changes are well-tested and documented.

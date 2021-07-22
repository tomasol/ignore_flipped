ignore_flipped
======
Fork of [ignore](https://crates.io/crates/ignore) crate, that
aims to add support for flipping the output - allowing to
iterate over files that are ignored.

Dual-licensed under MIT or the [UNLICENSE](https://unlicense.org/).

### Status
WIP. Parallel execution is not implemented.
Tested only

### Documentation

[https://docs.rs/ignore](https://docs.rs/ignore)

### Usage

Add this to your `Cargo.toml`:

```toml
[dependencies]
ignore_flipped = "0.4"
```

### Example

This example shows the most basic usage of this crate. This code will
recursively traverse the current directory while automatically filtering out
files and directories according to ignore globs found in files like
`.ignore` and `.gitignore`:

By default, the recursive directory iterator will ignore hidden files and
directories. This can be disabled by building the iterator with `WalkBuilder`.

```rust,no_run
use ignore_flipped::WalkBuilder;

for result in WalkBuilder::new("./").hidden(false).flip_result(true).build() {
    // Each item yielded by the iterator is either a directory entry or an
    // error, so either print the path or the error.
    match result {
        Ok(entry) => println!("{}", entry.path().display()),
        Err(err) => println!("ERROR: {}", err),
    }
}
```

Result is list of files (including hidden files) that are blacklisted by files
like `.ignore` and `.gitignore`.
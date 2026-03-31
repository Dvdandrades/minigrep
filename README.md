# minigrep

A command-line search tool built in Rust, inspired by the classic `grep` utility. Searches for a text pattern within a file and prints every matching line to stdout.

This project is based on the I/O project from [The Rust Programming Language](https://doc.rust-lang.org/book/ch12-00-an-io-project.html) book.

## Features

- Search for a string pattern across any text file
- Case-insensitive search via an environment variable
- Clean separation of concerns between `main.rs` and `lib.rs`
- Descriptive error messages printed to stderr

## Project Structure

```
minigrep/
├── Cargo.toml
├── Cargo.lock
├── poem.txt          # Sample file for testing
└── src/
    ├── main.rs       # Entry point: argument parsing and error handling
    └── lib.rs        # Core logic: Config, run, search functions
```

## Usage

### Build

```bash
cargo build
```

### Run

```bash
cargo run -- <query> <file_path>
```

**Example:**

```bash
cargo run -- the poem.txt
```

This will print every line in `poem.txt` that contains the word `the`.

### Case-insensitive search

Set the `IGNORE_CASE` environment variable to perform a case-insensitive search:

```bash
IGNORE_CASE=1 cargo run -- the poem.txt
```

On Windows (PowerShell):

```powershell
$Env:IGNORE_CASE=1; cargo run -- the poem.txt
```

## Running Tests

```bash
cargo test
```

The test suite covers both case-sensitive and case-insensitive search behaviour.

## How It Works

1. `main.rs` collects command-line arguments and passes them to `Config::build`.
2. `Config::build` validates the arguments and reads the `IGNORE_CASE` environment variable.
3. `run` reads the target file and delegates to either `search` or `search_case_insensitive`.
4. Matching lines are printed to stdout. Errors are printed to stderr and the process exits with code `1`.

## Requirements

- [Rust](https://www.rust-lang.org/tools/install) 1.56 or later

## License

This project is available under the [MIT License](LICENSE).

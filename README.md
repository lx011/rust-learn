# Rust Learn

## Start

### Install

```bash
# installing `rustup` on Linux or macOS
curl https://sh.rustup.rs -sSf | sh

export PATH="$HOME/.cargo/bin:$PATH"
```

### Updating & Uninstalling

```bash
rustup update

rustup self uninstall
```

### Troubleshooting

```bash
rustc

rustup

cargo
cargo new
cargo check
cargo run
cargo build [--release]
cargo doc [--open]
cargo test

# If you don’t want to run the tests in parallel
# or if you want more fine-grained control over the number of threads used
# We set the number of test threads to 1, telling the program not to use any parallelism.
cargo test -- --test-threads=1

# disable the output capture behavior
cargo test -- --nocapture

# Filtering to Run Multiple Tests
# note that the module in which a test appears becomes part of the test’s name,
# so we can run all the tests in a module by filtering on the module’s name.
cargo test <fn_part_name>

# run only the ignored tests
cargo test -- --ignored

# to run all the tests in a particular integration test file
cargo test --test <filename>

# run tests for one particular crate in a workspace from the top-level directory
cargo test -p <crate_name>

cargo login <API_TOKEN>
cargo publish
# `--undo`: By adding `--undo` to the command, you can also undo a yank and allow projects to start depending on a version again
cargo yank --vers <version> [--undo]

cargo install <binary_crate>
```

> [Cargo.toml](https://doc.rust-lang.org/cargo/reference/manifest.html)

```toml
[package]
name = "pack_name" # the name of the package
version = "pack_version" # the current version, obeying semver
authors = ["name <email@example.com>"]
edition = "2018"

[profile.dev]
opt-level = 0

[profile.release]
opt-level = 3

[dependencies]

[workspace]
members = ["..."]
```

### Local Documentation

```bash
rustup doc
```

## Data Types

* Integer Types

  | Length  | Signed | Unsigned |
  | ------- | ------ | -------- |
  | 8-bit   | i8     | u8       |
  | 16-bit  | i16    | u16      |
  | 32-bit  | i32    | u32      |
  | 64-bit  | i64    | u64      |
  | 128-bit | i128   | u128     |
  | arch    | isize  | usize    |

  * signed: **-2<sup>n-1</sup> ～ 2<sup>n-1</sup>-1**
  * unsigned: **0 ～ 2<sup>n</sup>-1**
  * `isize` & `usize`: 64 bits *(64-bit architecture)*, 32 bits *(32-bit architecture)*

* Floating-Point Types

> `f32`, `f64`(default): The `f32` type is a single-precision float, and `f64` has double precision.

* The Boolean Type: `bool`

* The Character Type: `char`

* Compound Types:

  * The Tuple Type: `tuple`

   > `tuple`: A finite heterogeneous sequence, (T, U, ..).

  * The Array Type: `array` `slice`

   > `array`: A fixed-size array, denoted `[T; N]`, for the element type, `T`, and the non-negative compile-time    constant size, `N`.

   > `slice`: A dynamically-sized view into a contiguous sequence, `[T]`.

## Documentation

> Documentation comments within items are useful for describing crates and modules especially. Use them to explain the overall purpose of the container to help your users understand the crate’s organization.

* `///`: documentation comments, support Markdown notation for formatting the text.
* `//!`: adds documentation to the item that contains the comments rather than adding documentation to the items following the comments.

> **Commonly Used Sections**

* `Panics`: The scenarios in which the function being documented could panic. Callers of the function who don’t want their programs to panic should make sure they don’t call the function in these situations.
* `Errors`: If the function returns a `Result`, describing the kinds of errors that might occur and what conditions might cause those errors to be returned can be helpful to callers so they can write code to handle the different kinds of errors in different ways.
* `Safety`: If the function is `unsafe` to call, there should be a section explaining why the function is unsafe and covering the invariants that the function expects callers to uphold.

## Attributes

```rust
/** syntax */
// InnerAttribute:
#![Attr]

// OuterAttribute:
#[Attr]
```

<table>
<thead>
  <tr>
    <th>Built-in attributes</th>
    <th>attribute</th>
    <th>description</th>
  </tr>
</thead>
<tbody>
  <!-- Conditional compilation -->
  <tr>
      <td rowspan="2">Conditional compilation</td>
      <td><b>cfg</b></td>
      <td>controls conditional compilation</td>
  </tr>
  <tr>
      <td><b>cfg_attr</b></td>
      <td>conditionally includes attributes</td>
  </tr>

  <!-- Testing -->
  <tr>
      <td rowspan="3">Testing</td>
      <td><b>test</b></td>
      <td>marks a function as a test</td>
  </tr>
  <tr>
      <td><b>ignore</b></td>
      <td>disables a test function</td>
  </tr>
  <tr>
      <td><b>should_panic</b></td>
      <td>indicates a test should generate a panic.</td>
  </tr>

  <!-- Testing -->
  <tr>
      <td rowspan="1">Derive</td>
      <td><b>derive</b></td>
      <td>automatic trait implementations</td>
  </tr>

  <!-- Macros -->
  <tr>
      <td rowspan="5">Macros</td>
      <td><b>macro_export</b></td>
      <td>exports a <code>macro_rules</code> macro for cross-crate usage</td>
  </tr>
  <tr>
      <td><b>macro_use</b></td>
      <td>expands macro visibility, or imports macros from other crates</td>
  </tr>
  <tr>
      <td><b>proc_macro</b></td>
      <td>defines a function-like macro</td>
  </tr>
  <tr>
      <td><b>proc_macro_derive</b></td>
      <td>defines a derive macro</td>
  </tr>
  <tr>
      <td><b>proc_macro_attribute</b></td>
      <td>defines an attribute macro</td>
  </tr>

  <!-- Diagnostics -->
  <tr>
      <td rowspan="3">Diagnostics</td>
      <td><b>allow, warn, deny, forbid</b></td>
      <td>alters the default lint level</td>
  </tr>
  <tr>
      <td><b>deprecated</b></td>
      <td>generates deprecation notices</td>
  </tr>
  <tr>
      <td><b>must_use</b></td>
      <td>generates a lint for unused values</td>
  </tr>

  <!-- ABI, linking, symbols, and FFI -->
  <tr>
      <td rowspan="11">ABI, linking, symbols, and FFI</td>
      <td><b>link</b></td>
      <td>specifies a native library to link with an <code>extern</code> block</td>
  </tr>
  <tr>
      <td><b>link_name</b></td>
      <td>specifies the name of the symbol for functions or statics in an <code>extern</code> block</td>
  </tr>
  <tr>
      <td><b>no_link</b></td>
      <td>prevents linking an extern crate</td>
  </tr>
  <tr>
      <td><b>repr</b></td>
      <td>controls type layout</td>
  </tr>
  <tr>
      <td><b>crate_type</b></td>
      <td>specifies the type of crate (library, executable, etc.)</td>
  </tr>
  <tr>
      <td><b>no_main</b></td>
      <td>disables emitting the main symbol</td>
  </tr>
  <tr>
      <td><b>export_name</b></td>
      <td>specifies the exported symbol name for a function or static</td>
  </tr>
  <tr>
      <td><b>link_section</b></td>
      <td>specifies the section of an object file to use for a function or static</td>
  </tr>
  <tr>
      <td><b>no_mangle</b></td>
      <td>disables symbol name encoding</td>
  </tr>
  <tr>
      <td><b>used</b></td>
      <td>forces the compiler to keep a static item in the output object file</td>
  </tr>
  <tr>
      <td><b>crate_name</b></td>
      <td>specifies the crate name</td>
  </tr>

  <!-- Code generation -->
  <tr>
      <td rowspan="4">Code generation</td>
      <td><b>inline</b></td>
      <td>hint to inline code</td>
  </tr>
  <tr>
      <td><b>cold</b></td>
      <td>hint that a function is unlikely to be called</td>
  </tr>
  <tr>
      <td><b>no_builtins</b></td>
      <td>disables use of certain built-in functions</td>
  </tr>
  <tr>
      <td><b>target_feature</b></td>
      <td>configure platform-specific code generation</td>
  </tr>

  <!-- Documentation -->
  <tr>
      <td rowspan="1">Documentation</td>
      <td><b>doc</b></td>
      <td>specifies documentation. See
        <a href="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html">The Rustdoc Book</a>
        for more information.
        <a href="https://doc.rust-lang.org/reference/comments.html#doc-comments">Doc comments</a>
        are transformed into <code>doc</code> attributes
      </td>
  </tr>

  <!-- Preludes -->
  <tr>
      <td rowspan="2">Preludes</td>
      <td><b>no_std</b></td>
      <td>removes std from the prelude</td>
  </tr>
  <tr>
      <td><b>no_implicit_prelude</b></td>
      <td>disables prelude lookups within a module</td>
  </tr>

  <!-- Modules -->
  <tr>
      <td rowspan="1">Modules</td>
      <td><b>path</b></td>
      <td>specifies the filename for a module</td>
  </tr>

  <!-- Limits -->
  <tr>
      <td rowspan="2">Limits</td>
      <td><b>recursion_limit</b></td>
      <td>sets the maximum recursion limit for certain compile-time operations</td>
  </tr>
  <tr>
      <td><b>type_length_limit</b></td>
      <td>sets the maximum size of a polymorphic type</td>
  </tr>

  <!-- Runtime -->
  <tr>
      <td rowspan="3">Runtime</td>
      <td><b>panic_handler</b></td>
      <td>sets the function to handle panics</td>
  </tr>
  <tr>
      <td><b>global_allocator</b></td>
      <td>sets the global memory allocator</td>
  </tr>
  <tr>
      <td><b>windows_subsystem</b></td>
      <td>specifies the windows subsystem to link with</td>
  </tr>

  <!-- Features -->
  <tr>
      <td rowspan="1">Features</td>
      <td><b>feature</b></td>
      <td>used to enable unstable or experimental compiler features. See
        <a href="https://doc.rust-lang.org/unstable-book/index.html">The Unstable Book</a>
        for features implemented in <code>rustc</code>
      </td>
  </tr>
</tbody>
</table>

```rust
/** Diagnostics */
// overrides the check for C so that violations will go unreported
#[allow(C)]
// warns about violations of C but continues compilation
#[warn(C)]
// signals an error after encountering a violation of C
#[deny(C)]
// is the same as deny(C), but also forbids changing the lint level afterwards
#[forbid(C)]
// since: specifies a version number when the item was deprecated
// note: specifies a string that should be included in the deprecation message
#[deprecated(since = "", note="")]
// is used to issue a diagnostic warning when a value is not "used"
#[must_use]


/** Code generation */
// suggests performing an inline expansion.
#[inline]
// suggests that an inline expansion should always be performed.
#[inline(always)]
// suggests that an inline expansion should never be performed.
#[inline(never)]

/** Testing */
#[test]
#[ignore]
#[should_panic]
```

## Concept

* `Object-Oriented`: Object-oriented programs are made up of objects. An object packages both data and the procedures that operate on that data. The procedures are typically called methods or operations.
* `Polymorphism`: To many people, polymorphism is synonymous with inheritance. But it’s actually a more general concept that refers to code that can work with data of multiple types. For inheritance, those types are generally subclasses. \
Rust instead uses generics to abstract over different possible types and trait bounds to impose constraints on what those types must provide. This is sometimes called bounded parametric polymorphism.

## Related Links

* [A closer look at Ownership in Rusts](https://blog.thoughtram.io/ownership-in-rust)



# wasi2ic

![Tests](https://github.com/wasm-forge/wasi2ic/actions/workflows/rust.yml/badge.svg?event=push)
[![Coverage](https://codecov.io/gh/wasm-forge/wasi2ic/graph/badge.svg?token=XE48Z6JSYS)](https://codecov.io/gh/wasm-forge/wasi2ic)

`wasi2ic` is a tool to convert WebAssembly System Interface (WASI) dependent Wasm module to run on the Internet Computer (IC) computer.


## Compiling wasi2ic

* Clone the https://github.com/wasm-forge/wasi2ic: 
```bash
  git clone https://github.com/wasm-forge/wasi2ic
```

* Enter the `wasi2ic` folder

* Compile the project with `cargo build` and copy the tool to some executable path or alternatively use `cargo install --path .`, but note that the project is still in the early development.


## Usage

To use this tool, navigate to the directory where the WASI-dependent project resides, and run the command:

```bash
  wasi2ic <input-wasm-file> <output_wasm_file>
```

This will read the old Wasm file and create a new Wasm file with the WASI dependencies removed.

**NOTE**

The tool requires that the polyfill implementation is present in your Wasm binary, to include the polyfill implementation into your canister project you need to add the dependency:

```bash
cargo add --git https://github.com/wasm-forge/ic-wasi-polyfill
```

This will create the polyfill methods in your `.wasm` file, which are needed for `wasi2ic`.

Also add the call to the init of the polyfill, example:

```rust
#[ic_cdk::init]
fn init() {
    unsafe {
        ic_wasi_polyfill::init(&[0u8; 32], &[]);
    }
}
```



## Related repositories



| Repository                                      |  Description                  | 
| --------------------------------------------- | ----------------------------- |
| [ic-wasi-polyfill](https://github.com/wasm-forge/ic-wasi-polyfill) | Polyfill library implementing the low-level WASI calls. |
| [stable-fs](https://github.com/wasm-forge/stable-fs) | Simple file system implementation based on the stable structures. The file system implements backend for the ic-wasi-polyfill |
| [examples](https://github.com/wasm-forge/examples) | Repository containing various examplpes of runnig WASI projects on the IC. |
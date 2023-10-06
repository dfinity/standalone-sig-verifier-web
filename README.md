# standalone-sig-verifier-web
Small wrapper around the `ic-standalone-sig-verifier` rust crate ([code](https://github.com/dfinity/ic/tree/master/rs/crypto/standalone-sig-verifier)) to publish it as a browser compatible library to npm.

## Prerequisites

- [rust](https://www.rust-lang.org)
- [wasm-pack](https://github.com/rustwasm/wasm-pack)

## Building
Run the following command
```bash
wasm-pack build --target web --out-dir dist --release
```

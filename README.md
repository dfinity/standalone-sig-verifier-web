# standalone-sig-verifier-web
JS/TS Wrapper for the `ic-standalone-sig-verifier` rust crate ([code](https://github.com/dfinity/ic/tree/master/rs/crypto/standalone-sig-verifier)) to publish it as a browser / node compatible library to npm.

> _**Warning:**_ There are some caveats to using this library:
> 1. **Verifying signatures in the front-end is generally unsafe!** Malicious users could modify the front-end code and bypass the signature verification. This library is intended for use in demos, prototypes, backends and other situations where the code either cannot be tampered with _or_ the tampering does not pose a security risk.
> 2. This library is built from the `master` branch of the `ic` repo rather than a proper release of the underlying library. This means that the API may change at any time.
> 3. The resulting wasm module is _heavy_, around 400 kb gzipped. Do not use this library if you are concerned about the size of your bundle.


## Prerequisites

- [rust](https://www.rust-lang.org)
- [wasm-pack](https://github.com/rustwasm/wasm-pack)

## Building
Run the following command
```bash
wasm-pack build --target web --out-dir dist --release --scope dfinity
```
## Usage Example

```js
import initSigVerifier, {verifyIcSignature} from '@dfinity/standalone-sig-verifier-web';

async function example(dataRaw, signatureRaw, derPublicKey, root_key) {
    // load wasm module
    await initSigVerifier(); 
    try {
        // call the signature verification wasm function
        verifyIcSignature(dataRaw, signatureRaw, derPublicKey, root_key);
        console.log('signature verified successfully')
    } catch (error) {
        // the library throws an error if the signature is invalid
        console.error('signature verifcation failed', error)
    }
}
```
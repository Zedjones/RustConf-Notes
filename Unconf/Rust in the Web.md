- `napi-rs`
    - Running a native Rust module alongside Node
- Not a great way to clean up data on the Rust side on a regular/controlled interval
    - Can allocate in JS but then you might have a dangling reference in Rust
- `web-sys` and `js-sys`
    - Access JavaScript APIs
- Bindgens
    - `wasm-bindgen`
    - `fp-bindgen`
    - `diplomat`
- Yew
    - React-like framework
    - Maintains a virtual DOM in Rust, eventually applying changes to actual DOM 
    - Alternatives: `sycamore`, `perseus`, `seed` 
        - Differences come from SSR vs. CSR, `perseus` biggest/most viable alternative at the moment (perhaps?)
        - Information for newcomers b/w choices could possibly be improved
- Interface types
    - WASI wg standard - common set of types b/w JavaScript and WASM environment
        - Currently a serialization game w/ u8 arrays
- Reference types
    - Pass references between the two sides
- Speed: Vanilla JS > wasm frameworks > React
- Could do entire UI in WebGL Canvas
    - Would be a massive development effort to get off the ground
- Binary size w/ WASM
    - WASM compiled will be larger than JS-equivalent code, not much you can do about it right now
        - Have to send everything down the wire at the moment
    - In JS, so much is included in the browser but not w/ WASM 
- Multi-threading
    - Can do at the moment, but is a massive pain
- Rayon bindgen can be used to do multi-threading 
- Can do async and put it on the JS event loop, but that comes with its own complexities
- `iambenwis`

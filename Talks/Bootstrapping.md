- Bootstrapping
    - Compiler written in Rust
        - Beta builds nightly, stable builds beta, previous stable builds stable
    - `std` library depends on implementation details of the compiler
        - Because of how intrinsically connected they are, the `std` library feels like part of the compiler itself
            - Works because `std` library only has to support exactly one version of the compiler
    - Build standard library before building the compiler itself
        - Allows us to dogfood experimental (unstable) features
        - Use two difference compilers to build `rustc`
            - Build the standard library twice due to ABI reasons
    - What happens when there's a bug in the compiler itself?
        - Undefined behavior (miscompilation)
            - Now compiled `std` library could have bugs
            - And compiled compiler now can have additional bugs
        - Release train stops a lot of bugs from getting through
        - How about when beta can't build nightly?
            - Patch beta compiler by backporting fix
    - _Reflections on Trusting Trust_
        - Have to build a chain of trust all the way down
            - Problem for Rust is that the chain of trust is very long, and it trails off around 2012
        - Solution: multiple compilers and cross-check their output
            - Problem with Rust is that there's only `rustc` 
                - Actually there's `mrustc`, written in C++
                    - A lot easier to establish trust chains for C++
                    - Problem: 1 person project, only supports up to 1.54 right now
                        - Have to compile 10 versions to establish chain of trust
    - How it could work in the future
        - In the future, we could have `gccrs` stablized
            - Another source for the trust chain
        - Where does beta come from?
            - Just download it
            - But now we have Python, which gets complicated bc Python
            - Solution: use a pre-installed `rustc` 
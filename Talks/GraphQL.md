- Apollo-rs
    - Parser, encoder, smith (test case generator), compiler
    - Compiler
        - **Provide API to its own database**
        - Performance isn't valuable without ergonomics
        - **Provide good diagnostics**
    - Lexing (validate input)
        - Input -> tokens
        - Look-ahead parsing
    - Parsing (validate statements)
        - Intermediary untyped syntax tree
            - Created using recursive descent parser
            - Used rust-analyzer/rowan
            - Fast and helps with ergonomic error output
        - Tokens -> typed syntax tree
            - Created from intermediary untyped syntax tree using `ungrammar`
    - Compiler (semantic analysis)
        - Validate that syntax tree compiles to a valid "program"
        - Uses `salsa-rs` for this step
            - Build out database of facts and query system for said database
            - Memoized to prevent duplicate computations
                - Only first use has large computational cost
        - Database allows for creation of useful diagnostics
    - Built to be fault-tolerant, shouldn't `panic` except in extraordinary circumstances (like recursive depth limits)
        - Gathers all errors before returning, allows for returning an AST alongside the errors
    - Lossless parser, even non-consequential input is kept in the tree
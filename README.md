# Crafting Interpreters

Working through [Crafting Interpreters](https://craftinginterpreters.com/) by Nystrom.

## Notes

### Chapter 1

- compiler-compilers are out of scope (see Yacc, Lex)

### Chapter 2

- Lexing / Scanning turns source code into tokens
- Parsing turns tokens into an AST
- Static analysis of AST can produce semantic insights e.g. symbol scope, type errors
  - This info could be shoved back into the AST itself
  - Or in a symbol table
  - Or an Intermediate Representation (IR)
- Lexing through to AST is called a "language front-end"
- IRs let you write one front-end per lang and one back-end per arch (`X+Y` instead of `X*Y`) e.g. Pascal -> x86, C -> ARM
- Code generation in the back-end can be done in one of two ways:
  - Gen machine code for a real CPU that can be loaded by an OS dircetly onto the chip
  - Gen bytecode for a virtual CPU
    - Another decision:
      - One mini-compiler-translator thing per arch
      - Or a Virtual Machine (VM) that emulates an abstract chip which supports your virtual architecture at runtime. (This is slower, but your lang will be automatically be supported by any arch that supports the lang the VM itself is written in)
        - NOTE: This Language VM (or Process VM) is distinct from a System VM.
- Single-pass compilers
  - Skip the AST step
  - Limits lang features since compiler can't look ahead
  - Mostly a thing of the past when memory was scarce
  - e.g. C, Pascal
- Tree-walk interpreters
  - Execute the AST itself
  - Too slow for real-world use
  - e.g. Ruby v1
- Transpilers
  - Output source code in another lang
  - e.g. Produce C to support all unix machines
  - e.g. Produce JS to support all browsers
- Just-in-time (JIT) compilers
  - Useful if you do not know what arch the user's machine supports
  - e.g. JavaScript
- "compiler" and "interpreter" are not mutually exclusive
  - compiler: Turn source code into another form that the user can run.
  - interpreter: The user runs the source code directly.
  - e.g. cPythong **is** an interpreter, but it **has** a compiler

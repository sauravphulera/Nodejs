# Deep Dive into V8 JavaScript Engine

## Episode 08: Behind the Scenes of V8 Engine

### Parsing Stage in V8 Engine
When JavaScript code is executed, it goes through several stages in the V8 engine. The first stage is **parsing**, which includes **lexical analysis** and **tokenization**.

## 1. Parsing Stage: Lexical Analysis and Tokenization

### Lexical Analysis
- **Purpose**: Break down raw JavaScript code into manageable pieces called tokens.
- **Process**:
  - **Input Code**: `var a = 10;`
  - **Tokenization**: The code is scanned to identify individual tokens.
  - **Example Tokens**:
    ```plaintext
    var (keyword)
    a (identifier)
    = (operator)
    10 (literal)
    ; (punctuation)
    ```

### What is Tokenization?
- **Definition**: The process of converting code into a series of tokens.
- **Why Tokenization?**: Helps the V8 engine read and understand the code more effectively, making further analysis and compilation easier.

### Output
- **Tokens**: The result of tokenization is a list of tokens used in subsequent parsing stages.

## 2. Syntax Analysis and Abstract Syntax Tree (AST)
After lexical analysis, the next step in parsing is **syntax analysis**. This stage converts tokens into an **Abstract Syntax Tree (AST)**.

### Syntax Analysis
- **Purpose**: Analyze the syntactic structure of tokens to build the AST.
- **Process**:
  - Tokens are analyzed according to JavaScript grammar rules to create a structured representation of the code.

### Abstract Syntax Tree (AST)
- **Definition**: A tree-like data structure representing the syntactic structure of the code.
- **Example**:
  ```plaintext
  var a = 10;
  ```
- **Explore AST structures**: [AST Explorer](https://astexplorer.net/)

### Interesting Fact
- **Syntax Errors**: If an unexpected token is encountered, a syntax error occurs because the AST cannot be generated.

## 3. Interpreter and Compilation

### Interpreted vs. Compiled Languages

#### Interpreted Languages
- **Definition**: Executed line by line by an interpreter.
- **Pros**: Faster to start, easier to debug.
- **Cons**: Slower execution compared to compiled languages.
- **Example**: Python

#### Compiled Languages
- **Definition**: Translated into machine code before execution.
- **Pros**: Faster execution.
- **Cons**: Longer compilation time, complex debugging.
- **Example**: C, C++

### Is JavaScript Interpreted or Compiled? 🤨
- **Answer**: JavaScript is **neither purely interpreted nor purely compiled**; it uses both techniques.
- **Interpreter**: Executes code quickly using an interpreter.
- **JIT Compilation**: Uses **Just-In-Time (JIT) Compilation** to optimize performance.

## 4. AST to Bytecode
- **Ignition**: The V8 engine’s interpreter converts AST into bytecode.
- **Bytecode Execution**: Ignition reads and executes bytecode line by line.

## 5. Just-In-Time (JIT) Compilation
- **TurboFan**: V8's compiler optimizes frequently executed (hot) code paths.
- **Optimization Process**:
  - Identifies frequently executed code.
  - Converts bytecode into optimized machine code.

## 6. Hot Code Optimization and Deoptimization

### Hot Code Optimization
- **Hot Code**: Code executed frequently.
- **Inline Caching**: Speeds up property access by caching lookup results.
- **Copy Elision**: Eliminates unnecessary object copying.

### Deoptimization
- **Scenario**: If TurboFan makes incorrect assumptions about code behavior, it **deoptimizes** the code.
- **Process**:
  - Sends the code back to Ignition for re-interpretation.
  - May be re-optimized later.
- **Best Practice**: Pass consistent types to functions to avoid deoptimization.

---
### Additional Resources
- **V8 Engine Bytecode Example**: [GitHub - V8 Bytecode](https://github.com/v8/v8/blob/master/test/cctest/interpreter/bytecode_exp)
- **V8 Documentation**: [V8.dev](https://v8.dev/)
- Full Documentation: [Full v8 doc](https://do6gp1uxl3luu.cloudfront.net/namaste-node/notes/Episode-08.pdf)

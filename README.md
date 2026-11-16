# Mini-AST (AST Builder Template)

This template sits between the Parser and the Semantic Analyzer in the compiler pipeline. It takes the concrete parse tree produced by ANTLR and transforms it into an **Abstract Syntax Tree (AST)** using the **Visitor Pattern**.

---

## Architecture

```text
Source File
       ↓
ANTLR Lexer & Parser (<GrammarName>Lexer.g4 / <GrammarName>Parser.g4)
       ↓
Concrete Parse Tree (CST / ParseTree)
       ↓
ASTBuilder (Visitor)
       ↓
Abstract Syntax Tree (AST Nodes: Program, Stmt, Expr, etc.)
       ↓
ASTPrinter / Semantic Checker / Code Generator
```

---

## Directory Structure

```text
mini-ast(ast builder)/
├── ast/                            # Object-oriented AST node definitions
├── visitor/                        # ASTBuilder & ASTPrinter visitors
├── utils/                          # ANTLR complete jar
├── tests/                          # Test programs
├── README.md                       # Documentation
└── .vscode/                        # Debug and editor configurations
```

---

## How to Build and Run

> **Template Placeholders:**
> * `<GrammarName>`: Base name of your grammar (e.g., `MyLang`).
> * `<TestFile>`: Path to your test input file (e.g., `tests/sample.txt`).

### 1. Generating ANTLR Parser Files (with Visitor Support)
* **WSL / Linux:**
  ```bash
  mkdir -p .antlr
  java -jar utils/antlr-4.13.1-complete.jar -visitor -no-listener -o .antlr <GrammarName>Lexer.g4 <GrammarName>Parser.g4
  ```
* **Windows (PowerShell):**
  ```powershell
  if (!(Test-Path .antlr)) { New-Item -ItemType Directory -Path .antlr }
  java -jar utils\antlr-4.13.1-complete.jar -visitor -no-listener -o .antlr <GrammarName>Lexer.g4 <GrammarName>Parser.g4
  ```

### 2. Compiling and Running
* **WSL / Linux:**
  ```bash
  javac -d .antlr -cp ".:utils/antlr-4.13.1-complete.jar" .antlr/*.java ast/*.java visitor/*.java Main.java
  java -cp ".antlr:utils/antlr-4.13.1-complete.jar" Main <TestFile>
  ```
* **Windows (PowerShell):**
  ```powershell
  javac -d .antlr -cp ".;utils\antlr-4.13.1-complete.jar" (Get-ChildItem .antlr\*.java, ast\*.java, visitor\*.java, Main.java)
  java -cp ".antlr;utils\antlr-4.13.1-complete.jar" Main <TestFile>
  ```
# mini-ast

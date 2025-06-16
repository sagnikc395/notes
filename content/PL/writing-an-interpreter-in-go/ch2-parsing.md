---
title: Parsing in Vanara
date: 16/5/25
tags:
  - vanara
  - parsing
  - parsing-algorithms
  - PL
  - interpreter
  - syntactic-analysis
---
### About Parsers
- Parser is a software component that takes input data (freqeuntly text) and builds a data structure - often some kind of parse tree, abstract syntax tree or other heirarchical structure 0 giving a structural representation of the input,checking for correct syntax in the process. The parser is often precedded by a seperate lexical anlyser, which creates tokens from the sequence of input characters.
- As software developers, we seldom get to see or interact with the parsed source code, with its internal repersentation. Lisp programmers are the exception to the rule - in Lisp, the data structures used to represent the source code are the ones used by Lisp user. The parsed source code is easily accessible as data in the program.
- In most interpreters and compilers the data structure used for the internal representation of the source code is called a 'syntax tree' or an 'abstract syntax tree' (AST). The 'abstract' is based on the fact that certain details visible in the source code are omitted in the AST. 
	- Semicolons, newlines, whitespace, comments, braces, bracket and parentheses -> depending on the language and the parser these details are not represented in the AST,but merely guide the parser when constructing it.
	- There is not one true, universal AST format that is used by every parser. Their implementations are all pretty similar, the concept is the same, but they differ in details. The concrete implementation depends on the programming language being parsed.
- Summary: Parsers take source code as inoput (either as text or tokens) and produce a data structure which represents this source code. While building up the data structure , they unavioidably analyze the input, checking that it confirms to the expected structure. Thus the process of parsing is also called syntactic analysis.

### About Parser Generators and why not them 
- Parser generators are tools like yacc,bison or ANTLR. These are tools that when fed with a formal description of a language, produce parsers as their output. This output is code that can then be compiled/ interpreted and itself fed with source code as input to produce a syntax tree.
- There exists many different parser generators, differeing in the format of the input they accept and the language of the output they produce. The majority of them use a Context-Free Grammar(CFG) as their input. A CFG is a set of rules that describe how to form correct(and also valid acc to syntax) sentences in a language. The most common notational formats of CFGs are the Backus Naur Form(BNF) or the Extended Backus-Naur Form(EBNF).
- Eg: EBNF for JS specification 
```ebnf 

 PrimaryExpression ::= "this"
                       | ObjectLiteral

                       | ( "(" Expression ")" )
                       | Identifier
                       | ArrayLiteral
                       | Literal

   Literal ::= ( <DECIMAL_LITERAL>
               | <HEX_INTEGER_LITERAL>

               | <STRING_LITERAL>
               | <BOOLEAN_LITERAL>
               | <NULL_LITERAL>
               | <REGULAR_EXPRESSION_LITERAL> )

   Identifier ::= <IDENTIFIER_NAME>
   ArrayLiteral ::= "[" ( ( Elision )? "]"

                    | ElementList Elision "]"
                    | ( ElementList )? "]" )
  ElementList ::= ( Elision )? AssignmentExpression
                   ( Elision AssignmentExpression )*

   Elision ::= ( "," )+
   ObjectLiteral ::= "{" ( PropertyNameAndValueList )? "}"
   PropertyNameAndValueList ::= PropertyNameAndValue ( "," PropertyNameAndValue

                                                     | "," )*
   PropertyNameAndValue ::= PropertyName ":" AssignmentExpression

   PropertyName ::= Identifier
                 | <STRING_LITERAL>

                 | <DECIMAL_LITERAL>              
```
- Why for using parser generator ?
	- Parsers are exceptionally well suited to being automatically generated. Parsing is one of the most well-understood branches of computer science and really smart people have already invested a lot of time into the problems of parsing. The results of their work are CFGH, BNF,EBNF etc.

- Why not parser generators ?
	- Purely for pedagogical reasons.
	- Also for the love of the game.

### Vanara Parser.
- In general, parsing a programming language has 2 main strategies:
	- top-down parsing 
		- Eg: recursive descent parsing, early parsing , predictive parsing are variants of top-down parsing 
	- bottom-up parsing 
		- Eg: LALR , table based parsing 
- Our parser for the Vanara project will be a recursive descent parser. In parrticular, it will be a 'top-down operator precedence' parser, also called as 'Pratt parser'.
- The main difference bw top-down and bottom up parsers is that the former starts with constructing root node of the AST node and then descends while the latter does it the other way around.
- When writing a parser ourselves we have to make some tradeoffs. 
	- Our parser wont be the fastest of all time.
	- We wont have formal proof of its correctness 
	- Error-Recovery process and detection of erroneous syntax wont be bullet-proof.
- It would be a full working parser, that is open for extension and improvements, easy to understand and a great start to further dive into the topic of parsing.


### Parsing let statements:
```vanara 
let x = 5;
let foobar = add(5,5);
let anotherName = barFoo;
```
- In Vanara, these stmts called as let statements, and bind a value to the given name. Our job in the parser for this, is to parse the let stmts correctly.
- parsing let stmts correctly means producing an AST that will accurately represents the information contained in the original let statement. 
- Vanara has the let binding of the following form:
```ebnf
let <identifier> = <expression>;
```
- ie. 2 changing parts : an identifier and an expression.
- Expressions produce a value, statements dont:
	- return 4; statements doesn't produce a value, whereas 5 does.
	- What exactly is an expression or an statement , what produces values and what doesn't depends on the programming language. 
	- Eg: In some languages function literals are expressions and can be used in any place where any other expression is allowed. In other programming languages though function literals can only be a part of a function declaration statement, in the toplevel of a program.

- In our AST, we have 3 interfaces, Node, Statement and Expression. Every node in our AST has to implement the Node interface, meaning it has to provide a TokenLiteral() methods that returns the literal value of the token it is associated with.
- AST that we are going to construct consists solely of Nodes that are connected to each other. Some of these nodes implement the Statement and some the Expression interface. These interfaces only contain dummy methods called statementNode and expressionNode. These aren't required but help us guide the Go compiler and possibly causing it to throw errors when we use a Statement where an Expression should have been used.
- `Program` node`(ast/ast.go)` is going to the root node of every AST our parser produces. Every valid Vanara program is a series of statements. These statements are contained in the `Program.Statements` , which is just a slice of AST nodes that implement the `Statement` interface.

- For our LetStatement Parser, it needs to able to point to any expression and can't just point to any literal value. And the the node also needs to keep track of the token the AST node is associated with, so we can implement the `TokenLiteral()` method.That makes 3 fields: one for the identifier, one for the expression that produces the value in the let statement and one for the token. `ast/letstmt.go`
- The identifier in a let stmt doesnt produce a value , so why is it an `Expression` ? To keep thing simple. Identifiers in other parts of a Vanara program do produce values. Eg: `let x = valueProducingIndentifier`, and to keep the number of different node types small, we'll use `Identifier` here to represent the name in a variable binding and later reuse it, to represent and identifier as part of or as a complete expression.


#### Parser's Fields:
- It has 3 fields: l, currToken and peekToken.
- l is a pointer to an instance of the lexer, on which we repeatedly call `NextToken()` to get the next token in the input.
- `currToken` and `peekToken` acts like 2 pointers our lexer has: `positon` and `peekPosition`. But instead of pointing to a character in the input they point to the current and the next token.
- `NewParser` is creating a new instance and `nextToken()` is a small helper that advances both the `currToken` and `peekToken` .

#### Recursive Descent Parsing:
- The basic idea behind recursive-descent parsing is that we start at an entry point `parseProgram` and it will construct the root node of the AST `newProgramASTNode()` and then build up the child nodes, the statements,bny calling other function that know which AST node to construct based on the current token.
- These other function will call each other again, recursively.
- The parser has to repeatedly advance the tokens and checks the current token to decide what to do next: either call another parsing function or throw an error. Each function then does its job and possibly construct an AST node so that the 'main loop' in `parseProgram()` can advance the tokens and decide what to do again.

#### Testing our Stub:
- Refer: [[testing-in-golang]]
- We provide Vanara source code as input and then set expectations on what we want the AST - produced by the parse - to look like. We do this by checking as many fields of the AST nodes as possible to make sure nothing is missing. 
- 2 noteworthy things about the tests:
	- We can ignore the `Value` field of the `*ast.LetStatement`. We'll check the value thing later, rn we need to make sure that the parsing of let statements works and ignore the Value.
	- Helper function `testLetStatement`. It might seem like over-engineering to use a seperate function, but we are going to need this function soon enough - and help to  make our test cases much more readble than lines and lines of type conversion strewn about.'


#### `ParseProgram method`
- First thing it does is construct the root node of the AST an `*ast.Program`. 
- It will then iterate over every token in the input until it encounters an token.EOF token. It does this by repeatedly calling nextToken, which advances both p.currToken and p.peekToken.
- In every iteration it calls parseStatement ,w hose job is to parse a statement.
- If parseStatement returned something other than nil, a ast.Statement its return valyue is added to Statements slice of the AST root node.
- When nothing is left to parse, the `*ast.Program` root node is returned.
- `parseLetStatement` is called when it encounters LET statements.
#### `parseLetStatement`
- It will construct an `*ast.LetStatement` node with the token its currently sitting on (a token. LET token) and then advance the tokens while making assertions about the next token with calls to `expectPeek`.
- First it will expect a token.IDENT token, which it will then use to construct an `*ast.Identifier` node. Then it expects an equal sign and finally it jumps over the expression following the equal sign until it encounters a semicolon.
- The skipping of expressions will be replaced, of course, as soon as we know how to parse them.
#### `expectPeek`
- This method is one of the 'assertion functions' nearly all parsers share.
- Their primary purpose is to enforce the correctness of the order of tokens by checking the type of the next token.
- Our `expectPeek` here will check the type of `peekToken` and only if the type is correct does it advance the tokens by calling `nextToken`.
#### `Errors()`
- which is just a slice of strings.
- This field gets initialized in `NewParser` and the helper function `peekError` can now be used to add an error to error when the type of `peekToken` doesn't match the expectation.
- With the `Errors` method we can check if the parser encountered any errors.
- `checkParserErrors` helper function does nothing more than check the parser for error and if it has any it will print them as test errors and stops the execution of the current test. 
- By changing `expectPeek` we can automatically add an error every time one of our expectations about the next token was wrong.

### Parsing Return Statements:
```ebnf 
return <expression>;
```
- Return stmt consist solely of the keyword return and an expression. That makes the definition of ast.ReturnStatement really simple.
- Like let stmt parsing, we will skip the parsing of the expression and the semicolon handling for now, but will come back to this later. The `statementNode` and `TokenLiteral` methods are there to fulfill the `Node` and `Statement` interfaces and look identical to the methods defined on `*ast.LetStatement`.
#### `parseReturnStatement()`
- Only thing it does is construct a `ast.ReturnStatement` with the current token its sitting on as `Token`. It then finally brings the parser in place for the expressions that comes next by calling `nextToken()` and finally , there's the cop-out./
- It will skip over every expression until it encounters a semicolon.
### Parsing Expressions:
- 
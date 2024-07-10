
- Lexing -> Parsing -> Semantic Analysis -> Optimization -> Code Generation 

- **Lexing**:
	- aka. lexical analysis ,tokenization, scanning 
	- text >> tokens("words")
	- foo = bar + 42;
	- chunk it into words that have meaning.

- Parsing:
	- extracts the input structure of the tokens that we have but we dont think of them as list of token, we think of them as adding 42 to bar and put the result into foo.
	- we want the result as a Abstract Syntax Tree -> hierarchy of operations.
	- catches syntax errors .
		- if x == 1 { System.out.println("ok");} // error in Java 
		- class Test { int x = y;} // not syntax error, cannot catch it.

- Semantic Analysis:
	- series of checks on AST.
	- 2 main types of checks -> name binding and type checking ,  other checking like flows etc.
	- **Type Checking** and also Type Checking.
	- 
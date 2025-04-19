### lexical analysis 

- we represent our source code in other forms that are easier to work with. We are going to change the representation of our source code 2 times before we evaluate it:
	- Source Code -> Tokens -> Abstract Syntax Tree 

- Transformations from source code to tokens -> lexical analysis or lexing for short. Its' done by a lexer(also called as a tokenizer or scanner).
- First transformation from source code to tokens, is called "lexical analysis" or "lexing" for short. It's done by a lexer (also called tokenizer or scanner).

- Tokens itself are small,easily categorizable data structures that are fed to the parser, which does the second transformation and turns the tokens into an "Abstract Syntax Tree".

- Whitespace characters don't show up as tokens.In our case that's okay, since whitespace length has no significance in Monkey language. Whitespace merely acts as a seperator for other tokens.

- A production-ready lexer might also attach the line number, column number and filename to a token. Why ? Eg: to later output more usueful error messages in the parsing stage. 

#### Defining our tokens:
- 
---
title: Lexing the Monkey Programming Language
draft: "true"
tags:
  - lexer
  - monkey-lang
date: 12/7/24
---
   
### Lexing 
- we represent our source code in other forms that are easier to work with. 
- we are going to change the representation of our source code 2 times before we evalute it.
	- source code -> tokens -> AST 
- **Lexical Analysis** -> transformations from source code to tokens / lexing.
	- Done by a lexer (also called as tokenizer / scanner)
- Tokens are the small , easily configurable data structures that are then fed to the parser, which does the second transformation and turns the tokens into an AST.
- what is a token varies between different lexer implementations.
- A thing to note here is that whitespace characters don't show up as tokens. It is because whitespace length is not significant in the Monkey lang. Whitespace will seperately act as seperator for other tokens.

### defining our tokens
- first we define the tokens our lexer is going to output. we are going to start with just a few tokens definitions and then add more when extending the lexer.
	- numbers like 5 and 10.
	- variable names like x,y ,add and result.
	- tokens like { , } etc.

- we call the variables as identifiers and treat them the same.

### token data structure:
- we need a type attribute for the token type , so that we can distinguish between integers and right bracket.
- also needs a field that holds the literal value of the token , so we can reuse it later and the information whether a number is a token.
- we define the TokenType type as a string. Helps us to use many different values as TokenTypes, which will allow us to disntinguish between different types of tokens.
- Easy to debug without a lot of boilerplate and helper functions, also can just print a string to check.
- Since there are a limited number of differnt token types, we can define the possible TokenType as constants.
	- Added 2 extra token types:
		- ILLEGAL -> signifies a token/character we dont know about 
		- EOF -> end of file , which tells us parser later on that it can stop.


### Lexer:
- It will take source code as input and will output the tokens that represents the source code. It will go through its input and output the tokens that represents the source code.
- It will go through its input and output the next token it recognizes. It doesn't need to buffer or save tokens, since there will only be one method called NextToken().
- Here, we will initialize the lexer with our source code and then repeatedly call NextToken() on it to go through the source code, token by token, character by character.
- We will also make life simpler here by using string as the type for our source code.
- 2 pointers for these two "pointers" pointing into our input string is in fact that we will need to be able to "peek" further into the input and look after the current character to see what comes up next.
- readPosition will always point to "next" character in the input, position will point to the character in the input that corresponds the the ch byte.
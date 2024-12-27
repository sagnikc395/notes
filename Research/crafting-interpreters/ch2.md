---
title: Map of the Territory
tags: 
date: 27/12/24
---
## Parts of the Language:

### Scanning:
- Scanning also known as lexing or lexical analysis. 
- Scanner takes in the linear stream of characters and chunks them together into a series of something more akin to "words". In programming languages, each of these words are called as token.
- Some characters in a source file doesnt actually mean anything. Whitespace is often insignificant and comments, by definition are ignore by the language.
### Parsing:
- Where our syntax gets a grammar - the ability to compose larger expressions and statements out of smaller parts. 
- Parser takes the flat sequence of tokens and builds a tree structure that mirrors the nested structure of the grammar. These trees are also called as parser tree or abstract syntax tree - depending on how close the bare syntactic structure of the source language they are.
- Parsers job also include letting us know when we do by reporting syntax errors.

### Static Analysis:
- Now the individual characteristiscs of each language start coming into play. At this point,we knwo the syntactic structure of the code - things like which expressions are nested in which, but we don't know much more than that.
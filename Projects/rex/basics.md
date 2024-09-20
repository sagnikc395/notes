---
title: rex -> a regex engine written from scratch in Go
tags:
  - automata-theory
  - golang
  - regex-engine
date: 20/9/24
---
## rex: Building a Regex engine from scratch 

### Background:
Recently I had a problem in one of our codebases where I was trying hard to parse the logic and write long code for the same, where my boss told me to simply use Regex. Huh! Totally forgot about that one. After fiddling and looking up syntax for the most part, I finally got a prototype and started reading more about regexes.

### Regex comes from Automata Theory
- Regex / Regular Expression's are just a notation to define a regular language.
- From the definition of regex, it only allows three operations:
	- Concatenation : ```ab``` , where it will match a followed by a b 
	- Alternation: ```(a|b)``` , where it will match a or b 
	- Kleene Star/Closure: ```a*``` , where it will match 0 or more a 
- Most of the modern regex engines allow an extended syntax for support for other operations like + , character matches , capture groups etc.
- Since a regex is language that can be recognized by a finite automata, to build a regex engine that can support and be extended, we just need to build a finite automata.
### Finite Automata and Regex:
- Automation is kinda like a state machine. It has a number of states and transitions that define the behaviour of the machine.
- It will read an input string one character at a time and each one makes the machine go through a transition.
	- Called as consuming a character -> since each character makes a single change in the machine.
	- Automation will recognize a regular language ``L`` if it is able to determine if any word ``w`` belongs to L.

### why finite ?
- 
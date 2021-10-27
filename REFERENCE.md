# Ztack reference manual

## Grammar

### Notation syntax

Ztack's reference grammar is written in a variation of Extended Backus-Naur Form (EBNF), which is defined as follows

```ebnf
grammar = { rule } ;

rule = identifier "=" expression ";" [ comment ] ;

expression = identifier | string_literal | group | optional | repetition | alternation | special_sequence ;

identifier = letter [ character ] ;
string_literal = """ any_character { any_character } """ ;
comment = any_character { any_character } ;

group = "(" expression ")" ; 
optional = "[" expression "]" ;               Can be used 0 or 1 times
repetition = "{" expression "}" ;             Can be used 0 or n times
alternation = expression { "|" expression } ;
special_sequence = "?" comment "?" ;          This sequence is used to describe the attributes of an expression in plain written language

letter = ? any spoken language character ? ;  e.g. "a".."z" or "A".."Z" in written English
character = ? any written character ? ;
any_character = ? any character, including whitespace and/or control characters ? ;
```

### Reference grammar

```ebnf
program = instruction { instruction } "end" ;

instruction = ( ( statement | expression ) whitespace { whitespace } ) | comment ;


statement = loop | conditional | operation | definition;

loop = ( "while" | "until" ) { statement } ";" ;
conditional = "if" { statement } [ "else" { statement } ] ;
operation = "dup" | "drop" | "swap" | "over" | "rot" | "." | "put" | "putstr" | "emit" | "cr" | "!" | "@" | "alloc" | "cells" ;


definition = variable_definition | constant_definition | word_definition ;

variable_definition = "variable" identifier ;
constant_definition = "constant" identifier ;
word_definition = "define" identifier { statement } ";" ;


expression = identifier | string_literal | number | mathematical_expression | comparative_expression | boolean_expression | "key" ;

mathematical_expression = "+" | "-" | "/" | "*" | "mod" ;
comparative_expression = ">" | "<" | "=" ;
boolean_expression = "and" | "or" | "invert" ;


identifier = letter { word_character } ;
string_literal = """ any_character { any_character } """ ;
number = digit { digit } ;
comment = "(" { any_character } ")" ;

word_character = letter | digit | underscore ;
any_character = ? any ASCII character ? ;

letter = ? any ASCII letter ? ;
digit = ? any ASCII digit ? ;
whitespace = ? any ASCII whitespace character ? ;
underscore = "_" ;
```

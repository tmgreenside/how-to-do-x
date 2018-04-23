# I want to do "X"

The following is a guide for how to get started with programming side projects. If something's missing and you know about it, feel free to submit a pull request and add it.

## Mobile Apps

## Linux

## Machine Learning

## Security

## Desktop apps

## Video Games and Computer Graphics

## Frontend Web

## Backend Web

## Infastructure and AWS

## Building Programming Languages

### Overview

Building languages is not as hard as it may appear! In general, the key concepts are:

* [Grammars](https://en.wikibooks.org/wiki/Introduction_to_Programming_Languages/Grammars), or the formal structure of a language.
* Lexing, or the conversion of text into abstract "tokens" that can be used in the grammar. For example, most languages convert the `+` into a `PLUS` token.
* [Parsing](https://en.wikibooks.org/wiki/Introduction_to_Programming_Languages/Parsing), or the conversion of "tokens" (pieces of a language) into an [Abstract Syntax Tree](http://azu.github.io/slide/JSojisan/resources/ast-is-true.png).

### First Project

A good first project is to build a calculator that can compute things like this:

```
1 + 2 * 5
```

#### Step 1: Write a grammar

You should probably write this in [EBNF form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form). It doesn't need to have the exact same syntax, but it's useful to understand the conventions.

To get you started, here's a partial grammar for the calculator:

```
add: add '+' add | NUM.
NUM: [0-9].

// TODO: Rest of the grammar
```

Notice that grammars are written as recursive "rules". In the example above, the string `1 + 2` would enter the `add` rule, then recurse till it matched the `NUM`.

#### Step 2: Write a lexer

The easiest way to do this is to use [regular expressions](https://regexr.com/). If you've never used regular expressions before or are generally scared of them, you're also welcome to parse out by iterating through characters.

Don't worry too much about doing it the "right" way at the moment, just focus on getting something working.

You'll typically define your tokens as an `enum` or your language's equivalent.

```javascript
enum Tokens = (
  PLUS,
  NUM
);

function lex(code) {
  let tokens = []

  // TODO: if parse out a '+'
  tokens.push(Tokens.PLUS)

  // TODO: if parse out a number
  tokens.push(Tokens.NUM)

  return tokens
}
```

#### Step 3: Write a parser

The common way to do this is with a [recursive descent parser](http://weblog.jamisbuck.org/2015/7/30/writing-a-simple-recursive-descent-parser.html). This is where your grammar will come in handy.

Your goal here is to create an Abstract Syntax Tree (AST), which is just a tree of your grammar rules!

Each node of the tree should have two values, the type and an optional value.

For example:

```javascript
class Node {
  this.value;    // Any type
  this.type;     // A token or rule name
  this.children; // Other nodes
}
```

When complete, your tree will look a lot like your grammar:

```
# An example input
1 + 2

# An example lexed output
(NUM, 1) PLUS (NUM, 2)

# An example tree
add
  - NUM, 2
  - PLUS, nil
  - NUM, 2
```

The general way people do this is by creating a number of functions corresponding to their rules that "accept" a token and build the part of the tree.

You'll probably want a "look ahead" that checks the next token in the sequence.

```javascript
function add() {
  if (lookahead == Tokens.PLUS) {
    // TODO: add an `add` node to tree and recurse!
    add();
    plus();
    add();
    return;
  }

  // Otherwise, we're a number!
  num();
  return;
}

function num() {
  // TODO: add a num node to tree
  return;
}
```

#### Step 4: Build an interpreter

Now that we have an Abstract Syntax Tree (AST), we can perform a [depth first search](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) and evaluate each node.

To start, let's give an example tree:

```
add
  - NUM 2
  - PLUS, nil
  - NUM 3
```

We typically build our interpreter similar to how we built our recursive descent parser; we build it with functions. Except this time, our functions can visit each child node and return a value.

For example:

```javascript
function visit(node) {
  // TODO: search down the tree until we get to a num and then return
  // that value
}

function visitAdd(node) {
  return visit(node.add[0]) + visit(node.add[0]);
}

function visitNum(node) {
  return node.value;
}
```

### Where to go from here

The world of programming languages is really, really big.

#### Compiler Compilers!

If you went through and built that recursive descent parser and found it to be a little tedious, you're in luck! There's options for auto-generating a recursive descent parser from a grammar.

* [Antlr](http://www.antlr.org/) is my personal favorite!
* [Yacc, Lex, and Bison](http://dinosaur.compilertools.net/)

#### Formal grammars

Many bugs you've faced can come down to ambiguities in your grammar. Having a better understanding of the different types of grammars and parsers and how they're defined can really help you.

* [LL(n)](https://en.wikipedia.org/wiki/LL_parser)
* [LALR](https://en.wikipedia.org/wiki/LALR_parser)
* [PEG](https://en.wikipedia.org/wiki/Parsing_expression_grammar)

### Example projects

#### A Portfolio Language

Build a language like markdown that creates portfolio websites for you!

#### Code Generators

Create an AST generator for an existing language and use that to generate code for the language.

#### AST Formatter

Create a formatter that takes an existing programming language, converts it to an AST, then reprints it the correct style.

#### Build a simple scripting language

Build another language in your favorite language! Add variables, functions, arrays, and more!

## Learning specific programming languages

### Ruby

### C++

## Functional Programming

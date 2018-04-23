# I want to do "X"

The following is a guide for how to get started with programming side projects. If something's missing and you know about it, feel free to submit a pull request and add it.

## Mobile Apps

## Linux

## Machine Learning

## Security
### Overview
Security itself is a very broad topic, as it encapsulates every app, website, backend or anything else very created that can be seen. Understanding basic security concepts for different types of applications is essential to make a good app. For instance, when using a backend database it's very important to use prepared statements with parameters. Otherwise, information could be stolen from the database, which makes a frowny face.

### First Steps
Read!  
REad!  
REAd!  
READ!  
Listen!  
LISTEN!  
Everyone starts at the bottom of the totem pole; but we've all got to get started at some point!  
Great resources to read/listen from:  

-
[Security Now](https://twit.tv/shows/security-now), is the best security podcast that discusses anything from updates in https, TLS and other things to recent hacks that have happened in the industry. Steve Gibson hosts this, with Leo creates more dialog. For a security podcast, it's quite entertaining!  
- [Krebs On Security](https://krebsonsecurity.com/), is one of the best blogs that a person can stay up-to-date with. He's the first to know about security breaches and other things in the industry. He usually has great posts about every 3 days on something new.  
- [List of Blogs](https://heimdalsecurity.com/blog/best-internet-security-blogs/) This is a list of computer security blogs that all serve a valuable purpose. However,there are thousands of other blogs and people willing to talk about things! So, find what fits you.

If the path is just understanding how to build solid and secure applications then just repeat the above until the end of time. However, if you want to get into the security business there's much, much more to follow!  

### First Project  
The first step to do some hacking or security based project is understanding the technology quite well to start with. So, it's very vital to pick a technology that you consider yourself very familiar with. For the purpose of this, I will pick SQL(structured query language) because of how widely used it is. SQL a language used to store and access information in a unified way. Further knowledge can be found at: [Learning MYSQL](https://www.digitalocean.com/community/tutorials/a-basic-mysql-tutorial) has a good description of how manipulate tables. Further, [Querying and More](https://www.w3schools.com/sql/) teaches basic querying and things. For the purposes of this, and most things you'll ever need to do, just learn how to alter, create and delete tables. Then, understanding what SELECT, FROM, and WHERE are all capable of is enough. After understanding these few things, databases are simple.

#### Step 1
Setting up a database is very, very important in order to use a database! So, this is step 1. It's recommended that this is done on a unix-y system, like Linux or MAC.  
[Setup MySQL](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-14-04)  
This links does a great job at getting the database set up locally.

#### Step 2
For the sake of the project, let's use a login screen for this. So, a basic 'table' can be used for this, representing the application. In the table, we will only have two columns:
username and password. This implementation is in Python.
The table will simply look like:

| __username__ | __password__ |
|   theGUman   |  123456789   |
|    Spike     |     Woof     |

-------  MAX, add it to your github.

#### Step 3
Here's the fun part: time to just mess around, read around and have fun with it! So, now that the authentication process works, now what? Well, the schema above has some major issues with it...
- Passwords: Seem funky that the databases are stored by itself in plain text? Well, you were right! What happens in practice is what are called 'one-way hash functions' are used to encrypt the information. A one-way hash function is a way to jumble up data so that it's impossible to go back to the original value. This is used because it can be used to **validate** whether a password is correct, without the database actually storing the password.
- Privileges: Within databases, as in everything are different types of users, which can do different actions. This can limit  

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

### First Steps

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

## Learning specific programming languages

### Ruby

### C++

## Functional Programming

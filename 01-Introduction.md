# 1. Introduction

Rant is a multi-paradigm, domain-specific language designed for concisely defining templates for procedural text generation. It borrows concepts from imperative, functional, and markup languages, and also contains an embedded scripting language known as "Richard". One of the most notable characteristics borrowed by Rant from conventional markup languages (e.g. HTML and Markdown) is that plain text counts as a valid Rant program, or "pattern". Tags, queries, escape sequences, and other dynamic elements can be used to control how the final output is generated.

One of the most unique features of the language is that it relies heavily on randomness to determine the behavior of many of its functions, notably queries and branches. A seed value can be passed to a Rant interpreter to control which random output is returned. Additionally, Rant can be provided with an existing random number generator instance if the user so desires.

This chapter will provide a brief overview of the features Rant has to offer.

## 1.1 Getting Started

A "Hello World" program in Rant is simply the text written as follows:

```rant
Hello, World
```

This will print the text "Hello, World" to the output and terminate the pattern.

### File Conventions

Rant patterns are typically stored in a plain text file with the extension `.rant` or `.rants`. Each of these extensions are used for something different, but they both contain the same kind of information. When in doubt, just use `.rant` to store patterns.

#### .rant
A file with the extension `.rant` stores a regular pattern. This refers to any pattern that outputs one or more channels (channels will be discussed later on). This is the default extension that should be expected by Rant interpreters.

#### .rants
The `.rants` extension denotes a *serial pattern*. This is still Rant code, but it is written in a way that causes it to to return multiple sequential outputs via the `[yield]` function. It is intended to provide a hint to programs supporting the extension that the pattern contained in the file requires the serial execution pipeline. It otherwise does not affect the pattern's behavior, and a serial pattern placed in a regular `.rant` file will still run (albeit incorrectly).

## 1.2 Tags

Tags are the most common way of adding functionality to a pattern. The term "tag" encompasses a number of different language elements, but they all share the characteristic of being enclosed in a pair of brackets.
```
some text [ tag ] some more text
```
The tag types are as follows:

### Functions
Functions are built-in, named operations which perform a task at the point in the pattern where they are placed. Some functions require arguments and some do not. There are quite a lot of functions available, but here are a few examples of how they can be used:

```rant
[case:upper]this will print in uppercase
```
```rant
[rep:10]Hell{o}!
```
```rant
I am [num:10;100] years old.
```

### Subroutines

Subroutines are user-defined functions whose logic is defined as a pattern. Subroutines can also accept arguments and be called similarly to built-in functions, with the exception that subroutines must be distinguished with a `$` prefix.

```rant
[$[greet:name]:
  Hello, [arg:name]!
]

[$greet:Berkin]
```
This outputs the following:
```
Hello, Berkin!
```

### Replacers

Replacers use regular expressions to match and replace substrings in a given input and print the final result. The replacement is defined by a pattern, so the each individual match may end up being replaced by something different, depending on the replacement pattern.

Here is an example of a replacer that repeats every vowel twice:
```rant
[`[aeiou]`:The quick brown fox jumps over the lazy dog.;[match][match]]
```
The output looks like this:
```
Thee quuiick broown foox juumps ooveer thee laazy doog.
```

### Richard scripts

Richard scripts (discussed later) are embedded inside of a tag that starts with the `@` symbol.

```rant
[@ 1 + 1]
```
```
2
```

## 1.3 Blocks

Blocks are sections of a pattern, consisting of one or more sequential parts, which are subject to branching behavior. Blocks are surrounded with braces.
```rant
{ block }
{
  multiline block
}
```
Separate branches of a block are delimited by the pipe character:
```rant
{ A | B | C | D | E }
```
Blocks can also be nested:
```rant
{
  { 1A | 1B | 1C }
  |
  { 2A | 2B | 2C | 2D }
  |
  { 3A | 3B | 3C | 3D | 3E }
}
```
The default behavior of a block is to randomly execute one of the items, however, this behavior can be modified through functions and other methods discussed later on.

## 1.4 Queries

Rant's query engine is one of its most powerful features. Queries allow Rant to interact with and retrieve data from an external dictionary to integrate a large vocabulary into outputs. Queries provide advanced filtering options that make it possible to achieve a variety of complex behaviors such as word association, comparisons, gender agreement, and even rhyming.

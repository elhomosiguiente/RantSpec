# The Rant Language Specification

#### Version 3.0

_**Fair warning**: This specification is a work-in-progress and should not be used as an official reference (yet)._

## Table of Contents

* [1 - Introduction](01-Introduction.md)
  * [1.1 - Getting Started](01-Introduction.md#11---getting-started)
  * [1.2 - Tags](01-Introduction.md#12---tags)
  * [1.3 - Blocks](01-Introduction.md#13---blocks)
  * [1.4 - Queries](01-Introduction.md#14---queries)
  * [1.5 - Richard](01-Introduction.md#15---richard)
* [2 - Basic Elements](02-Basic-Elements.md)
  * [2.1 - Text & Whitespace](02-Basic-Elements.md#21---text--whitespace)
  * [2.2 - Comments](02-Basic-Elements.md##22---comments)
  * [2.3 - Escape Sequences](02-Basic-Elements.md#23---escape-sequences)
  * [2.4 - Constant Literals](02-Basic-Elements.md#24---constant-literals)
  * 2.5 - Blocks
* 3 - Functions
  * 3.1 - Built-In Functions
  * 3.2 - Subroutines
    * 3.2.1 - Parameter Types
    * 3.2.2 - Argument Access
* 3 - Matching & Replacing
  * 3.1 - Regular Expressions
  * 3.2 - Replacers
* 4 - Queries
  * 4.1 - Tables
  * 4.2 - Subtypes
  * 4.3 - Filters
    * 4.3.1 - Class Filters
      * 4.3.1.1 - Exclusivity
    * 4.3.2 - Regex Filters
    * 4.3.3 - Syllable Count Filter
    * 4.3.4 - Rank Filters
  * 4.4 - Carriers
    * 4.4.1 - The `=` Operator (Match)
    * 4.4.2 - The `!` Operator (Unique)
    * 4.4.3 - The `@` Operator (Association)    
    * 4.4.4 - The `@=` Operator (Match-Association)
    * 4.4.5 - The `@!` Operator (Dissociation)
    * 4.4.6 - The `@!=` Operator (Match-Dissociation)
    * 4.4.7 - The `@+` Operator (Divergence)
    * 4.4.8 - The `@+=` Operator (Match-Divergence)
    * 4.4.9 - The `@?` Operator (Relation)
    * 4.4.10 - The `@?=` Operator (Match-Relation)
    * 4.4.11 - The `!=` Operator (Mismatch)
    * 4.4.12 - The `&` Operator (Rhyme)
    * 4.4.13 - The `^=` Operator (Rank Match)
    * 4.4.14 - The `^!` Operator (Rank Mismatch)
    * 4.4.15 - The `^>` Operator (Rank Greater Than)
    * 4.4.16 - The `^<` Operator (Rank Less Than)
    * 4.4.17 - The `^>=` Operator (Rank Greater Than or Equal)
    * 4.4.18 - The `^<=` Operator (Rank Less Than Or Equal)
  * 4.5 - Query Macros
    * 4.5.1 - Partial Macros
  * 4.6 - Deferred Queries
* 5 - Scripting
  * 5.1 - Types
  * 5.2 - Variables
  * 5.3 - Operators
  * 5.4 - Functions
  * 5.5 - Control Flow
    * 5.5.1 - The If Statement
    * 5.5.2 - The While Loop
    * 5.5.2 - The For Loop

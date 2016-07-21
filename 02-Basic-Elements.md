# 2. Basic Elements

This chapter provides information on the static (non-changing) aspects of the langauge, how whitespace and other non-essentials are handled by the compiler, and blocks (branching).

## 2.1 - Text & Whitespace

### Text

Text is only text and nothing more. A pattern that is just some text will just print some text. For example, that sentence will work as a pattern.

```rant
A pattern that is just some text will just print some text.
```

There are some exceptions to this, of course, and those are **whitespace** and **reserved characters**. In a top-level context (not inside any kind of tag, query, or other semantic element), certain characters are not allowed because they are used by the language itself. Here is a list of reserved top-level characters:

```
[
]
<
>
{
}
#
\
`
"
```

Most lower contexts impose further restrictions on allowed characters. It is generally a safe and encouraged practice to simply escape all special characters that are intended to be literally printed. Escaping will be discussed in detail farther along in this chapter.

### Whitespace

Only whitespace between non-whitespace characters will be acknowledged. This means line breaks are ignored. This also means that indentation is ignored. You can indent a pattern one million spaces and it will still give the same output. The only difference is that people will think you're ridiculous for indenting that much.

As an example, consider these three lines of text. They will print exactly the same thing.
```rant
Hello, world!
    Hello, world!
        Hello, world!
```

These three lines, however, will print differently:
```rant
Hello, world!
Hello,  world!
Hello,   world!
```

Notice the difference here. In the first example, the difference in whitespace is at the beginning of the line. Since it is not surrounded on both sides by non-whitespace characters, it is ignored. *(The same rule applies also for whitespace at the end of lines, and before comments.)*

On the other hand, the whitespace in the second example occurs between two words. Consequentially, it is printed verbatim. Such is Rant.

#### Line breaks

To print a line break to the output, an escape sequence, such as `\n` or `\N`, must be used. Actual line breaks will be ignored.

## 2.2 - Comments

Rant uses Python-style comments that start with a `#` character. Comments span from the point of this character to the end of the line on which it occurs.

Here are a few examples of comment usage:

```rant
# This is a comment
```

```rant
[rep:10] # Repeat ten times
[sep:\s] # Separate with spaces
{
  Beep|
  Boop|
  Bleep|
  Bloop
}
```

## 2.3 - Escape Sequences

Escape sequences are used to print reserved characters or characters that can't be typed with a normal keyboard. They can also be used to generate random characters of different types, like decimal digits and letters. Escape sequences may appear in any place where plain text is allowed.

There are two types of escape sequences: **simple** and **quantified**.

A **simple** escape sequence begins with a backslash (`\`) character, followed by an **escape code**. The escape code determines what kind of character is printed, and is usually one character long (the one exception to this rule is `\uXXXX`). Some escape codes literally print themselves, like braces. Some have special behaviors, for example, line feed (`\n`) and carriage return (`\r`). Some may print more than one character, such as the system-specific line separator (`\N`). Any special character (that is not whitespace) can be escaped.

Below are a few examples of simple escape sequences:

```rant
This\ntext\nspans\nmultiple\nlines.

# You can split them by line for easier reading if you want.
This\n
text\n
spans\n
multiple\n
lines.

# Separate these words by spaces
[repeach][sep:\s][x:_;ordered]{Rant|is|awesome!}

# Escaping special characters
\<These angle brackets will print just fine.\>
```

A **quantified** escape sequence includes an additional argument that instructs Rant to repeat the desired character a certain number of times.

The structure for a quantified escape sequence is slightly different. Instead of the escape code immediately following the `\` character, first must come a positive, nonzero integer indicating the number of characters to generate. Following this must be a comma, followed by the regular escape code.
```
\COUNT,CODE
```

This example shows how a quantified escape sequence can be used to generate a random hexadecimal string:
```rant
\64,x
```

### Supported Escape Codes

|Code|Character|
|----|---------|
|`\a`|English indefinite article|
|`\N`|System-specified line separator _(may be more than one character)_ |
|`\n`|Line feed (0x0A)|
|`\r`|Carriage return (0x0D)|
|`\v`|Vertical tab (0x0B)|
|`\b`|Backspace (0x08)|
|`\s`|Space (0x20)|
|`\c`|Random lowercase letter|
|`\C`|Random uppercase letter|
|`\d`|Random decimal digit|
|`\D`|Random nonzero decimal digit|
|`\w`|Random lowercase alphanumeric character|
|`\W`|Random uppercase alphanumeric character|
|`\x`|Random lowercase hexadecimal digit|
|`\X`|Random uppercase hexadecimal digit|
|`\uXXXX`|UTF-16 character (replace `XXXX` with the hex code of the desired character)|

## 2.4 - Constant Literals

Some situations may require the user to print a large number of special characters in a row. Escaping every individual character would be both tiresome and a waste of space; therefore, another solution exists: the **constant literal**.

A constant literal collectively escapes a group of distinct characters. They are created by surrounding the desired string with double-quotes (`"`).

To give an example, consider this set of escape sequences below.
```rant
\{\<\[example\]\>\}
```

This is quite long and can be difficult to read. Here is the same pattern using a single constant literal instead of escape sequences:
```rant
"{<[example]>}"
```

Both of these patterns output the following:
```
{<[example]>}
```

To use double-quotes inside of a constant literal, simply use two double-quotes in a row, like so:
```rant
"This is some text with ""quotation marks"" in it."
```

Constant literals literally print everything inside of them (with the exception of the double-quote rule). This means that even line breaks work inside of them.

```rant
"Constant literals
Compressed escape sequences
For your sanity"
```
This outputs the following:
```
Constant literals
Compressed escape sequences
For your sanity
```

## 2.5 - Blocks

One of the fundamental ideas of procedural generation is some degree of randomness, and Rant uses **blocks** to facilitate randomized diversions in the generation of textual output. A block is essentially a fork in the generation path, allowing the generator to choose one of several paths of execution to create highly varied end results. Blocks can be nested, weighted, repeated, and many other things that will be detailed further in this document. Firstly, an overview of the structure and basic usage of blocks shall be provided.

A block consists of one or more **elements** contained within a **scope**, which defines the block's execution context. The scope of a block is always denoted by a pair of braces:
```rant
{ ... content here ... }
```
Multiple elements are separated by the pipe character:
```rant
{ A | B | C | D | E }
```
Unescaped whitespace is trimmed from the beginning and end of each element in a block.

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

Notice the difference here. In the first example, the difference in whitespace is at the beginning of the line. Since it is not surrounded on both sides by non-whitespace characters, it is ignored. *(The same rule applies also for whitespace at the end of lines.)*

On the other hand, the whitespace in the second example occurs between two words. Consequentially, it is printed verbatim. Such is Rant.

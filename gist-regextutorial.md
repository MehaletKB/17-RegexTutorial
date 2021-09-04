# 17-Regex Tutorial

Using regex to validate Youtube links.

## Summary

The regular expression interpreted here will be the following: 
<pre><code>/^(?:https?:\/\/)?(?:www\.)?(?:youtube\.com\/watch\?v=([a-zA-Z0-9_]+)|youtu\.be\/([a-zA-Z\d_]+))(?:&.*)?$/gm</code></pre>

This expression is used to validate Youtube urls which are not uniform. The following links all take us to the same (imo) hilarious video:

    https://www.youtube.com/watch?v=z_SKgkg6ltQ
    https://youtube.com/watch?v=z_SKgkg6ltQ
    https://youtu.be/z_SKgkg6ltQ


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)
- [Regex Explanation](#regex-explanation)

## Regex Components
A regular expression (regex) is a string that is considered to be a literal, and so must be wrapped in ``/`` characters.

### Anchors:
The ``^`` and ``$`` characters are known as anchors. <br>

- ``^`` signifies a string that begins with the characters that follow it (except when in ``[]``, in which case ``^`` will be a negation)

- ``$`` signifies a string that ends with the characters that precede it 

In our example the string must start with something that matches this pattern: `(?:https?:\/\/)`. <br>
We do not include the ending pattern here because the ``?`` before the ``$`` anchor is a quantifier (see below).

### Quantifiers:
Quantifiers set the limits of the string that a regex matches. They are inherently greedy, meaning they match as many occurrences of a pattern as possible.

In our examples we find the following quantifiers:
- ``+`` matches the previous token or pattern one or more times
- ``?`` matches the previous token or pattern zero or one time 
- ``*`` matches the previous token or pattern zero or more time 

### Grouping Constructs:
Complex regular expressions at times need to be broken into multiple parts to determine whether different sections fulfill different requirements. Grouping constructs are used to break the string into sections.

The primary way to group a section is by using parentheses. Sections within ``(())`` are known as subexpressions.
Subexpressions look for an exact match unless they're told otherwise.

Grouping constructs have two primary categories: **capturing** and **non-capturing**. A grouping construct can be made non-capturing by adding ``?:`` at the beginning of an expression inside the ``()``.

In our example every subexpression is a non-capturing grouping construct, meaning they don't capture the matched character sequences.

### Bracket Expressions:
Bracket expressions outline characters we want to include. Anything inside a set of ``[]`` represents a range of characters that we want to match.

In our example we find the following bracket expressions:
- ``[a-zA-Z0-9_]`` can include any lowercase letter, any uppercase letter, any numerical digit and the ``_`` character
- ``[a-zA-Z\d_]`` can include any lowercase letter, any uppercase letter, any numerical digit and the ``_`` character

### Character Classes:
A character class defines a set of characters. An example of this is the bracket ``[]`` expressions discussed above. Other character classes we find in our example are the following:
- `*` matches any character except the newline character `\n`
- ``\d`` matches any numerical digit (equivalent to ``[0-9]``)

### The OR Operator:
The OR operator uses the ``|`` character to verify whether one criteria or another is satisfied. <br>
In our example we check weather ``youtube\.com\/watch\?v=([a-zA-Z0-9_]+)`` or ``youtu\.be\/([a-zA-Z\d_]+)`` is valid by separating the two sections with a `|` character.

### Flags:
Flags are placed at the end of a regex, they define additional functionality or limits for the regex. They can be used alone or can be combined.<br>
In our example we find the following flags:
- `g` global search, meaning the regex should be tested against all possible matches in the string
- `m` multi-line search, meaning a multi-line input string should be treated as multiple lines.

### Character Escapes:
The ``\`` character in a regex escapes a character that otherwise would be interpreted literally.<br>
In our example every time there is a ``\`` before a character, it means that the regex should look for that literal character instead of executing it's function within the regex context.

### Regex Explanation:
Let's now apply all our knowledge to interpret our regex!
<pre><code>/^(?:https?:\/\/)?(?:www\.)?(?:youtube\.com\/watch\?v=([a-zA-Z0-9_]+)|youtu\.be\/([a-zA-Z\d_]+))(?:&.*)?$/gm</code></pre>

**Non-captured group** ``(?:https?:\/\/)``:<br>
`http` matches the characters http literally<br>
`s` matches the character s literally<br>
`:` matches the character : literally<br>
`\/` matches the character / literally<br>
`\/` matches the character / literally<br>
<br>

**Non-capturing group** ``(?:www\.)?``:<br>
`?` matches the previous token between zero and one times, as many times as possible, giving back as needed <br>
`www` matches the characters www literally<br>
`\.` matches the character . literally<br>
<br>

**Non-capturing group** ``(?:youtube\.com\/watch\?v=([a-zA-Z0-9_]+)|youtu\.be\/([a-zA-Z\d_]+))``:<br>

1st Alternative ``youtube\.com\/watch\?v=([a-zA-Z0-9_]+)``:<br>
`youtube` matches the characters youtube literally<br>
`\.` matches the character .literally<br>
`com` matches the characters com literally<br>
`\/` matches the character /literally<br>
`watch` matches the characters watch literally<br>
`\?` matches the character ? literally<br>
`v=` matches the characters v= literally<br>

1st Capturing Group ``([a-zA-Z0-9_]+)``:<br>
``+`` matches the previous token between one and unlimited times, as many times as possible, giving back as needed <br>
`a-z` matches a single character in the range between a and z<br>
`A-Z` matches a single character in the range between A and Z<br>
`0-9` matches a single character in the range between 0 and 9<br>
`_` matches the character _ literally<br>

2nd Alternative ``youtu\.be\/([a-zA-Z\d_]+)``:<br>
`youtu` matches the characters youtu literally<br>
`\.` matches the character . literally<br>
`be` matches the characters be literally<br>
`\/` matches the character / literally<br>

2nd Capturing Group ``([a-zA-Z\d_]+)``:<br>
`+` matches the previous token between one and unlimited times, as many times as possible, giving back as needed <br>
`a-z` matches a single character in the range between a and z<br>
`A-Z` matches a single character in the range between A and Z<br>
`\d` matches any numerical digit<br>
`_` matches the character _ literally<br>
<br>

**Non-capturing group** ``(?:&.*)?``:<br>
`?` matches the previous token between zero and one times, as many times as possible, giving back as needed <br>
`&` matches the character & literally<br>
`.` matches any character (except for line terminators - `\n`, `\r` etc.)<br>
`*` matches the previous token between zero and unlimited times, as many times as possible, giving back as needed <br>
`$` asserts position at the end of a line<br>
<br>

**Global pattern flags**:<br>
`g` modifier: global. All matches (don't return after first match)<br>
`m` modifier: multi line. Causes `^` and `$` to match the begin/end of each line (not only begin/end of string)<br>

## Author

Mehalet KesateBirhan <br>
https://github.com/MehaletKB

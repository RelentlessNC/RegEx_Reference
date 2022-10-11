# RegEx Email Finder

This is a tuturoial on how to use Regular Expressions to find email addresses in text.

## Summary

In this tutorial, I will be showing you how to use the regular expression below to search text for all email addresses.

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

Anchors are unique in that they match a position within a string, not a character.

`\B` **Not Word Boundary**
 : *example: `s\B`*
 : The `\B`Matches any position that is not a word boundary. This matches a position, not a character.

`\b` **Word Boundary**
: *example: `s\b`*
: The `\b` Matches a word boundary position between a word character and non-word character or position (start / end of string). See the word character class `(w)` for more info.

`^` **Beginning Anchor**
: *example: `^\w+`*
: The `^` matches the beginning of the string, or the beginning of a line if the multiline flag `(m)` is enabled.  This matches a position, not a character.

`$` **End Anchor**
: *example: `\w+$`*
: The `$` matches the end of the string, or the end of a line if the multiline flag `(m)` is enabled.  This matches a position, not a character.

---

In my expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` notice we have a `^`, which means we are looking for the character set `([a-z0-9_\.-]+)` at the beginning of the string.

In my expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` notice we have a `$`, which means we are looking for the character set `([a-z\.]{2,6})` at the end of the string.

### Quantifiers

`+` **Plus**
: *example: `b\w+`*
: Matches 1 or more of the preceding token.

`*` **Star**
: *example: `b\w`*
: Matches 0 or more of the preceding token.

`{}` **Quantifier**
: *example: `{1,3}`*
: Matches the specified quantity of the previous token. `{1,3}` will match 1 to 3. `{3}` will match exactly 3. `{3,}` will match 3 or more.

`?` **Optional**
: *example: `colou?r`*
: Matches 0 or 1 of the preceding token, effectively making it optional.

`?` **Lazy**
: *example: `b\w+?`*
: Makes the preceding quantifier lazy, causing it to match as few characters as possible. By default, quantifiers are greedy, and will match as many characters as possible.

---

In my expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` there is a single quantifier at the end which is looking for 2-6 characters in length and those characters can be letters *a-z* and a *dot* (.).

### OR Operator

`|` **Alternation**
: *example: `b(a|e|i)d`*
: Acts like a boolean OR. Matches the expression before or after the |. It can operate within a group, or on a whole expression. The patterns will be tested in order.

### Character Classes

`[ABC]` **Character Set**
: *example: `[aeiou]`*
: Match any character in the set.

`[^ABC]` **Negated Character Set**
: *example: `[^aeiou]`*
: Match any character that is not in the set.

`[A-Z]` **Range**
: *example: `[g-s]`*
: Matches a character having a character code between the two specified characters inclusive.

`.` **Dot**
: Matches any character except linebreaks. Equivalent to `[^\n\r]`.

`[\s\S]` **Match Any**
: A character set that can be used to match any character, including line breaks, without the dotall flag `(s)`.
An alternative is `[^]`, but it is not supported in all browsers.

`\w` **Word**
: Matches any word character (alphanumeric & underscore). Only matches low-ascii characters (no accented or non-roman characters). Equivalent to `[A-Za-z0-9_]`.

`\W` **Not Word**
: Matches any character that is not a word character (alphanumeric & underscore). Equivalent to `[^A-Za-z0-9_]`.

`\d` **Digit**
: Matches any digit character (0-9). Equivalent to `[0-9]`.

`\D` **Not Digit**
: Matches any character that is not a digit character (0-9). Equivalent to `[^0-9]`.

`\s` **Whitespace**
: Matches any whitespace character (spaces, tabs, line breaks).

`\S` **Not Whitespace**
: Matches any character that is not a whitespace character (spaces, tabs, line breaks).

`\p{L}` **Unicode Category**
: Matches a character in the specified unicode category. For example, `\p{Ll}` will match any lowercase letter.
: Requires the `u` flag.
: For a list of values, see this [MDN page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes).

`\P{L}` **Not Unicode Category**
: Matches any character that is not in the specified unicode category.
: Requires the `u` flag.
: For a list of values, see this [MDN page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes).

`\p{Han}` **Unicode Script**
: Matches any character in the specified unicode script. For example, `\p{Arabic}` will match characters in the Arabic script.
: Requires the u flag.
: For a list of values, see this [MDN page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes).

`\P{Han}` **Not Unicode Script**
: Matches any character that is not in the specified unicode script.
: Requires the `u` flag.
: For a list of values, see this [MDN page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes).

---

In my expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, the following character classes are used.

`[a-z0-9_\.-]`
: This particular character set is looking for any letter a-z or any number 0-9 or an underscore(_), or a dot(.), or a hyphen(-).

`[\da-z\.-]`
: The above character set is looking for any digit 0-9, or any letter a-z, or a dot(.), or a hyphen(-).

`[a-z\.]`
: The above character set is looking for any letter a-z or a dot(.).

### Flags

Flags
: *example: `/.+/igm`*
: Expression flags change how the expression is interpreted. Flags follow the closing forward slash of the expression. There are 3 flags in the above expression, those flags are `i` `g` and `m`.

`i` **Ignore Case**
: Makes the whole expression case-insensitive. For example, `/aBc/i` would match AbC.

`g` **Global Search**
: Retain the index of the last match, allowing subsequent searches to start from the end of the previous match.
: Without the global flag, subsequent searches will return the same match.
: [RegExr](https://regexr.com/) only searches for a single match when the global flag is disabled to avoid infinite match errors.

`m` **Multiline**
: When the multiline flag is enabled, beginning and end anchors (`^` and `$`) will match the start and end of a line, instead of the start and end of the whole string.
: Note that patterns such as `/^[\s\S]+$/m` may return matches that span multiple lines because the anchors will match the start/end of **any** line.

`u` **Unicode**
: When the unicode flag is enabled, you can use extended unicode escapes in the form \x{FFFFF}.
: It also makes other escapes stricter, causing unrecognized escapes (ex. `\j`) to throw an error.

`y` **Sticky**
: The expression will only match from its lastIndex position and ignores the global (`g`) flag if set. Because each search in [RegExr](https://regexr.com/) is discrete, this flag has no further impact on the displayed results.

`s` **Dotall**
: Dot (`.`) will match any character, including newline.

 ---

There are no flags in my expression that checks for email adresses.

### Grouping and Capturing

Groups multiple tokens together and creates a capture group for extracting a substring or using a backreference.  Groups are encapsulated by a matching set of parenthesis ( ).  (ex. `(ha)+`).  In this example, the tokens 'h' and 'a' are grouped together.
Looking at my expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` there are 3 groups.

- `([a-z0-9_\.-]+)`

  - In the above group, we are looking for a sequence of 1 or more characters in the preceeding [bracket expression](#bracket-expressions).

- `([\da-z\.-]+)`

  - In the above group, we are looking for a sequence of 1 or more characters in the preceeding [bracket expression](#bracket-expressions).

- `([a-z\.]{2,6})`

  - The above group contains a [bracket expression](#bracket-expressions) and a [quantifier](#quantifiers).

### Bracket Expressions

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)

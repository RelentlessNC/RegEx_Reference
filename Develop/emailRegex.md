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
- [Lookaround](#lookaround)
- [Substitution](#substitution)
- [Escaped Characters](#escaped-characters)
- [Final Explanation](#final-explanation)

## Regex Components

### Anchors

*Anchors are unique in that they match a position within a string, not a character.*

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

***In my expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` notice we have a `^`, which means we are looking for the character set `([a-z0-9_\.-]+)` at the beginning of the string.***  

***In my expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` notice we have a `$`, which means we are looking for the character set `([a-z\.]{2,6})` at the end of the string.***

---

### Quantifiers

*Quantifiers indicate that the preceding token must be matched a certain number of times. By default, quantifiers are greedy, and will match as many characters as possible.*

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

***In my expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` there is a single quantifier at the end which is looking for 2-6 characters in length and those characters can be letters *a-z* and a *dot* (.).***

---

### OR Operator

`|` **Alternation**
: *example: `b(a|e|i)d`*
: Acts like a boolean OR. Matches the expression before or after the |. It can operate within a group, or on a whole expression. The patterns will be tested in order.

### Character Classes

*Character classes match a character from a specific set. There are a number of predefined character classes and you can also define your own sets.*

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

***In my expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, the following character classes are used.***

`[a-z0-9_\.-]`
: This particular character set is looking for any letter a-z or any number 0-9 or an underscore(_), or a dot(.), or a hyphen(-).

`[\da-z\.-]`
: The above character set is looking for any digit 0-9, or any letter a-z, or a dot(.), or a hyphen(-).

`[a-z\.]`
: The above character set is looking for any letter a-z or a dot(.).

---

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

***There are no flags in my expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`***

---

### Grouping and Capturing

*Groups allow you to combine a sequence of tokens to operate on them together. Capture groups can be referenced by a backreference and accessed separately in the results.*

`()` **Capturing Group**
: *example: `(ABC)`*
: Groups multiple tokens together and creates a capture group for extracting a substring or using a backreference.

`(?<>)` **Named Capturing Group**
: *example: `(?<name>ABC)`*
: Creates a capturing group that can be referenced via the specified name.

`\1` **Numeric Reference**
: *example: `(\w)a\1`*
: Matches the results of a capture group. For example \1 matches the results of the first capture group & \3 matches the third.

`(?:ABC)` **Non-Capturing Group**
: *example: `(?:ha)+`*
: Groups multiple tokens together without creating a capture group.

---

***My expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` has 3 groups.***

- `([a-z0-9_\.-]+)`

  - In the above group, we are looking for a sequence of 1 or more characters in the preceeding [character set](#character-classes).

- `([\da-z\.-]+)`

  - In the above group, we are looking for a sequence of 1 or more characters in the preceeding [character set](#character-classes).

- `([a-z\.]{2,6})`

  - The above group contains a [character set](#character-classes) and a [quantifier](#quantifiers).

---

### Lookaround

*Lookaround lets you match a group before (lookbehind) or after (lookahead) your main pattern without including it in the result.
Negative lookarounds specify a group that can NOT match before or after the pattern.*

`(?=ABC)` **Positive Lookahead**
: *example: `\d(?=px)`*
: Matches a group after the main expression without including it in the result.

`(?!ABC)` **Negative Lookahead**
: *example: `\d(?!px)`*
: Specifies a group that can not match after the main expression (if it matches, the result is discarded).

`(?<=ABC)` **Positive Lookbehind**
: *example: `\d(?<=px)`*
: Matches a group before the main expression without including it in the result.

`(?<!ABC)` **Negative Lookbehind**
: *example: `\d(?<!px)`*
: Specifies a group that can not match before the main expression (if it matches, the result is discarded).

---

***My expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` has 0 lookaround.***

---

### Substitution

*These tokens are used in a substitution string to insert different parts of the match.*

`$&` **Match**
: Inserts the matched text

`$1` **Capture Group**
: Inserts the results of the specified capture group. For example, $3 would insert the third capture group.

$` **Before Match**
: Inserts the portion of the source string that precedes the match.

`$'` **After Match**
: Inserts the portion of the source string that follows the match.

`$$` **Escaped $**
: Inserts a dollar sign character ($).

`\n` **Escaped Characters**
: For convenience, these escaped characters are supported in the Replace string in RegExr: `\n`, `\r`, `\t`, `\\`, and unicode escapes `\uFFFF`. This may vary in your deploy environment.

---

***My expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` has 0 substitutions.***

---

### Escaped Characters

Escape sequences can be used to insert reserved, special, and unicode characters. All escaped characters begin with the \ character.

`\+` **Reserved Characters**
: The following characters have special meaning, and should be preceded by a `\` (backslash) to represent a literal character:
`+*?^$\.[]{}()|/`
: Within a character set, only `\`, `-`, and `]` need to be escaped.

`\000` **Octal Escape**
: Octal escaped character in the form `\000`. Value must be less than 255 (`\377`).

`\xFF` **Hexadecimal Escape**
: *example: `\xA9`*
: Hexadecimal escaped character in the form `\xFF`.

`\uFFFF` **Unicode Escape**
: *example: `\u00A9`*
: Unicode escaped character in the form `\uFFFF`

`\u{FFFF}` **Extended Unicode Escape**
: Unicode escaped character in the form `\u{FFFF}`. Supports a full range of unicode point escapes with any number of hex digits.
: Requires the unicode flag (`u`).

`\cI` **Control Character Escape**
: *example: `\cI` matches TAB (char code 9).*
: Escaped control character in the form `\cZ`. This can range from `\cA` (SOH, char code 1) to `\cZ` (SUB, char code 26).

`\t` **Tab**
: Matches a TAB character (char code 9).

`\n` **Line Feed**
: Matches a LINE FEED character (char code 10).

`\v` **Vertical Tab**
: Matches a VERTICAL TAB character (char code 11).

`\f` **Form Feed**
: Matches a FORM FEED character (char code 12).

`\r` **Carriage Return**
: Matches a CARRIAGE RETURN character (char code 13).

`\0` **Null**
: Matches a NULL character (char code 0).

---

***My expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` makes use of the escaped character dot (`\.`)***

---

### Final Explanation

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

1. `([a-z0-9_\.-]+)`
Look for a string of length 1 or more that contains any combination of letters, digits, underscores, dots, or hyphens.

2. `@`
Look for the @ symbol following the previous string

3. `([\da-z\.-]+)`
Following the @ symbol, look for a second string of length 1 or more that contains any combination of digits, letters, hyphens, or dots.

4. `\.`
Following the second string, look for a dot.

5. `([a-z\.]{2,6})`
Following the dot, look for a string of length 2-6 characters and it may contain letters or dots.

## Author

[RelentlessNC](https://github.com/RelentlessNC)

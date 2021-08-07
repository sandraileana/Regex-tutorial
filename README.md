# Regex Tutorial

## Description

Brief regex tutorial that defines concepts, explain components and give examples.

## Table of Contents

  - [What is a Regex?](#regex)
    * [Hex Value](#hex-value)
    * [Email](#email)
    * [URL](#url)
    * [HTML](#html)
  - [Regex components](#components)
    * [Alternation operator](#alternation-operator)
    * [Anchors](#anchors)
    * [Back references](#back-references)
    * [Boundaries](#boundaries)
    * [Character classes](#character-classes)
    * [Flags](#flags)
    * [Grouping](#grouping)
    * [Greedy and lazy match](#greedy-and-lazy-match)
    * [List operators](#list-operators)
    * [Look-ahead and look-behind](#look-ahead-and-look-behind)
    * [Quantifiers](#quantifiers)
  - [Advantages](#advantages)
  - [Credits](#credits)
  - [References](#references)


# Regex

A **regex**, which is short for **regular expression**, is a sequence of characters that defines a specific search pattern. When included in code or search algorithms, regular expressions can be used to find certain patterns of characters within a string, or to find and replace a character or sequence of characters within a string. They are also frequently used to validate input. 

For example, the following regular expression can be used to verify that user input is a valid email address:

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

Each component of this regex has a unique responsibility to make sure that a user enters an email address that begins with an unspecified number of characters preceding the `@` symbol, followed by a domain.


## Hex Value

* Matching a Hex Value: `/^#?([a-f0-9]{6}|[a-f0-9]{3})$/`


## Email

* Matching an Email: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`


## URL

* Matching a URL: `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`


## HTML

* Matching an HTML Tag: `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`


[BACK TO TABLE OF CONTENTS](#table-of-contents)


# Components

## Alternation operator

* **Definition:** matches on a choice of regular expressions. The character(s) representing the alternation operator between any two characters (y and x) in the regular expression, the result matches the union of the strings that those two characters match (y and x).

* Types of OR Operators:
```
    `(|)` - matches a string that has any anterior characters followed by the characters on the left or right of the vertical bar.
    `[]` - matches a string that has any anterior characters without any characters within the brackets.
```

* Examples: 
```
x(y|z)          Matches a string that has x followed by y or z (and captures y or z)
x[yz]           Matches a string that has x, but without capturing y or z
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## Anchors

* **Definition:** characters within the regular expression that allow the user to match strings that begin with and/or end with certain characters. 

* Types of anchors:
```
    `^` - match-beginning-of-line operator - matches any string that start with the anterior word
    `$` - match-end-of-line operator - matches a string that end with preceeding word before the character
```

* Examples:
```
^Hi             Matches a string starting with `Hi`.
Cat$            Matches a string ending with `Cat`.
^Hello World$   Matches exact string.
winter          Matches a string exactly with the text `winter`.
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## Back references

* **Definition:** when using [grouping](#grouping) you may Capture the Group, which is saved in memory for later use. Backreferencing is the name given to the action of using these matches. Backreferencing is the refernce of a captured match, save in memory, by a captured group.

* Examples:
```
(a)\1                   Matches 'aa'
(bana)na\1bo\1          Matches 'bananabanabobana'
([xyz])\1               Using \1  matches the same text that was matched by the first capturing group.
([uwx])([yz])\2\1       Use \2 (\3, \4, ...) to identify the same text that was matched by the second (third, fourth, ...) capturing group.
                        By using one of `\1' through `\9' after the corresponding group's close-group operator, you can match a substring identical to the one that the group does.
(?<bar>[xzy])\k<bar>    Name <bar> to the group and we reference later (\k<foo>). The result is the same of the first regex.
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## Boundaries

* **Definition:** places between characters; should be thought of as a wall between any adjacent characters. 

* Types of Boundaries:
```
    **Word** and ***Non-Word**, each denoted by a specific character. 

    `\b` - a position that bounds a word, or where a word starts or ends. It denotes a place between a word and non-word character, at the start and end of a string.
    `\B` - exact opposite of a word boundary, the negation of `\b` and will match **any position a word boundary doesnt.**
    `*` - match between a word and word character, as well as between a non-word and non-word character.
```

* Examples:
```
Hello World     Has 12 total Boundaries with 8 Word Boundaries:   |H|e|l|l|o| |W|o|r|l|d|
                                                                  ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^
                                                                  N W W W W N N W W W W N
                                                                  N = Nonword Boundary \ W = Word Boundary
\bxyz\b         Matches a "whole words only search" for the string `xyz`.
\Bxyz\B         Matches only if the pattern is fully surrounded by word characters `txyzt` would match the string `xyz` because it only has word boundaries.
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## Character classes

* **Definition:** the regex engine will recognize and match only one out several specific characters, such as digits, words, or whitespace.

* **Synonim:** Character Set

* Types of Character Classes:
```
    `\d` - matches a single character that is a digit.
    `\w` - matches a word character (any alphanumeric character plus underscore).
    `\s` - matches a whitespace character (including tabs and line brakes).
    `.` - matches any character.
    The capital case for any aformentioned characters will inverse the match.
```

* Examples:
```
\d              Matches a single any digit 0-9.
\w              Matches a single any character that is a-z.
\s              Matches ` `.
.               Matches any character.
\D              Matches a single non-digit character.
\W              Matches a single any non-character that is a-z.
\S              Matches a single non-` `.
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## Flags

* **Definition:** optional parameters that we can add to a plain expression to make it search in a different way. Each flag is denoted by a single alphabetic character, and serves different purposes in modifying the expression's searching behavior.

* Types of flags:
```
    `g` - Global - Does not return after the first match, which restarted any subsequest searches from the end of the previous match (Makes the expression search for all occurences).
    `m` - Multi-line - When enabled the Anchors (^ $) will match the start and end of a line, rather than the whole string.
    `i` - Insensitive - Makes the entire expression case-insensitive.
```

* Examples:
```
/Hello/g        Matches all `Hello` in the test.
/Hello/m        Matches the beginning and ending of each line with `Hello`, rather than the whole string `Hello` itself.
/Hello/i        Matches all `hello` despite case (Hello, hEllo, heLlo, hellO, hello, HELLO all match).
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## Grouping

* **Definition:** unifies a pattern or string in a way that it is matched in a complete block.

* **Synonym:** subexpression.

* Types of Grouping:
```
    `()` - parentheses creates a capture group
    `(?:)` - using `?:` disables the capturing group
    `(?<>)` - using `?<>` puts a name to the group
```

* Examples:
```
x(yz)           Parentheses create a capturing group with value yz.
x(?:yz)*        Using ?: we disable the capturing group.
x(?<bar>yz)     Using ?<bar> we put a name to the group.
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## Greedy and lazy match

* **Definition:** quantifies that expand the match as far as possible through the text. 

* Types of Greedy and/or Lazy Matching:
```
    `* + {}` - any one of these character can be used as a quanitifer for a Greedy or Lazy Match.
```

* Examples:
```
<.+?>           Matches any character that is one or more times included inside `<` and `>`, and expands as needed.
<[^<>]+>        Matches any character expects `<` or `>` one or more times included inside `<` and `>`. 
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## List operators

* **Definition:** a set of one or more items. An item is a character, a character class expression or a range expressión. Characters enclosed by a bracket `[]` matching any single character within the brackets. If the first character within the brackets is a `^` then it signifies any character **not** in the list, and is unspecified whether it matches an encoding error. 


* **Synonym:** bracket expressions

* Types of list operators:
```
    `[...]` - matching list - matches a single character represented by one of the list items. Form a matching list by enclosing one or more items within an open-matching-list operator "[" and a close-list operator "]".
    `[...]%` - matching the string inside the brackets before the `%`.
    `[^...]` - non matching list - match a single character not represented by one of the list items. 
```

* Examples:
```
[abc]           Matches a string that either has a or a b or a c (same as a|b|c).
[a-c]           Matches a string that either has a or a b or a c (same as a|b|c).
[0-9]%          Matches a string that has a character from 0-9 before a %.
[^abc]          Matches any character except 'a' or `b' or 'c'.
[.*]            Matches '.' and '*'.
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## Look-ahead and look-behind

* **Definition:** `start and end` zero-length assertions [anchors](#anchors) but they actually match characters, then ends the match, returning only the result: **Match or No Match**. They do not consume characters in the string, but only assert wether a match is possible or not. Lookaround allows you to create regular expressions that are impossible to create without them, or that would get very longwinded without them.

* Types of look-ahead and look-behind:
```
    'h(?=t)' - matches a h only if is followed by t, but t will not be part of the match.
    '(?<=t)h' - matches a h only if is preceded by an t, but t will not be part of the match.
```

* Examples:
```
h(?!t)          Matches a h only if is not followed by t, but t will not be part of the match.
(?<!t)h         Matches a h only if is not preceded by an t, but t will not be part of the match.
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## Quantifiers

* **Definition:** characters within the regular expression that specify how many instances a character, group, or character class must be represented in the input to be matched.

* Types of quantifers:
```
    `*` - matches-zero-or-more operator - matches a string that has the anterior followed by zero or more of the last character.
    `+` - match-one-or-more operator - matches a string that has the anterior followed by one or more of the last character.
    `?` - match-zero-or-one operator - matches a string that has the atnerior follwoed by zero or one of the last character.
    `{...}` - interval operators = open-interval operator
    `\{...\}` - interval operators = close-interval operator
    `{count}` - matches exactly count occurrences of the preceding regular expression.
    `{min,}` - matches min or more occurrences of the preceding regular expression.
    `{min, max}` - matches at least min but no more than max occurencesof the preceding regular expression.
    `()*` - matches a string that has any anterior characters followed by zero or more copies of the string within the brackets.
```

* Examples:
```
xyz*            Matches a string that has xy followed by zero or more z.
xyz+            Matches a string that has xy followed by one or more z.
xyz?            Matches a string that has xy followed by zero or one z.
xyz{2}          Matches a string that has xy followed by 2 z.
xyz{3,}         Matches a string that has xy followed by 3 or more z
xyz{4,7}        Matches a string that has xy followed by 4 up to 7 z
x(yz)*          Matches a string that has x followed by zero or more copies of the sequence yz
x(yz){4,7}      Matches a string that has x followed by 4 up to 7 copies of the sequence yz
```


[BACK TO TABLE OF CONTENTS](#table-of-contents)


## Range Operator

* **Definition:** recognizes range expressions inside a list. They represent those characters that fall between two elements in the current collating sequence. Range expression by putting a range operator between two characters. 

* Types of range operator:
````
    `-' - represents the range operator
````

* Examples:
````
a-f             Within a list represents all the characters from `a' through `f' inclusively.
````



[BACK TO TABLE OF CONTENTS](#table-of-contents)


# Advantages

After this the user will be able to:

  * Identify important concepts and components of Regex.

  * Understand usage of regex.

  * Be able to apply knowledge.


[BACK TO TABLE OF CONTENTS](#table-of-contents)


# Credits

* Author: Sandra Pérez
* [Personal Github](https://github.com/sandraileana)


[BACK TO TABLE OF CONTENTS](#table-of-contents)


# References
1. Regular expressions tutorial: https://www.regular-expressions.info/tutorial.html
2. Common operators: http://web.mit.edu/gnu/doc/html/regex_3.html
3. Regular expressions: https://www.princeton.edu/~mlovett/reference/Regular-Expressions.pdf
4. Regular expressions!: https://ryanstutorials.net/regular-expressions-tutorial/

[BACK TO TABLE OF CONTENTS](#table-of-contents)


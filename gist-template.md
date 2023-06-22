# Regex Tutorial

A regex, which is short for regular expression, is a sequence of characters that defines a specific search pattern. When included in code or search algorithms, regular expressions can be used to find certain patterns of characters within a string, or to find and replace a character or sequence of characters within a string. They are also frequently used to validate input.

In this regex tutorial, I'll be defining the regex structure of the hex value:

````
/^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/
````

## Summary

```
AS A web development student
I WANT a tutorial explaining a specific regex
SO THAT I can understand the search pattern the regex defines

```

```
GIVEN a regex tutorial
WHEN I open the tutorial
THEN I see a descriptive title and introductory paragraph explaining the purpose of the tutorial, a summary describing the regex featured in the tutorial, a table of contents linking to different sections that break down each component of the regex and explain what it does, and a section about the author with a link to the author’s GitHub profile
WHEN I click on the links in the table of contents
THEN I am taken to the corresponding sections of the tutorial
WHEN I read through each section of the tutorial
THEN I find a detailed explanation of what a specific component of the regex does
WHEN I reach the end of the tutorial
THEN I find a section about the author and a link to the author’s GitHub profile

```
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

**Start/end strings**
Anchors don't match any character. Rather they match a position before or after the character.

```^``` is used to match at the _start_ of the string while ```$```is used to match at the _end_ of the string.

Example: 
```
let str1 = "Mary had a little lamb";
console.log( /^Mary/.test(str1) ); // true

let str2 = "its fleece was white as snow";
console.log( /snow$/.test(str1) ); // true

```

[Source for Anchors](https://launchschool.com/books/regex/read/anchors)

**Boundaries**

Boundaries include words-only searches (\b), non-words searches (\B), character searches (\w), and non-character searches (\W).

More info on boundaries:
- [Boundaries](#boundaries)

### Quantifiers

- Quantity {n}: simply added to the end of a character and specifies how many characters are needed

```
\d{5}:  Exactly 5 digits
\d{3,5}: Shows a range of 3 to 5 digits
\d{3,}: Ranges from 3 to more
```
For the hex value regex, there are two quantities ({3} and {6}). Both sides of the expression are separated by the OR operator, meaning that the hex value can either be a length of 3 or 6.

- Shorthands
 -```+```: another way of writing {1,}, or "one or more"
 -```?```: the same as {0,1}, or "zero or one"
 -```*```: the same as {0,}, or "zero or more"


[Source for Quantifiers](https://javascript.info/regexp-quantifiers)

### OR Operator

The OR (|) operator is used to match characters or an expression at either the left or right of the | operator and behaves like a boolean expression.

Example:
```
bye|goodbye: Match a string that contains either "bye" or "goodbye"
(b|cd)ef: Matches a string that contains either "bef" or "cdef"
(a|b)*c: Matches a string that has a sequence of alternating "a" and "b" ending with "c"
```

In the regex expression, as mentioned above, there contains an OR operator, meaning that the expression takes on either a length of 6 characters or digits after the "#" or 3.

[Source for OR Operator](https://support.workiva.com/hc/en-us/articles/4407304269204-Regular-expression-operators)

### Character Classes

Character classes specifies a set of characters that will match a single character from a given input string and the regex engine can match only one of several characters.

```\d```: describes a digit from 0 to 9
```\s```: describes a  space (\t for tab, \n for newline, etc.)
```\w```: describes latin letters, digits, underscore '_'
```\D```: describes non-digits
```\S```: describes anything outside of \s
```\W```: describes anything outside of \w
```.```: describes any character outside of a newline \n
```[A-Z]```: describes a range of pre-defined characters
```[145]```: describes specific digits to be matched


[Source for Character Classes](https://www.regular-expressions.info/charclass.html)
[Source for Character Classes](https://javascript.info/regexp-character-classes#summary)

### Flags

Flags is an optional parameter to a regex that shifts the default searching behavior. It uses a single lowercase alphabetical character

```i```: causes the expression to be search case-insensitive (ignoring cases)
```g```: causes the expression to search for all occurrences (global)
```s```: causes the '.' character to match newlines '\n' as well (dot all)
```m```: causes the boundary characters ^ and $  to match the beginning and ending of every single line instead of the beginning and ending of the whole string (multiline)
```y```: causes the expression to start its searching from the index indicated in its lastIndex property (sticky)
```u```: causes the expression to assume individual characters as code points rather than code units, and thus match 32-bit characters as well (unicode)

[Source for Flags](https://www.codeguage.com/courses/regexp/flags)

### Grouping and Capturing

Grouping and capturing allows us to get a part of the match as a separate item in the result array. Quantifier appended after the parentheses ```(...)``` will apply to the objects in the parentheses, and parentheses groups are numbered left to right. A group may be excluded from numbering by adding ```?:```

[Source for Grouping and Capturing](https://javascript.info/regexp-groups)

### Bracket Expressions

Bracket expressions are a list of characters and/or character classes enclosed in brackets []. They are used when you need to match single characters in a list, or a range of characters in a list. If a carat ^ is added as the first character then it matches characters that are not in the list.

Examples
```
[abc]: means a, b, or c
[a-z]: a to z
[^ars]: any character outside of a, r, or s
```

In the example regex for the hex code, there includes a list of alphanumerical characters that include a to z, A to Z, and 0 to 9, meaning that we have required for the match of either of these characters to be included in our hex value.

[Source for Bracket Expressions](https://docs.trendmicro.com/all/ent/imsva/v8.5/en-us/imsva8.5_olh/usg_kw_exp_regexp_brkt.html)

### Greedy and Lazy Match

_Greedy behavior_ is a default matching where the quantifier tells the engine to match as many instances of its quantified token or subpattern as possible. For the match attempt that starts at a given position, a greedy quantifier gives you the longest match.

```
let greedyRegex = /".+"/g;

let str = 'a "witch" and her "broom" is one';

alert( str.match(greedyRegex) ); // "witch" and her "broom"

```

However, _lazy behavior_ is the complete opposite of greedy behavior. In contrast, it eats up as many instances of the quantified token as possible and tells the engine to match as few of the quantified tokens as needed. 

```
let lazyRegex = /".+?"/g;

let str = 'a "witch" and her "broom" is one';

alert( str.match(lazyRegex) ); // "witch", "broom"
```

It's used by putting a question mark ```?``` after the quantifier while greedy uses a ```+```. Depending on what kind of match is necessary to get the desired result, either matching can be utilized, but the lazy matching behavior leads to higher optimizization and works faster.

[Source for Greedy and Lazy search](https://javascript.info/regexp-greedy-and-lazy)
[Source for Greedy and Lazy search](https://www.rexegg.com/regex-quantifiers.html)

### Boundaries

As mentioned above, boundaries include words-only searches (\b), non-words searches (\B), character searches (\w), and non-character searches (\W). ```\b``` is a test, similar to that of '^' and '$', and it checks if the position in the string is a word boundary

```
alert( "Hello, Java!".match(/\bHello\b/) ); // Hello
alert( "Hello, Java!".match(/\bJava\b/) );  // Java
alert( "Hello, Java!".match(/\bHell\b/) );  // null (no match)
alert( "Hello, Java!".match(/\bJava!\b/) ); // null (no match)
```

[Source for Boundaries](https://javascript.info/regexp-boundary)

### Back-references

Back-references are regular expression commands that refererence a previous part of the matched regular expression. Back-references are specified with a backslash and a single digit, such as ```\2```. The part of the regular expression they refer to is the capturing group, which is encased by parentheses.

[Source for Backreferences](https://www.gnu.org/software/sed/manual/html_node/Back_002dreferences-and-Subexpressions.html#:~:text=back%2Dreferences%20are%20regular%20expression,and%20is%20designated%20with%20parentheses.)

### Look-ahead and Look-behind

Lookahead and lookbehind are useful for matching something depending on what goes before (lookbehind) or after (lookahead). Here are some steps

Lookahead Positive
    -```A(?=B)```: Find expression A where expression B follows
Lookahead Negative
    -```A(?!B)```: Find expression A where expression B does not follow
Lookbehind Positive
    -```(?<=B)A```: Find expression A where expression B precedes
Lookbehind Negative
    -```(?<!B)A```: Find expression A where expression B does not precede

[Source for Look-ahead and Look-behind](https://stackoverflow.com/questions/2973436/regex-lookahead-lookbehind-and-atomic-groups)

## Author

[Author's page](https://github.com/jmaduafo)



# Regex - What is a Regex? - Regular expression == regex

Not universal.

A concise Domain Specific Language (DSL) for string pattern matching.
Regexes are widely employed in text processing tasks like validation, parsing, and string manipulation.

Very confusing.

## Regex simplified grammar - phase 1
`
R               ::= SEQUENCE [ | SEQUENCE ]*
SEQUENCE        ::= [ ELEMENT[QUANTIFIER] ]+
ELEMENT         ::= LITERAL | GROUP
GROUP           ::= (?: R )
QUANTIFIER      ::= ? | * | +
LITERAL         ::= character other than \.[]{}()^$*+?|"-\n
                    can use \x00 notation for special characters `

a R->SEQUENCE->ELEMENT->LITERAL 
matches the letter 'a'

aa R->SEQUENCE->ELEMENT ELEMENT->LITERAL LITERAL 
matches the letters 'aa'

a*b R->SEQUENCE->ELEMENT QUANTIFIER ELEMENT->LITERAL * LITERAL
matches any amount of 'aaaaaa' and a 'b'

ab?c R->SEQUENCE->ELEMENT ELEMENT QUANTIFIER ELEMENT->LITERAL LITERAL ? LITERAL
matches an 'a', zero or one 'b' and a 'c'

(?:ab)?c R->SEQUENCE->ELEMENT QUANTIFIER ELEMENT->GROUP ? LITERAL->(LITERAL LITERAL) ? LITERAL
matches zero or one time 'ab', and a 'c'

a|b R->SEQUENCE|SEQUENCE->ELEMENT|ELEMENT->LITERAL|LITERAL
matches 'a' or 'b'

## Regex matching mindset

```Match.java
Pattern p = Pattern.compile("regex string");
Matcher m = p.matcher("input string");
m.find();
m.group().equals("")
m.start() == 2;
m.end() == 5;
```

### regex: abc|abde - a regex pattern

input: abdk

start abc               index 0 on both strings
a matches a             index 1 on both strings
b matches b             index 2 on both strings
d does not match c      restart the input index and move the regex index to the next alternative

start adbe              index 0 on both strings
a matches a             index 1 on both strings
b matches b             index 2 on both strings
d matches d             index 3 on both strings
k does not match e      no match

### regex (?:ab|abc)c

input: abccde

start group             index 0 on both strings
a matches a             index 1 on both strings
b matches b             there is a match, move out of the group

start c                 index 2 on input 
c matches c             matched

### regex (?:abc|ab)c

input: aaabccde

start group             index 0 on both strings
a matches a             index 1 on both strings
a does not match b      restart the input index and move the regex index to the next alternative

start group             index 0 on both strings
a matches a             index 1 on both strings
a does not match b      blacklist the first a and restart on index one until the regex matches 

### backtracking regex (?:ab|a)b(?:ck|bc)

input: abbc

a matches
b matches
first group done

b matches

c matches
End Of String doesn't match k: 
backtrack to c, go to alternative
c doesn't match b

backtrack from the last alternative that we matched
go to first group alternative
restart from index 0

a matches
first group done

b matches

c does not match, go to alternative
b matches
c matches
regex matched

> an intuitive regex will use recursion

## decimal

\d stands for decimal
`\d == (?:0|1|2|3|4|5|6|7|8|9)`
cannot write \d because \ is a string escape character

java needs "\\d"

\d might mean slightly different things

what if we wanted to match an actual list of numbers with square brackets?

```
\ -> \x5C
. -> \x2E
[ -> \x5B
] -> \x5D
{ -> \x7B
} -> \x7D
( -> \x28
) -> \x29
^ -> \x5E
$ -> \x24
* -> \x2A
+ -> \x2B
? -> \x3F
| -> \x7C
" -> \x22
- -> \x2D
\n-> \x0A
```

## Regex simplified grammar - phase 2
`
R           ::= SEQUENCE [ | SEQUENCE ]*
SEQUENCE    ::= [ ELEMENT[QUANTIFIER] ]+
ELEMENT     ::= LITERAL | GROUP | PCC | CC
GROUP       ::= (?: R )
QUANTIFIER  ::= ? | * | +
LITERAL     ::= character other than \.[]{}()^$*+?|"-\n
                can use \x00 notation for special characters
PCC         ::= \s | \d | \w | \S | \D | \W | .
CC          ::= [ CHAR+ ] | [^ CHAR+ ]
CHAR        ::= LITERAL | RANGE | PCC
RANGE       ::= LITERAL - LITERAL
.           ::= all characters except \r and \n
\s          ~= white space
\d          ~= digits [0-9]
\w          ~= word characters [a-zA-Z0-9_]
`

`(?:0|1|2|3|4|5|6|7|8|9) ==  [0-9] == [0123456789] == [\d] == \d`

`[^\d]` is a negated character class

## String literal regex - poor mans version

`"\\x22(?:\\x5C.|[^\\x22])*\\x22"`

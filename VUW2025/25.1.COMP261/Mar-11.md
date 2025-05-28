# Regex

Regex's are a bunch of symbols

2 index's: grammar and tokens

## String literal regex

Poor Mans String Literal

`"\\x22(?:\\x5C.|[^\\x22])*\\x22"`
     `"(?:\.|[^"])*"`

```literal.java
static final Pattern p= Pattern.compile("??????");
public static boolean matches(String input){
    return p.matcher(input).find();
}
public static void main(String[] a){
    assert matches("\"hello\""); //"hello"
    assert matches("\"hello world\""); //"hello world"
    assert !matches("\"hello\nworld\""); //No new lines inside string lit
    assert matches("\"hello\\nworld\"");//"hello \nworld"
    assert matches("\"Hi\tMario!\""); //"Hi Mario"
    assert matches("\"Hi\\tMario!\""); //"Hi\tMario"
    assert matches("\"Hi \\\"Mario\\\"\""); //The string lit `Hi "Mario"`
    assert !matches("\"\\\""); //The string lit composed of 3 char: " \ "
}
```

Regex will give you exactly what you ask for, apart from very rare bugs.

`"\\x22(?:\\x5C[nt\\x22\\x5C]|[^\\x22\\x5C\\x0A])*\\x22"`
     `"(?:\[nt"\]|[^"\\n])*"`

## Regex simplified grammar - phase 3
`
R           ::= SEQUENCE [ | SEQUENCE ]*
SEQUENCE    ::= [ ELEMENT[QUANTIFIER] ]+
ELEMENT     ::= LITERAL | GROUP | PCC | CC
GROUP       ::= (?: R ) | ( R )
QUANTIFIER  ::= ? | * | +
LITERAL     ::= character other than \.[]{}()^$*+?|"-\n
                can use \x00 notation for special characters
PCC         ::= \s | \d | \w | \S | \D | \W | .
CC          ::= [ CHAR+ ] | [^ CHAR+ ]
CHAR        ::= LITERAL | RANGE | PCC
RANGE       ::= LITERAL - LITERAL
LOOK        ::= (?= R ) | (?! R ) |                 // look ahead       - this regex is/not valid in front of us
                (?<= R ) | (?<! R ) |               // look behind      - this regex is/not valid behind us
                \A | \z | \Z | ^ | $ | \b | \B      // anchors          - the text where we are is one of x cases
                beginning of the string
                matches the end of the string 
                matches the end of the string also before a newline
                matches the start of a line/string depending on regex mode
                matches the end of a line/string depending on regex mode
                matches a word boundary position
                matches a non word boundary position
.           ::= all characters except \r and \n
\s          ~= white space
\d          ~= digits [0-9]
\w          ~= word characters [a-zA-Z0-9_]
`
`(?:(?![04])[abc\\d])+`

a12b456 = a12b

abc = abc

00a12b456 = a12b

## Only parentheses group

A group with just ().

It works just like a normal group when it comes to matching.
But it has another feature after matching.

we can call `matcher.group(number);`

# Tokenization

Tokenization is a fundamental step for parsing.

Break down the raw text into tokens.

`File -> String -> List<Token> -> AST`

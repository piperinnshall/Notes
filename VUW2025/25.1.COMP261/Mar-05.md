# Parsing

Why parsing?

It will be a very good exercise to fully understand recursion.

It is about recursive behaviour with mutation.

COMP102 and COMP103 focused on using a simple Scanner to seperate the words and numbers.

Real world text data isnt so simple.
- Structured text (eg HTML, XML, JSON)
- Programs written in programming languages
- Semi-structured text data with semi-standard formatting (CVS)
- Natural language text is complicated
    (paragraphs, sentences, punctuation, parts-of-speech,
    grammatical structure, footnotes, word endings, ... )

## Formal Language

Formal languages can be described by a grammar:

A set of rules describing how to construct valid examples of the language.

The grammar rules specify the structure of the text in that language.

A parser is a program that is built using the grammar rules
to parse an input and construct a data structure to contain the structure of the text.

A simple HTML grammar:

```grammar.html
HTMLFILE ::= "<html>" [ HEAD ] BODY "</html>"
HEAD ::= "<head>" TITLE "</head>"
TITLE ::= "<title>" TEXT "</title>"
BODY ::= "<body>" [ BODYTAG ]* "</body>"
BODYTAG ::= H1TAG | PTAG | OLTAG | ULTAG
H1TAG ::= "<h1>" TEXT "</h1>"
PTAG ::= "<p>" TEXT "</p>"
OLTAG ::= "<ol>" [ LITAG ]+ "</ol>"
ULTAG ::= "<ul>" [ LITAG ]+ "</ul>"
LITAG ::= "<li>" TEXT "</li>"
TEXT ::= sequence of characters other than < and >
```

Each grammar line is called a:
- 'production',
- 'Production rule'
- 'Grammar rule'

The ::= symbol often read 'is' or 'is-defined as' identifies the production rule.

The upper case names are called 'non-terminals' All non-terminals are defined by a production.

The string looking things are called 'terminals' or 'tokens' And they represent the text in the string literal.

Open/Close squares represent optionality. The expression inside may, or may not be present in the denoted language.

## The importance of verbalising code.

`HTMLFILE ::= "<html>" [ HEAD ] BODY "</html>"`

An HTML file is defined as an open HTML tag, an optional HEAD, a BODY, and a closing HTML tag.

`HEAD ::= "<head>" TITLE "</head>"`

"A head is defined as an open head token, a title and a closed head token."

`TITLE ::= "<title>" TEXT "</title>"`

A title is defined as an open title token, a text and a closed title token."

`BODY ::= "<body>" [ BODYTAG ]* "</body>"`

"A body is defined as open body token, any number of bodytags and a closed body token"

`BODYTAG ::= H1TAG | PTAG | OLTAG | ULTAG`

"A bodytag is defined as either an H-one-tag, or a P-tag, or an O-L-tag, or an U-L-tag."

`H1TAG ::= "<h1>" TEXT "</h1>"`

"An H-one-tag is defined as an open H-one token, text, and a closed H-one token."

`PTAG ::= "<p>" TEXT "</p>"`

"A P-tag is defined as an open p token, text, and a closed p token."

## Concrete parse tree

Concrete parse tree has redundant information.

abstract syntax tree.


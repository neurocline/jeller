---
title: "Introduction"
date: 2019-04-02T18:24:22-07:00
---

Let's do it all. Write a new parser generator capable of parsing ambiguous grammars, but
only those with spurious ambiguity, not essential ambiguity (the latter means that there
are multiple parse trees with different semantics). We want "close to linear time", and
we want good error recovery, and we want to be able to parse multiple kinds of
grammars

- complex grammars like C++
- messy grammars like Markdown
- bit-level grammars with state (like length-prefixed data)

This is a lot. But it's necessary. And eventually, we want to be able to parse and assign
semantics to actual language, like English, which means we probably need to embrace
essential ambiguity.

We'll also make grammars for our tools, and we want to be able to translate one language
to another. We want to take a grammar specification written in a different spec language
and translate it to ours.

Finally, we want to handle strings with mixed languages. This is happening more and more,
but it always happened, we just ignored it. Here are some big use cases

- comments in a programming language
- template language embedded in HTML document
- SQL statements as data in say Python or C++ code

The long run is to be able to parse and generate code for a truly mixed-language file; imagine
a Go file with both C and assembly language code in it, where we can call across language
bounds and generate code that follows the whole composed system constraints.

## Starting point

Define a syntax and semantics for writing grammars. Crib heavily from existing
systems, most of which are some kind of BNF.

Write a parser generator. There's an obvious bootstrap issue, the parser generator's internal parser
can't start out defined in itself, we need something written by hand that can read a grammar.

## Some starting points

This is a prototype of the Asciidoc grammar written in ANTLR4 (from the AsciiDoctor project).
Unfortunately, the fleshed-out version is much harder to read (second link)

- [asciidoc-grammar-prototype/src/main/antlr/Asciidoc.g4](https://github.com/asciidoctor/asciidoc-grammar-prototype/blob/master/src/main/antlr/Asciidoc.g4)
- [asciidoctor/inline_parser/asciidoctor_grammar.treetop](https://github.com/Mogztter/asciidoctor-inline-parser/blob/master/lib/asciidoctor/inline_parser/asciidoctor_grammar.treetop)

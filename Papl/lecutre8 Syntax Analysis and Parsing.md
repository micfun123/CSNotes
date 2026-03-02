
## Remove Ambiguity

This requires the addition of extra non-terminals and rules.

he example grammar for <exp> can be disambiguated by adding rules that forces + operation to appear above * in parse trees (to deprive the freedom to choose from + & * rules):
<exp> → <exp> + <term> | <term>
<term> → <term> * <factor> | <factor>
<factor> → x |y |z

Where `term` and the `factor` are newly introduced non terminal rules


## Limits of context-Free Grammar

There are some aspects of programming
language syntax that cannot be captured using a
context-free grammar.
• For example, the rule that variables must be
declared before they are used is a context-
sensitive property.
• Context-sensitive properties are resolved by the
semantic analyser (beyond the scope of this
module).

## Syntax Analyser

Give an input program the goal of a syntax analuser is to 
 > Find all syntax errors and produce a error message 
 > Produce the parse tree for the program for the code genoration
 
 ## Parsers

### Top Down Parsers
	Beginning with the root (the start symbole of grammar roles)
	each node is visited before its braches are followed
	Branch from a particular node are visited in left-to-right order
	-a leftmost derivation;

### Bottem up parser
	Beginning at the leave of parse tree (terminal symbols) and progressing towards the root
	Order is that of the revers of a rightmost derivation

### Recursive-Descent Parser ( RDP)

An RDP consists of a collection of subprograms many of which are recursive (therefore its name) and produces a parse tree in top-down order.

There is a subprogram for each nonterminal in
the grammar.

• A grammar for simple expressions:
<expr> → <term>+<term>|<term>-<term>
<term> → <factor>*<factor>|<factor>/<factor>
<factor> → id | int_constant|(<expr>)
• We can write the grammar for <expr> and <term> in a
more compact form, because the only difference in the
two alternatives in both cases is a terminal symbol (+ or -
, * or/).
<expr> → <term> {(+ | -) <term>}
<term> → <factor> {(* | /) <factor>}
<factor> → id | int_constant|(<expr>)


### Rules with Multiple RHS
The example shows, when a nonterminal that
has more than one RHS (e.g., rule <factor>)
requires an initial process to determine which
RHS it is to choose.
• The correct RHS could be chosen based on the
next token of input
– The next token of input is compared with the first
token of each RHS until a match is found (e.g., the
next input token is a left parenthesis “(”, rule
<factor> -> (<expr>) would be selected)
– If no match is found, it is a syntax error.
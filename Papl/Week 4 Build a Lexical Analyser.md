
DFA = Deterministic Finite Automaton


The set of all strings accepted by a DFA is known as the language recognised.

{anbn |n≥1} cannot be recognized by a FA ( Finite Automata )

RE and DFA can be eqivilant

give a RE r and a DFA M 

L(M) = L(r)

A Finite Automata is a has a finenite number state. This is due to it not being remember how many tokens it has previously due if its a large arbatary number.

So, for a language that requires matching counts like a^n
b^n , where n can be any number, a FA is unable to handle it because it would need to remember the exact number of 'a's to ensure the same number of 'b’s to follow

A given language being regular language or not depends
on if it possesses the essential “pumping” property of all
regular languages,  which says that for every long enough string in a regular
language, there must be a middle section (y) that can be
repeated (pumped) any number of times to produce a
string that is still in the language.


## Simplification to DFA

We often have a large number of transitions between
two states in a DFA.
• E.g., in an identifier recognition DFA,
– 52 arcs for English letters (labelled by each of the lower- and
upper-case letters)
– 10 for digits
• Obviously, drawing so many transition arcs to a DFA is
not a good choice.
• Similar to the case of REs, we name a set of symbols
letter = {a,b,c,...,z,A,B,C,...,Z}
digit = {0,...,9}
and replace their arcs by a single arc labelled letter Or
digit (or simply d as in our example)


There for, RE
	ident = letter (_ | letter | digit)*


Consider the DFA for the lexical analyser for a minimal
language that includes:
– identifiers
– the symbols :=, +, ;
– keywords program, begin, end, input &
output.
• It has output tokens END OF INPUT, ERROR,
IDENTIFIER, ASSIGN, PLUS, SEMI COLON,
PROGRAM, BEGIN, END, INPUT & OUTPUT.

![[Pasted image 20260216092450.png]]
The DFA begins in its initial state START, and a token is
recognised as soon as the accepting state DONE is
reached.
• (e.g., if the arc labelled “+” is taken, token PLUS has
been recognised).
• The “re-read” means that the input character that
resulted in this particular transition being taken should be
read again (because it is the first character of the next
token).
• The state names IN_ID and IN_ASSIGN can be replaced
with any other meaningful names.

## Build Lexical Analyser
Lexical analyser tend to be built in three ways:
• (1) Write a formal description (e.g., REs) of the token
patterns, and these description are used as input to a
software tool, e.g., Lex, which automatically generates a
lexical analyser.
Or, design DFAs that describe the token patterns, then
• (2) write a program to implement the diagram, or
• (3) write a table-driven implementation of DFA.
• There are algorithms that construct lexical analysers
from DFAs automatically. The construction algorithms
are beyond the scope of this module.


## Lexical Analysiser Tool: Lex

The following is a complete (albeit simple) Lex file (Lex
program) that displays (prints) token names rather than
returning tokens to the syntax analyser.
%%
[ \n\t]+ { ; }
if { printf("IF\n"); }
then { printf("THEN\n"); }
[0-9]+ { printf("NUMBER\n"); }
[a-zA-Z][_0-9a-zA-Z]* { printf("IDENT\n"); }
. { printf("ERROR\n"); }
%%

The patterns on the left are all regular expressions,
although in a slightly different notation to what have been
discussed in last lecture. For example,
\n and \t represent the newline and tab characters;
[abc] is the shorthand for (a | b | c);
[a-z] is the shorthand for (a|b|···|z);
. means any character not in the alphabet.

For example, on reading the following text:
why then, iff
it’s 321?
The C compiled lexical analyser will output the following results:
IDENT (why)
THEN (then)
ERROR (,)
IDENT (iff)
IDENT (it)
ERROR (’)
IDENT (s)
NUMBER (321)
ERROR (?)
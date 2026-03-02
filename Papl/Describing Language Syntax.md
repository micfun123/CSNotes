Context-free grammar (CFG) – the tool for defining the
syntax of programming languages.
• Backus-Naur Form (BNF) – a notation for CFG
definitions of real programming languages.
• Derivation – the process/procedure of using the
language grammar to check the syntax of source code .


## GFG 

There are four classes of formal grammar to describe natural languages : regular, context-free, context-sensitive and recursively enumerables.

Of these, two grammar classes have been found to be useful to describe programming languages:
– regular grammars (equivalently, regular expressions) are useful for
defining languages’ lexical structure; and
– context-free grammars (CFG) for defining their syntax

### CFG Definition

Formally, a **context-free grammar** is a tuple:

G=(T,N,S,P)G = (T, N, S, P)G=(T,N,S,P)

where:

### • T — Terminal Symbols

- A finite, nonempty set of **terminal symbols**
    
- These are the actual strings of the language
    
- They appear in the final sentences of the language
    
- Example: `while`
    

---

### • N — Non-Terminal Symbols

- A finite, nonempty set of **non-terminal symbols**
    
- N∩T=∅N \cap T = \varnothingN∩T=∅ (disjoint from terminals)
    
- Represent syntactic structures defined by other rules
    
- Example: `<exp>`
    

---

### • S — Start Symbol

- S∈NS \in NS∈N
    
- The distinguished non-terminal from which derivations begin
    

---

### • P — Production Rules

- A set of **context-free productions** of the form:
    

A→αA \rightarrow \alphaA→α

where:

- A∈NA \in NA∈N
    
- α∈(T∪N)∗\alpha \in (T \cup N)^*α∈(T∪N)∗
    
- (T∪N)∗(T \cup N)^*(T∪N)∗ denotes any string (including the empty string) of terminals and/or non-terminals
    

---

Grammar Examples
• G1 = (T, N, S, P) where
	– T = {a, b},
	– N = {S} and
	– P = {S → ab, S → aSb}.
	
• G2 = (T, N, S, P) where
– T = {a, b},
– N = {S, C} and
– P ={S →ε, S →C, S →aSa, S →bSb, C → a, C → b}.

• Instead of writing each individual rules of a given 	nonterminal, we group the alternative righthand 	sides and separate them using |
• For example, G2 can be written as follows:
	S → ε | C | aSa | bSb
	C → a | b



## Backus-Naur Form (BNF)
A popular notation for CFG definitions of real
programming languages is Backus-Naur Form
(BNF).
• In BNF, non-terminal symbols are given a
descriptive name, within < >.
• For example, for use <exp>, <number> and
<digit> as nonterminals, and +, -, *, /, 0,1,…, 9
are terminal symbols when defining the syntax of
a language.

Using these symbols, the syntactic structure for
arithmetic expression would be defined by the
following productions:
<exp> → <exp> + <exp> | <exp> − <exp> |
<exp> ∗ <exp> | <exp> / <exp> | (<exp>) | <number>
<number> → <digit> | <digit> <number>
<digit> → 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
Where <exp>, <number> and <digit> are nonterminals,
and +, -, *, /, 0,1,…, 9 are terminals


## Derivations

We use a context-free grammar to derive strings of
terminal symbols.
• Starting with the start symbol S, we repeatedly apply the
production rules until we obtain a string comprising only
of terminal symbols, which is called a sentence. This
process is called derivation.
• Every string of symbols in a derivation is a sentential
form.


### Grammar, Derivation and
Languages


We say that the language defined by a grammar is made
up of exactly those sentences that can be derived from it.

## Leftmost & Rightmost Derivations

• Consider the following grammar for arithmetic
expressions:
<exp> → <exp>+<exp>|<exp>*<exp> |x|y|z
• A derivation of the sentence x + y * z from this grammar
could be:
<exp> ⇒ <exp> + <exp>
⇒ x + <exp>
⇒ x + <exp> * <exp>
⇒ x + y * <exp>
⇒ x + y * z
• This particular derivation is known as a leftmost derivation
– This is because, at each step, the leftmost non-terminal symbol is
resolved.

'## Parse Trees
• We can illustrate the structure of the expression given by
a derivation as a parse tree – it shows how terminal
symbols are derived from the grammar.
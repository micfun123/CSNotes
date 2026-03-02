
Types of Top-down Parsers
	Recursive descent parser 
	Table-Driven Parsers
	Parsing table construction (information only)

## Rules with Left Recursion

If a grammar has left recursion, either direct or
indirect, it cannot be used directly by a
recursive-decent parse.
– Direct left recursion
S → S
 (note that S →
 S is not left recursion)
– Indirect left recursion
S → A

A → S
• It leads to indefinite/non-terminating recursion.


A grammar can be modified to remove direct left
recursion.
• For each nonterminal, A,
1. Group the A-rules as A → Aα1 | … | Aαm | β1 | β2 | … | βn
where A → Aα1 | … | Aαm are rules with left recursion and
A → β1 | β2 | … | βn are rules without left recursion
2. Introduce a new nonterminal A’ and replace the original
rules with
A → β1A’ | β2A’ | … | βnA’
A’ → α1A’ | α2A’ | … | αmA’ | ε


## Left Recursion Removal

A grammar can be modified to remove direct left
recursion.
• For each nonterminal, A,
1. Group the A-rules as A → Aα1 | … | Aαm | β1 | β2 | … | βn
where A → Aα1 | … | Aαm are rules with left recursion and
A → β1 | β2 | … | βn are rules without left recursion
2. Introduce a new nonterminal A’ and replace the original
rules with
A → β1A’ | β2A’ | … | βnA’
A’ → α1A’ | α2A’ | … | αmA’ | ε


## LL Parsers


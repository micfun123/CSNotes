
Subprograms are the fundamental building
blocks of programs and are among the most
important concepts of language design. They
facilitates the flow control at program level.

## SubProgramms

Decomposing a problem into sub-problems makes better
management of complexity – smaller problems are easier to solve. It
is necessary that programming languages provide facilities that
support the decomposition.
• The key concept provided by all modern languages is that of the
subprogram, procedure, or function.
• A subprogram is a piece code that is identified by a name, is given a
local reference environment of its own and can exchange
information with the rest of the code using parameters.
• Both procedures and functions are subprograms. Normally, a
function has a return value, but a procedure does not.
• For rest of the lecture, we will consider only functions, but the
discussions are equally applicable to procedures.


Subprograms/Functions provide one of the two fundamental
abstraction facilities of programming languages:
– Process/control abstraction:
• Provides programmers with the ability to hide procedural details.
• Allows programmers to be concerned only with a procedure’s
interface, rather its implementation.
• E.g., given a function sort(var anArray : ArrayOfInt);
(sorts anArray into ascending order) we don’t need to know the
body of sort to use it.
– Data abstraction: allows the use of sophisticated data types without
knowing how such types are implemented. Again, the aims are to
separate concerns and to promote reusability and maintainability of
programs.
• Emphasized in the1980s.


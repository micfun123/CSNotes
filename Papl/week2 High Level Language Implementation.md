

![[Pasted image 20260127140521.png]]

The whole Operating System is separated into several layers ( from 0 to n ) as the diagram shows. Each of the layers must have its own specific function to perform. There are some rules in the implementation of the layers as follows.

1. The outermost layer must be the User Interface layer.
2. The innermost layer must be the Hardware layer.
3. A particular layer can access all the layers present below it but it cannot access the layers present above it. That is layer n-1 can access all the layers from n-2 to 0 but it cannot access the nth layer.

Thus if the user layer wants to interact with the hardware layer, the response will be traveled through all the layers from n-1 to 1. Each layer must be designed and implemented such that it will need only the services provided by the layers below it.

**Advantages :**

There are several advantages to this design :

1. **Modularity :** This design promotes modularity as each layer performs only the tasks it is scheduled to perform.
2. **Easy debugging :** As the layers are discrete so it is very easy to debug. Suppose an error occurs in the CPU scheduling layer, so the developer can only search that particular layer to debug, unlike the Monolithic system in which all the services are present together.
3. **Easy update :** A modification made in a particular layer will not affect the other layers.
4. **No direct access to hardware :** The hardware layer is the innermost layer present in the design. So a user can use the services of hardware but cannot directly modify or access it, unlike the Simple system in which the user had direct access to the hardware.
5. **Abstraction :** Every layer is concerned with its own functions. So the functions and implementations of the other layers are abstract to it.

**Disadvantages :**

Though this system has several advantages over the Monolithic and Simple design, there are also some disadvantages as follows.

1. **Complex and careful implementation :** As a layer can access the services of the layers below it, so the arrangement of the layers must be done carefully. For example, the backing storage layer uses the services of the memory management layer. So it must be kept below the memory management layer. Thus with great modularity comes complex implementation.
2. **Slower in execution :** If a layer wants to interact with another layer, it sends a request that has to travel through all the layers present in between the two interacting layers. Thus it increases response time, unlike the Monolithic system which is faster than this. Thus an increase in the number of layers may lead to a very inefficient design.

### Compilation
Translate high-level program (source language) into
machine code (machine language)
• Slow translation, fast execution
• Compilation process has several phases:
– lexical analysis: converts characters in the source program into
lexical units
– syntax analysis: transforms lexical units into parse trees which
represent the syntactic structure of program
– Semantics analysis: generate intermediate code
– code generation: machine code is generated
• This work is done by a compiler

![[Pasted image 20260202092334.png]]

### Structure of a compiler 
This diagram shows the dataflow of a compiler 
![[Pasted image 20260202092409.png]]



### Lexical Analysis
The lexical analyser (or scanner): reads the source
program’s text (one character at a time); and returns a
sequence of tokens to send to the next phase.
• Tokens are symbolic names for the lexical elements of
the source language; in a Pascal compiler, for example:
– IF might be the token for the Pascal keyword if
– IDENT stands for any identifier (e.g., foo, n12).

### Symbol Table
The symbol table is a data structure containing all the
identifiers (together with their attributes) of a source
program.
• Attributes
– For variables, typical attributes include type, size, scope.
– For methods, procedures or functions:
• number of arguments and their types and passing mechanisms;
• the return type (if any).

### syntax analyser (parser)
The syntax analyser (parser) analyses the syntactic structure of the
source program.
• The input to a parser is the sequence of output tokens from the
lexical analyser.
• It attempts to apply the rules that define the syntax of the language
on the sequence of tokens.

## Semantic Analysis
Checks weather the the code is semantic correct.  Such as checking that floats cannot be added to string. Code can be syntax correct but semantically wrong

### Code generation
The final task of the compiler is to generate code for a
specific machine. In this phase we need to consider such
things as:
– Instruction selection: which (machine language) instructions to use.
– Instruction scheduling in which order to put those instructions.
– Register allocation: the allocation of variables to processor registers
– Debug data generation if required so the code can be debugged

### Pure interpretation 
In this implementation, a program is interpreted by
another program called interpreter that directly executes
the programs written in a high-level programming
language without previously batch-compiling them into
machine language.



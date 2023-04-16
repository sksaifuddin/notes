1. Complex Conditional: a complex conditional statement  
2. Complex Method: a method with high cyclomatic complexity  
3. Duplicate Code: a code clone within a method  
4. Empty Catch Block: a catch block of an exception is empty  
5. Long Identifier: an identifier with excessive length  
6. Long Method: a method is excessively long  
7. Long Parameter List: a method has long parameter list  
8. Long Statement: an excessive long statement
9. Magic Number: an unexplained number is used in an  
expression  
10. Missing Default: a switch statement does not contain a  
default case  
11. Virtual Method Call from Constructor: a constructor calls a  
virtual method.

SOURCE: https://www.tusharma.in/smells/IMPL.html

Cyclomatic complexity:

It is a measure of number of linearly independent paths in it. It is a software metric used to indicate the complexity of a program. A control flow graph can used to determine it with a formula.

==cyclomatic complexity = E-N+2P ==

E = number of edges in the flow graph.
N = number of nodes in the flow graph.
P = number of nodes that have exit points

SOURCE: https://www.geeksforgeeks.org/cyclomatic-complexity/

[[code smells - Home]]
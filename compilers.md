# Compilers

## Lexical analysis
* takes modified source code from preprocesors in the form of sentences 
* patterns explain what can be tokens and patterns are defined by regex
* Q: How does this relate to DFAs and NFAs?
  * finite languages can be described by regular expressions and regular expressions can be formed or described by FAs 
  * [Tutorial](https://www.tutorialspoint.com/compiler_design/compiler_design_lexical_analysis.htm#:~:text=Finite-,Automata,-Finite%20automata%20is)

## Syntax analysis
* uses a CFG because things liked balanced parens cannot be checked by a regular expression 
* also described as a Parser 
* takes a token stream from a lexical analyzer and checks for any errors
* the output of the SA is a parse tree 
* 

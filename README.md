# Ex-4-LETTER-FOLLOWED-BY-ANY-NUMBER-OF-LETTERS-OR-DIGITS-USING-YACC-USING-YACC
RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
# Date:
# Aim:
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a statement as input and the valid variables are identified as output.
# PROGRAM
### var.l
```
%{
#include "y.tab.h"
#include <stdio.h>
%}

%%

"int" { return INT; } 
"float" { return FLOAT; }
"double" { return DOUBLE; }

[a-zA-Z][a-zA-Z0-9]* {
    printf("\nIdentifier is %s", yytext);
    return ID;
}

[ \t] { /* ignore whitespace */ }
\n { return 0; } 

. { return yytext[0]; } 

%%

int yywrap() { 
    return 1; 
}

```
### var.y
```
%{
#include <stdio.h>
#include <stdlib.h>

void yyerror(char *s);
int yylex(void);
%}

%token ID INT FLOAT DOUBLE

%% 
D: T L; 
L: L ',' ID   | ID; 
T: INT | FLOAT | DOUBLE; 

%% 

extern FILE *yyin;

int main() {
    
    // yyin = fopen("input.txt", "r");
    
    do {
        yyparse();
    } while (!feof(yyin)); 
    return 0;
}

void yyerror(char *s) { 
    fprintf(stderr, "Error: %s\n", s); 
}

```
# Output
![Screenshot from 2024-10-22 11-25-06](https://github.com/user-attachments/assets/db59caeb-8b83-41e2-9fb3-799e8b5b3382)


# Result
A YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.

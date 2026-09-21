# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
## DATE:25.08.26

# Name: S.Senthil velan 
# Reg.No: 212223225002

# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.

# ALGORITHM
1.	Start the program.

2.	Write a program in the vi editor and save it with .l extension.

3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.

4.	Write a program in the vi editor and save it with .y extension.

5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l

6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y

7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c

8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM
```python
%{
#include "exp3cd_0117.tab.h"
#include <stdio.h>
%}

%%

[0-9]+                  { return NUMBER; }
[a-zA-Z][a-zA-Z0-9]*    { return ID; }

"+"     { return '+'; }
"-"     { return '-'; }
"*"     { return '*'; }
"/"     { return '/'; }
"("     { return '('; }
")"     { return ')'; }

[ \t]   ;          /* ignore spaces */
\n      return 0;

.       return yytext[0];

%%

int yywrap()
{
    return 1;
}
```
```python
%{
#include <stdio.h>
#include <stdlib.h>

int yylex();
void yyerror(const char *s);

int valid = 1;
%}

%token NUMBER ID

%%

statement:
        expr
        {
            if(valid)
                printf("\nValid Arithmetic Expression\n");
        }
        ;

expr:
        expr '+' term
      | expr '-' term
      | term
      ;

term:
        term '*' factor
      | term '/' factor
      | factor
      ;

factor:
        '(' expr ')'
      | NUMBER
      | ID
      ;

%%

int main()
{
    printf("Enter Expression:\n");
    yyparse();
    return 0;
}

void yyerror(const char *s)
{
    valid = 0;
    printf("\nInvalid Arithmetic Expression\n");
}
```
# OUTPUT
<img width="912" height="689" alt="Screenshot 2026-05-12 115221" src="9b195oa4Ho (1).png" />

# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.

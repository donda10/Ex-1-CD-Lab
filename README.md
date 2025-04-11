# Ex-1 IMPLEMENTATION-OF-SYMBOL-TABLE
# Register Number : 212224040318
# Date : 11/04/2025
# AIM :
## To write a C program to implement a symbol table.
# ALGORITHM
1.	Start the program.
2.	Get the input from the user with the terminating symbol ‘$’.
3.	Allocate memory for the variable by dynamic memory allocation function.
4.	If the next character of the symbol is an operator then only the memory is allocated.
5.	While reading, the input symbol and memory address are inserted into the symbol table.
6.	The steps are repeated till ‘$’ is reached.
7.	To reach a variable, enter the variable to be searched and the symbol table has been checked for the corresponding variable, the variable along with its address is displayed as a result.
8.	Stop the program. 
# PROGRAM
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

#define MAX_SYMBOLS 100

typedef struct {
    char symbol;
    int *address;
    char type[20];
} SymbolTableEntry;

int main() {
    SymbolTableEntry table[MAX_SYMBOLS];
    int symbolCount = 0;
    char input[256];
    int i = 0;

    printf("Enter the Expression terminated by $: ");
    fgets(input, sizeof(input), stdin);
    printf("Given Expression: %s\n", input);

    while (input[i] != '$' && input[i] != '\0') {
        if (isalpha(input[i])) {
            char variable = input[i];
            int exists = 0;
            for (int j = 0; j < symbolCount; j++) {
                if (table[j].symbol == variable) {
                    exists = 1;
                    break;
                }
            }
            if (!exists) {
                int *memory = (int *)malloc(sizeof(int));
                table[symbolCount].symbol = variable;
                table[symbolCount].address = memory;
                strcpy(table[symbolCount].type, "identifier");
                symbolCount++;
            }
        }
        i++;
    }

    printf("\nSymbol Table\n");
    printf("Symbol\taddr\t\ttype\n");
    for (int j = 0; j < symbolCount; j++) {
        printf("%c\t%p\t%s\n", table[j].symbol, (void *)table[j].address, table[j].type);
    }

    char searchVar;
    printf("\nThe symbol to be searched: ");
    scanf(" %c", &searchVar);

    int found = 0;
    for (int j = 0; j < symbolCount; j++) {
        if (table[j].symbol == searchVar) {
            printf("Symbol Found\n");
            printf("%c@address %p\n", table[j].symbol, (void *)table[j].address);
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Symbol not found in table.\n");
    }

    for (int j = 0; j < symbolCount; j++) {
        free(table[j].address);
    }

    printf("\n=== Code Execution Successful ===\n");
    return 0;
}


```
# OUTPUT

![Screenshot 2025-04-11 161502](https://github.com/user-attachments/assets/4a102b87-a58d-49ed-8b3f-b63d5afd6e89)

![Screenshot 2025-04-11 161556](https://github.com/user-attachments/assets/e980217a-9f43-49a0-b6d5-27d11ea668fe)

# RESULT
### The program to implement a symbol table is executed and the output is verified.

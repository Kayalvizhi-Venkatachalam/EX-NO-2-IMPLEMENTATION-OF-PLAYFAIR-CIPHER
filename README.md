## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




Program:
```
#include <stdio.h>
#include <string.h>

int main()
{
    int key[3][3];
    int plain[100], cipher[100];
    char msg[100];
    int i, j, k, sum, len;

    printf("Enter Plain Text (UPPERCASE): ");
    scanf("%s", msg);

    printf("Enter the 3x3 Key Matrix:\n");
    for(i = 0; i < 3; i++)
    {
        for(j = 0; j < 3; j++)
        {
            scanf("%d", &key[i][j]);
        }
    }

    len = strlen(msg);

    // Padding with X if length is not multiple of 3
    while(len % 3 != 0)
    {
        msg[len] = 'X';
        len++;
    }
    msg[len] = '\0';

    // Convert letters to numbers
    for(i = 0; i < len; i++)
    {
        plain[i] = msg[i] - 'A';
    }

    // Encrypt block by block
    for(k = 0; k < len; k += 3)
    {
        for(i = 0; i < 3; i++)
        {
            sum = 0;
            for(j = 0; j < 3; j++)
            {
                sum += key[i][j] * plain[k + j];
            }
            cipher[k + i] = sum % 26;
        }
    }

    printf("\nCipher Text: ");
    for(i = 0; i < len; i++)
    {
        printf("%c", cipher[i] + 'A');
    }

    return 0;
}

```



OUTPUT:
<img width="1847" height="797" alt="OUTPUT EX 2" src="https://github.com/user-attachments/assets/3911d6fb-72df-4032-9426-ef9352d48874" />




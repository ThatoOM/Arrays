# Arrays
Caesar
# Caesar Cipher Implementation

I'll design and implement a program that encrypts messages using Caesar's cipher according to the specifications provided.

## Approach
1. **Command-line argument validation**: Check for exactly one argument and verify it's a numeric value
2. **Key processing**: Convert the string argument to an integer
3. **Input handling**: Get plaintext from the user
4. **Encryption**: Rotate each alphabetical character by the key while preserving case and leaving non-alphabetical characters unchanged
5. **Output**: Display the ciphertext

## Solution Code
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <stdlib.h>

int is_digit_string(const char *str);

int main(int argc, char *argv[])
{
    // Check for correct number of arguments
    if (argc != 2)
    {
        printf("Usage: ./caesar key\n");
        return 1;
    }

    // Check if argument is a valid digit string
    if (!is_digit_string(argv[1]))
    {
        printf("Usage: ./caesar key\n");
        return 1;
    }

    // Convert the key to an integer
    int key = atoi(argv[1]);

    // Get plaintext from user
    printf("plaintext:  ");
    char plaintext[1024];
    fgets(plaintext, sizeof(plaintext), stdin);

    // Remove newline character if present
    plaintext[strcspn(plaintext, "\n")] = '\0';

    printf("ciphertext: ");

    // Encrypt each character
    for (int i = 0; plaintext[i] != '\0'; i++)
    {
        char c = plaintext[i];
        if (isalpha(c))
        {
            char base = isupper(c) ? 'A' : 'a';
            c = (c - base + key) % 26 + base;
        }
        printf("%c", c);
    }

    printf("\n");
    return 0;
}

// Helper function to check if string consists only of digits
int is_digit_string(const char *str)
{
    for (int i = 0; str[i] != '\0'; i++)
    {
        if (!isdigit(str[i]))
        {
            return 0;
        }
    }
    return 1;
}
```

## Explanation
1. **Command-line Validation**: The program first checks if exactly one command-line argument was provided. If not, it prints the usage message and exits with error code 1.

2. **Digit Check**: The helper function `is_digit_string` verifies that all characters in the argument are digits. If any non-digit is found, it prints the usage message and exits.

3. **Key Conversion**: The valid digit string is converted to an integer using `atoi`.

4. **Plaintext Input**: The program prompts for plaintext using `fgets` to safely read input and removes any trailing newline character.

5. **Encryption Process**:
   - For each character in the plaintext:
     - If it's an alphabetical character, determine its case (upper or lower)
     - Calculate the rotated position using modulo 26 arithmetic to handle wrap-around
     - Non-alphabetical characters are left unchanged
6. **Output**: The ciphertext is printed character by character, followed by a newline.


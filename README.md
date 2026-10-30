# VIGENERE-CIPHER
## EX. NO: 4
 

## IMPLEMETATION OF VIGENERE CIPHER
 

## AIM:

To implement the Vigenere Cipher substitution technique using C program.

## DESCRIPTION:

To encrypt, a table of alphabets can be used, termed a tabula recta, Vigenère square,or Vigenère table. It consists of the alphabet written out 26 times in differnt rows, each
 
alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses adifferent alphabet from one of the rows. The alphabet used at each point repeating keyword.depends on a Each row starts with a key letter. The remainder of the row holds the letters A to Z. Although there are 26 key rows shown, you will only use as many keys as there are unique letters in the key string, here just 5 keys, {L, E, M, O, N}. For successive letters of the message, we are going to take successive letters of the key string, and encipher each message letter using its corresponding key row. Choose the next letter of the key, go along that row to find the column heading that	atches the message character; the letter at the intersection of
[key-row, msg-col] is the enciphered letter.


## ALGORITHM:

STEP-1: Arrange the alphabets in row and column of a 26*26 matrix.
STEP-2: Circulate the alphabets in each row to position left such that the first letter is attached to last.
STEP-3: Repeat this process for all 26 rows and construct the final key matrix.
STEP-4: The keyword and the plain text is read from the user.
STEP-5: The characters in the keyword are repeated sequentially so as to match with that of the plain text.
STEP-6: Pick the first letter of the plain text and that of the keyword as the row indices and column indices respectively.
STEP-7: The junction character where these two meet forms the cipher character.
STEP-8: Repeat the above steps to generate the entire cipher text.


## PROGRAM:
     #include <ctype.h>
     #include <stdio.h>
     #include <string.h>

     int main(void)
    {
    char plaintext[500];
    char keyword[100];
    char ciphertext[500];
    size_t keyLength;
    size_t keyIndex = 0;

    printf("Enter the plaintext: ");
    if (fgets(plaintext, sizeof(plaintext), stdin) == NULL)
        return 1;

    plaintext[strcspn(plaintext, "\n")] = '\0';

    printf("Enter the keyword: ");
    if (fgets(keyword, sizeof(keyword), stdin) == NULL)
        return 1;

    keyword[strcspn(keyword, "\n")] = '\0';
    keyLength = strlen(keyword);

    if (keyLength == 0) {
        printf("Keyword cannot be empty.\n");
        return 1;
    }

    /* Check that the keyword contains only letters. */
    for (size_t i = 0; i < keyLength; i++) {
        if (!isalpha((unsigned char)keyword[i])) {
            printf("Keyword must contain only letters.\n");
            return 1;
        }
        keyword[i] = (char)toupper((unsigned char)keyword[i]);
    }

    for (size_t i = 0; plaintext[i] != '\0'; i++) {
        unsigned char ch = (unsigned char)plaintext[i];

        if (isalpha(ch)) {
            int plainValue = toupper(ch) - 'A';
            int keyValue = keyword[keyIndex % keyLength] - 'A';
            int cipherValue = (plainValue + keyValue) % 26;

            ciphertext[i] = (char)('A' + cipherValue);
            keyIndex++;
        } else {
            /* Keep spaces and punctuation; they do not use a key letter. */
            ciphertext[i] = (char)ch;
        }
    }

    ciphertext[strlen(plaintext)] = '\0';

    printf("Ciphertext: %s\n", ciphertext);

    return 0;
}

## OUTPUT
<img width="300" height="77" alt="Screenshot 2026-10-30 122316" src="https://github.com/user-attachments/assets/41f39da1-8af6-43dd-b016-569aa9d22606" />


## RESULT:
The Vigenere cipher program was implemented and executed successfully. The plaintext was encrypted using the
keyword, and the ciphertext was displayed.

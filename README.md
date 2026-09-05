# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:
```
#include <stdio.h>
#include <string.h>

unsigned long generateMAC(char key[], char message[])
{
    unsigned long hash = 5381;
    int i;

    // Process the secret key
    for(i = 0; key[i] != '\0'; i++)
    {
        hash = ((hash << 5) + hash) + key[i];
    }

    // Process the message
    for(i = 0; message[i] != '\0'; i++)
    {
        hash = ((hash << 5) + hash) + message[i];
    }

    return hash;
}

int main()
{
    char message[100];
    char key[100];
    char received[100];
    unsigned long mac1, mac2;

    printf("====================================\n");
    printf("       MESSAGE AUTHENTICATION CODE\n");
    printf("====================================\n");

    printf("Enter the message: ");
    scanf("%s", message);

    printf("Enter the secret key: ");
    scanf("%s", key);

    // Generate MAC
    mac1 = generateMAC(key, message);

    printf("\nOriginal Message : %s", message);
    printf("\nSecret Key       : %s", key);
    printf("\nGenerated MAC    : %lu", mac1);

    // Read received message
    printf("\n\nEnter received message: ");
    scanf("%s", received);

    // Generate MAC for received message
    mac2 = generateMAC(key, received);

    printf("Received MAC     : %lu", mac2);

    // Verify MAC
    if(mac1 == mac2)
    {
        printf("\n\nMAC Verification Successful!");
        printf("\nMessage is authentic and unchanged.");
    }
    else
    {
        printf("\n\nMAC Verification Failed!");
        printf("\nMessage has been modified.");
    }

    return 0;
}
```
## Output:
<img width="1784" height="691" alt="Screenshot (587)" src="https://github.com/user-attachments/assets/fa0da29a-a37b-4049-b5c9-6daf3ff24c29" />


## Result:
The program is executed successfully.

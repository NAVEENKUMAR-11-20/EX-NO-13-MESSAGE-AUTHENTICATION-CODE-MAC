EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

AIM:

To implement MESSAGE AUTHENTICATION CODE(MAC)

ALGORITHM:

Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

Initialization:

Choose a cryptographic hash function ( H ) (e.g., SHA-256) and a secret key ( K ).
The message ( M ) to be authenticated is input along with the secret key ( K ).
MAC Generation:

Compute the MAC by applying the hash function to the combination of the message ( M ) and the secret key ( K ): [ \text{MAC}(M, K) = H(K || M) ] where ( || ) denotes concatenation of ( K ) and ( M ).
Verification:

The recipient, who knows the secret key ( K ), computes the MAC using the received message ( M ) and the same hash function.
The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.
Security: The security of the MAC relies on the secret key ( K ) and the strength of the hash function ( H ), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

Program:

```c
#include <stdio.h>
#include <string.h>
#define MAC_SIZE 32

// Simple XOR-based MAC computation
void computeMAC(const char *key, const char *message, char *mac) {
    int key_len = strlen(key);
    int msg_len = strlen(message);
    for (int i = 0; i < MAC_SIZE; i++) {
        mac[i] = key[i % key_len] ^ message[i % msg_len];
    }
}

// Helper to print MAC in hexadecimal
void printMAC(const char *mac) {
    for (int i = 0; i < MAC_SIZE; i++) {
        printf("%02x", (unsigned char)mac[i]);
    }
    printf("\n");
}

int main() {
    char key[100], message[100];
    char mac[MAC_SIZE], receivedMAC[MAC_SIZE];

    printf("Enter the secret key: ");
    scanf("%s", key);

    printf("Enter the message: ");
    scanf("%s", message);

    // Compute MAC
    computeMAC(key, message, mac);

    printf("Computed MAC (in hex): ");
    printMAC(mac);

    printf("Enter the received MAC (as hex, 64 hex digits): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        unsigned int val;
        scanf("%2x", &val);
        receivedMAC[i] = (char)val;
    }

    // Verify MAC
    if (memcmp(mac, receivedMAC, MAC_SIZE) == 0) {
        printf("MAC verification successful. Message is authentic.\n");
    } else {
        printf("MAC verification failed. Message is not authentic.\n");
    }

    return 0;
}
```

Output:
<img width="869" height="328" alt="image" src="https://github.com/user-attachments/assets/afd5c296-a2d5-486b-80f9-2ac0dd06b41e" />



Result:

The program is executed successfully.

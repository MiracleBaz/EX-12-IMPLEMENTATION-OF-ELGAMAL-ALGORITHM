
## AIM:

To implement the ElGamal encryption and decryption algorithm using C for secure communication.


## ALGORITHM:
1.	Choose a large prime number p and a primitive root g of p.
2.	Select a private key x such that 1 < x < p.
3.	Compute the public key y = g^x mod p.
4.	To encrypt a message M:
a.	Choose a random integer k such that 1 < k < p.
b.	Compute C1 = g^k mod p.
c.	Compute C2 = (M * y^k) mod p.
d.	The ciphertext is the pair (C1, C2).
5.	To decrypt the ciphertext (C1, C2):
a.	Compute s = C1^(p-1-x) mod p.
b.	Compute the original message M = (C2 * s) mod p.
6.	Display the decrypted message.


## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>

int modular_exponentiation(int base, int exp, int mod)
{
    int result = 1;
    base = base % mod;
    while (exp > 0)
    {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int main()
{
    int p, g, x, k, M;
    int y, C1, C2, decrypted_message;

    printf("Enter a prime number p: ");
    scanf("%d", &p);
    printf("Enter a primitive root g of p: ");
    scanf("%d", &g);
    printf("Enter the private key x: ");
    scanf("%d", &x);

    y = modular_exponentiation(g, x, p);
    printf("Public key y: %d\n", y);

    printf("Enter the message (integer) to encrypt: ");
    scanf("%d", &M);
    printf("Enter a random integer k: ");
    scanf("%d", &k);

    C1 = modular_exponentiation(g, k, p);
    C2 = (M * modular_exponentiation(y, k, p)) % p;
    printf("Encrypted message: (C1, C2) = (%d, %d)\n", C1, C2);

    decrypted_message = (C2 * modular_exponentiation(C1, p - 1 - x, p)) % p;
    printf("Decrypted message: %d\n", decrypted_message);

    return 0;
}
```

## OUTPUT:

<img width="815" height="432" alt="Screenshot 2025-10-25 144720" src="https://github.com/user-attachments/assets/b0d981af-90a0-4354-a999-cd3c6ec3ac45" />

## RESULT:

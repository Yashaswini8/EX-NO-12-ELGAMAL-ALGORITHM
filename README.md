# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
NAME:YASHASWINI S
REGISTER NO:212224220123
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

// Function for modular exponentiation
long long mod_exp(long long base, long long exp, long long mod)
{
    long long result = 1;
    base = base % mod;

    while(exp > 0)
    {
        if(exp % 2 == 1)
            result = (result * base) % mod;

        base = (base * base) % mod;
        exp = exp / 2;
    }

    return result;
}

// Function to find modular inverse
long long mod_inverse(long long a, long long m)
{
    long long m0 = m, t, q;
    long long x0 = 0, x1 = 1;

    if (m == 1)
        return 0;

    while (a > 1)
    {
        q = a / m;
        t = m;

        m = a % m;
        a = t;
        t = x0;

        x0 = x1 - q * x0;
        x1 = t;
    }

    if (x1 < 0)
        x1 += m0;

    return x1;
}

int main()
{
    long long p, g, x, y;
    long long m, k;
    long long a, b, s, s_inv, decrypted;

    printf("Enter prime number (p): ");
    scanf("%lld", &p);

    printf("Enter generator (g): ");
    scanf("%lld", &g);

    printf("Enter private key (x): ");
    scanf("%lld", &x);

    // Public key generation
    y = mod_exp(g, x, p);

    printf("Public key (p, g, y): (%lld, %lld, %lld)\n", p, g, y);
    printf("Private key: %lld\n", x);

    printf("Enter message: ");
    scanf("%lld", &m);

    printf("Enter random number (k): ");
    scanf("%lld", &k);

    // Encryption
    a = mod_exp(g, k, p);
    b = (m * mod_exp(y, k, p)) % p;

    printf("Encrypted message (a, b): (%lld, %lld)\n", a, b);

    // Decryption
    s = mod_exp(a, x, p);
    s_inv = mod_inverse(s, p);

    decrypted = (b * s_inv) % p;

    printf("Decrypted message: %lld\n", decrypted);

    return 0;
}
```

## Output:


## Result:
The program is executed successfully.

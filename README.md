# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```
#include <stdio.h>

int gcd(int a, int b) {
    while (b) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int mod_exp(int base, int exp, int mod) {
    int result = 1;
    base %= mod;
    while (exp) {
        if (exp % 2) result = (result * base) % mod;
        exp /= 2;
        base = (base * base) % mod;
    }
    return result;
}

int mod_inverse(int e, int phi) {
    int t = 0, new_t = 1, r = phi, new_r = e;
    while (new_r) {
        int q = r / new_r;
        t = new_t - q * (new_t = t);
        r = new_r - q * (new_r = r);
    }
    return r > 1 ? -1 : (t < 0 ? t + phi : t);
}

int main() {
    int p, q, n, phi, e, d, message;

    printf("Enter two primes (p and q): ");
    scanf("%d %d", &p, &q);

    n = p * q;
    phi = (p - 1) * (q - 1);

    do {
        printf("Enter public key exponent (1 < e < %d, gcd(e, phi) = 1): ", phi);
        scanf("%d", &e);
    } while (gcd(e, phi) != 1);

    if ((d = mod_inverse(e, phi)) == -1) {
        printf("No modular inverse for 'e'.\n");
        return 1;
    }

    printf("Public key: (n = %d, e = %d)\nPrivate key: (n = %d, d = %d)\n", n, e, n, d);

    printf("Enter message to encrypt: ");
    scanf("%d", &message);

    printf("Encrypted: %d\nDecrypted: %d\n", mod_exp(message, e, n), mod_exp(mod_exp(message, e, n), d, n));

    return 0;
}

```



## Output:



![image](https://github.com/user-attachments/assets/5dabc437-a933-4abf-a7d6-f5e8b8e0e6ac)


## Result:
 The program is to Implement RSA Encryption Algorithm in Cryptography was executed successfully.

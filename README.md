 ## IMPLEMENTATION OF RSA
 # AIM :
 To write a C program to implement the RSA encryption algorithm.

## ALGORITHM:
STEP-1: Select two co-prime numbers as p and q.

STEP-2: Compute n as the product of p and q.

STEP-3: Compute (p-1)*(q-1) and store it in z.

STEP-4: Select a random prime number e that is less than that of z.

STEP-5: Compute the private key, d as e *
mod-1
(z).

STEP-6: The cipher text is computed as messagee *

STEP-7: Decryption is done as cipherdmod n.

## PROGRAM:
```
#include<stdio.h>  
#include<stdlib.h>  
#include<math.h>  
#include<string.h>  
  
long int p, q, n, t, flag, e[100], d[100], temp[100], j, m[100], en[100], i;  
char msg[100];  
  
int prime(long int);  
void ce();  
long int cd(long int);  
void encrypt();  
void decrypt();  
  
int main()  
{  
    printf("ENTER FIRST PRIME NUMBER: ");  
    scanf("%ld", &p);  
    flag = prime(p);  
    if (flag == 0 || p == 1)  
    {  
        printf("WRONG INPUT\n");  
        exit(1);  
    }  
  
    printf("ENTER ANOTHER PRIME NUMBER: ");  
    scanf("%ld", &q);  
    flag = prime(q);  
    if (flag == 0 || q == 1 || p == q)  
    {  
        printf("WRONG INPUT\n");  
        exit(1);  
    }  
  
    printf("ENTER MESSAGE: ");  
    scanf(" %[^\n]s", msg);  
    for (i = 0; i < strlen(msg); i++)  
        m[i] = msg[i];  
  
    n = p * q;  
    t = (p - 1) * (q - 1);  
  
    ce();  
  
    printf("\nPOSSIBLE VALUES OF e AND d ARE:\n");  
    for (i = 0; i < j - 1; i++)  
        printf("%ld\t%ld\n", e[i], d[i]);  
  
    encrypt();  
    decrypt();  
  
    return 0;  
}  
  
int prime(long int pr)  
{  
    int i;  
    if (pr == 1)  
        return 0;  
  
    for (i = 2; i <= sqrt(pr); i++)  
    {  
        if (pr % i == 0)  
            return 0;  
    }  
    return 1;  
}  
  
void ce()  
{  
    int k;  
    k = 0;  
    for (i = 2; i < t; i++)  
    {  
        if (t % i == 0)  
            continue;  
        flag = prime(i);  
        if (flag == 1 && i != p && i != q)  
        {  
            e[k] = i;  
            flag = cd(e[k]);  
            if (flag > 0)  
            {  
                d[k] = flag;  
                k++;  
            }  
            if (k == 99)  
                break;  
        }  
    }  
}  
  
long int cd(long int x)  
{  
    long int k = 1;  
    while (1)  
    {  
        k = k + t;  
        if (k % x == 0)  
            return (k / x);  
    }  
}  
  
void encrypt()  
{  
    long int pt, ct, key = e[0], k, len;  
    i = 0;  
    len = strlen(msg);  
    while (i < len)  
    {  
        pt = m[i];  
        pt = pt - 96;  
        k = 1;  
        for (j = 0; j < key; j++)  
        {  
            k = k * pt;  
            k = k % n;  
        }  
        temp[i] = k;  
        ct = k + 96;  
        en[i] = ct;  
        i++;  
    }  
    en[i] = -1;  
    printf("\nTHE ENCRYPTED MESSAGE IS:\n");  
    for (i = 0; en[i] != -1; i++)  
        printf("%c", (char)en[i]);  
}  
  
void decrypt()  
{  
    long int pt, ct, key = d[0], k;  
        i = 0;  
    while (en[i] != -1)  
    {  
        ct = temp[i];  
        k = 1;  
        for (j = 0; j < key; j++)  
        {  
            k = k * ct;  
            k = k % n;  
        }  
        pt = k + 96;  
        m[i] = pt;  
        i++;  
    }  
    m[i] = -1;  
    printf("\nTHE DECRYPTED MESSAGE IS:\n");  
    for (i = 0; m[i] != -1; i++)  
        printf("%c", (char)m[i]);  
}  
```
## OUTPUT:
![exp2](https://github.com/kanmanikannu/19CS412---CRYPTOGRAPHY---ADVANCED-ENCRYPTION/assets/114866367/6b1ac77c-5b0b-4d2d-81e5-3be10897ecae)


## RESULT :

Thus the C program to implement RSA encryption technique had been
implemented successfully





## IMPLEMENTATION OF DIFFIE HELLMAN KEY EXCHANGE ALGORITHM

## AIM:

To implement the Diffie-Hellman Key Exchange algorithm using C language.


## ALGORITHM:

STEP-1: Both Alice and Bob shares the same public keys g and p.

STEP-2: Alice selects a random public key a.

STEP-3: Alice computes his secret key A as g
a mod p.

STEP-4: Then Alice sends A to Bob.


STEP-5: Similarly Bob also selects a public key b and computes his secret
key as B and sends the same back to Alice.


STEP-6: Now both of them compute their common secret key as the other
one’s secret key power of a mod p.

## PROGRAM: 

```
#include <math.h>
#include <stdio.h>
// Power function to return value of a ^ b mod P
long long int power(long long int a, long long int b,
long long int P)
{
if (b == 1)
return a;
else
return (((long long int)pow(a, b)) % P);
}
int main()
{
long long int P, G, x, a, y, b, ka, kb;
// Both the persons will be agreed upon the
// public keys G and P
printf("Enter the value of P:");
scanf("%lld",&P); // A prime number P is taken
printf("The value of P : %lld\n", P);
printf("Enter the value of G:");
scanf("%lld",&G); // A primitive root for P, G is taken
printf("The value of G : %lld\n\n", G);
// Alice will choose the private key a
a = 4; // a is the chosen private key
printf("The private key a for Alice : %lld\n", a);
x = power(G, a, P); // gets the generated key
// Bob will choose the private key b
b = 3; // b is the chosen private key
printf("The private key b for Bob : %lld\n\n", b);
y = power(G, b, P); // gets the generated key
// Generating the secret key after the exchange
// of keys
ka = power(y, a, P); // Secret key for Alice
kb = power(x, b, P); // Secret key for Bob
printf("Secret key for the Alice is : %lld\n", ka);
printf("Secret Key for the Bob is : %lld\n", kb);
return 0;
}
```
## OUTPUT:

<img width="342" alt="image" src="https://github.com/AlluguriSrikrishnateja/19CS412---CRYPTOGRAPHY---ADVANCED-ENCRYPTION/assets/118343892/a3f5b0fa-ef81-4215-9521-2a16c87cef68">


## RESULT: 

Thus the Diffie-Hellman key exchange algorithm had been successfully
implemented using C.





## IMPLEMENTATION OF DES ALGORITHM

## AIM:
To write a program to implement Data Encryption Standard (DES)

## ALGORITHM :

STEP-1: Read the 64-bit plain text.

STEP-2: Split it into two 32-bit blocks and store it in two different arrays.

STEP-3: Perform XOR operation between these two arrays.

STEP-4: The output obtained is stored as the second 32-bit sequence and the
original second 32-bit sequence forms the first part.

STEP-5: Thus the encrypted 64-bit cipher text is obtained in this way. Repeat the
same process for the remaining plain text characters.

### PROGRAM :

```
from cryptography.fernet import Fernet
message = input()
key = Fernet.generate_key()
fernet = Fernet(key)
encMessage = fernet.encrypt(message.encode())
print("original string: ", message)
print("encrypted string: ", encMessage)

decMessage = fernet.decrypt(encMessage).decode()
 
print("decrypted string: ", decMessage)
```
## OUTPUT:

<img width="756" alt="image" src="https://github.com/AlluguriSrikrishnateja/19CS412---CRYPTOGRAPHY---ADVANCED-ENCRYPTION/assets/118343892/23e74c08-7cea-4381-b9fe-97e247b17470">

## RESULT:

Thus the data encryption standard algorithm had been implemented
successfully.


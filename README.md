# Code-block-experiment-4
# 🔐 Code Block Experiment 4 – Encryption and Decryption (C Program)

## 📘 **Aim**
To implement a simple **encryption and decryption** mechanism using the **C programming language**.

---

## 💻 **Requirements**
- PC with **Linux Operating System**  
- **Code::Blocks IDE** or any C compiler  

---

## ⚙️ **Algorithm**
1. Open Code::Blocks and create a new C file.  
2. Write the encryption and decryption program.  
3. Save the file with the extension `.c`.  
4. Compile and run the program.  
5. Enter two prime numbers as input.  
   - If the number is not prime, display **"WRONG INPUT"**.  
6. Enter the message to be encrypted.  
7. Display the **encrypted message**.  
8. Display the **decrypted message** as final output.  
9. Verify that the decrypted message matches the original input.  

---

## 🧠 **Concept**
This program demonstrates **RSA-like encryption and decryption** using modular arithmetic and prime numbers.  
It converts characters to numbers, applies encryption using a public key, and decrypts using a private key.

---

## 🧩 **Program**

```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <string.h>

long int p, q, n, t, flag, e[100], d[100], temp[100], j, m[100], en[100], i;
char msg[100];

int prime(long int);
void ce();
long int cd(long int);
void encrypt();
void decrypt();

void main()
{
    printf("\nENTER FIRST PRIME NUMBER: ");
    scanf("%ld", &p);
    flag = prime(p);
    if (flag == 0)
    {
        printf("\nWRONG INPUT\n");
        exit(1);
    }

    printf("\nENTER ANOTHER PRIME NUMBER: ");
    scanf("%ld", &q);
    flag = prime(q);

    if (flag == 0 || p == q)
    {
        printf("\nWRONG INPUT\n");
        exit(1);
    }

    printf("\nENTER MESSAGE: ");
    fflush(stdin);
    scanf("%s", msg);

    for (i = 0; msg[i] != '\0'; i++)
        m[i] = msg[i];

    n = p * q;
    t = (p - 1) * (q - 1);
    ce();

    printf("\nPOSSIBLE VALUES OF e AND d ARE:\n");
    for (i = 0; i < j - 1; i++)
        printf("\n%ld\t%ld", e[i], d[i]);

    encrypt();
    decrypt();
}

int prime(long int pr)
{
    int i;
    j = sqrt(pr);
    for (i = 2; i <= j; i++)
    {
        if (pr % i == 0)
            return 0;
    }
    return 1;
}

void ce()
{
    int k = 0;
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
    j = k;
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

    while (i != len)
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

    printf("\nTHE ENCRYPTED MESSAGE IS: ");
    for (i = 0; en[i] != -1; i++)
        printf("%c", en[i]);
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

    printf("\nTHE DECRYPTED MESSAGE IS: ");
    for (i = 0; m[i] != -1; i++)
        printf("%c", m[i]);
}
```

## SAMPLE OUTPUT:

<img width="1920" height="1080" alt="Screenshot 2025-10-24 091258" src="https://github.com/user-attachments/assets/f9a7a29a-4190-489a-8c2c-5f165ea0244b" />


## RESULT:
Thus the encryption and decryption is implemented and the output is obtained and verified successfully

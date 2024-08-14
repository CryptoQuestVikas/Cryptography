# Cryptography

# **Cryptography Task**
> 01. “Xjnvw lc sluxjmw jsqm wjpmcqbg jg wqcxqmnvw; xjzjmmjd lc wjpm sluxjmw jsqm bqccqm zqy.” Zlwvzjxj Zpcvcol
> 2. if you are crarcking this task so using https://www.quipqiup.com/

# **Symmetric Encryption:**

## **GNU Privacy Guard**
The GNU Privacy Guard, also known as GnuPG or GPG, implements the OpenPGP standard.
> 1. We can encrypt a file using GnuPG (GPG) using the following command: ``gpg --symmetric --cipher-algo CIPHER message.txt``
> 2. You can decrypt using the following command: ``gpg --output original_message.txt --decrypt message.gpg``
> 3. The default output is in the binary OpenPGP format; however, if you prefer to create an ASCII armoured output, which can be opened in any text editor, you should add the option --armor. For example, ``gpg --armor --symmetric --cipher-algo CIPHER message.txt``

## **OpenSSL Project**
The OpenSSL Project maintains the OpenSSL software.
> 1. We can encrypt a file using OpenSSL using the following command: ``openssl aes-256-cbc -e -in message.txt -out encrypted_message``
> 2. We can decrypt the resulting file using the following command: ``openssl aes-256-cbc -d -in encrypted_message -out original_message.txt``
> 3. To make the encryption more secure and resilient against brute-force attacks, we can add ``-pbkdf2`` to use the Password-Based Key Derivation Function 2 (PBKDF2); moreover, we can specify the number of iterations on the password to derive the encryption key using ``-iter`` NUMBER. To iterate 10,000 times, the previous command would become: ``openssl aes-256-cbc -pbkdf2 -iter 10000 -e -in message.txt -out encrypted_message``
> 4. Consequently, the decryption command becomes: ``openssl aes-256-cbc -pbkdf2 -iter 10000 -d -in encrypted_message -out original_message.txt``


In the following questions, we will use ``gpg`` and ``openssl`` on the AttackBox to carry out symmetric encryption.

The necessary files for this task are located under ``/root/Rooms/cryptographyintro/task02.`` The zip file attached to this task can be used to tackle the questions of tasks 2, 3, 4, 5, and 6.

# **Asymmetric Encryption:**

> 1. ``openssl genrsa -out private-key.pem 2048``: With openssl, we used genrsa to generate an RSA private key. Using ``-out``, we specified that the resulting private key is saved as ``private-key.pem``. We added ``2048`` to specify a key size of ``2048 bits``.
> 2. ``openssl rsa -in private-key.pem -pubout -out public-key.pem``: Using ``openssl``, we specified that we are using the RSA algorithm with the rsa option. We specified that we wanted to get the public key using -pubout. Finally, we set the private key as input using ``-in`` ``private-key.pem ``and saved the output using ``-out`` ``public-key.pem``
> 3. ``openssl rsa -in private-key.pem -text -noout``: We are curious to see real RSA variables, so we used ``-text`` ``-noout``. The values of ``p, q, N, e,`` and ``d`` are ``prime1, prime2``, ``modulus, publicExponent, and privateExponent``, respectively.
> 4. If we already have the recipient’s public key, we can encrypt it with the command ``openssl pkeyutl -encrypt -in plaintext.txt -out ciphertext -inkey public-key.pem -pubin``
> 5. The recipient can decrypt it using the command  ``openssl pkeyutl -decrypt -in ciphertext -inkey private-key.pem -out decrypted.txt``

On the AttackBox, you can find the directory for this task located at /root/Rooms/cryptographyintro/task03; alternatively, you can use the task file from Task 2 to work on your own machine.


# Cryptography

# **Cryptography Task**
> 01. “Xjnvw lc sluxjmw jsqm wjpmcqbg jg wqcxqmnvw; xjzjmmjd lc wjpm sluxjmw jsqm bqccqm zqy.” Zlwvzjxj Zpcvcol
> 2. if you are crarcking this task so using https://www.quipqiup.com/
--
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

# **Diffie-Hellman Key Exchange**
1. Let’s take a look at actual Diffie-Hellman parameters. We can use ``openssl`` to generate them; we need to specify the option ``dhparam`` to indicate that we want to generate Diffie-Hellman parameters along with the specified size in bits, such as ``2048`` or ``4096``

2. In the console output below, we can view the prime number ``P`` and the generator ``G`` using the command ``openssl dhparam -in dhparams.pem -text -noout``. (This is similar to what we did with the RSA private key.)
> 1. Command : ``openssl dhparam -out dhparams.pem 2048``

# **Hashing**
> 1. ls -lh
> 2. sha256sum *
> 3. hexdump text1.txt -C
> 4. sha256sum text1.txt
## HMAC
> 1. The figure above represents the steps expressed in the following formula: H(K⊕opad,H(K⊕ipad,text)).

> 2. To calculate the HMAC on a Linux system, you can use any of the available tools such as ``hmac256`` (or ``sha224hmac``, ``sha256hmac``, ``sha384hmac``, and ``sha512hmac``, where the secret key is added after the option ``--key``). Below we show an example of calculating the HMAC using ``hmac256`` and ``sha256hmac`` with two different keys.
> 3. ``hmac256 s!Kr37 message.txt``
> 4. ``sha256hmac message.txt --key s!Kr37``

On the AttackBox, you can find the directory for this task located at /root/Rooms/cryptographyintro/task05; alternatively, you can use the task file from Task 2 to work on your own machine.

# **PKI and SSL/TLS**
You can use ``openssl`` to generate a certificate signing request using the command ``openssl req -new -nodes -newkey rsa:4096 -keyout key.pem -out cert.csr``. We used the following options:
```

    req -new create a new certificate signing request
    -nodes save private key without a passphrase
    -newkey generate a new private key
    rsa:4096 generate an RSA key of size 4096 bits
    -keyout specify where to save the key
    -out save the certificate signing request
```
Then you will be asked to answer a series of questions, as shown in the console output below.
> 1. ``openssl req -new -nodes -newkey rsa:4096 -keyout key.pem -out cert.csr``
``` Once the CSR file is ready, you can send it to a CA of your choice to get it signed and ready to use on your server.

Once the client, i.e., the browser, receives a signed certificate it trusts, the SSL/TLS handshake takes place. The purpose would be to agree on the ciphers and the secret key.

We have just described how PKI applies to the web and SSL/TLS certificates. A trusted third party is necessary for the system to be scalable.

For testing purposes, we have created a self-signed certificate. For example, the following command will generate a self-signed certificate.
```
> 2. ``openssl req -x509 -newkey -nodes rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 365``
> 3. The  ``-x509`` indicates that we want to generate a self-signed certificate instead of a certificate request. The ``-sha256`` specifies the use of the ``SHA-256`` digest. It will be valid for one year as we added ``-days 365``.
> 4. To answer the questions below, you need to inspect the certificate file ``cert.pem`` in the ``task06`` directory. You can use the following command to view your certificate: ``openssl x509 -in cert.pem -text``
On the AttackBox, you can find the directory for this task located at ``/root/Rooms/cryptographyintro/task06``; alternatively, you can use the task file from Task 2 to work on your own machine.

# **Authenticating with Passwords**
> **Question:** You were auditing a system when you discovered that the MD5 hash of the admin password is 3fc0a7acf087f549ac2b266baf94b8b1. What is the original password?
> **Answer :** qwerty123

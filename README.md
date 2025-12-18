# AES Encryption using Symmetric Cryptography

I was tasked with demonstrating symmetric encryption using AES on Kali Linux. The goal was to show secure file encryption, decryption, and a stronger approach using a random key instead of a password. I used OpenSSL throughout this task because it is available by default and widely trusted.

---

## Step 1: Encrypting a File Using AES-256

I started by encrypting a plaintext file called secret.txt using AES-256. This algorithm is fast and suitable for large files.

# Command used:
openssl enc -aes-256-cbc -pbkdf2 -salt -in newsecret.txt -out newsecret.enc -k yourpassword

What I did and why:
• I used -aes-256-cbc to apply AES with a 256 bit key in CBC mode.
• I added -pbkdf2 to strengthen the password derivation and slow brute force attempts.
• I enabled -salt to add randomness and block dictionary attacks.
• I specified newsecret.txt as the input file.
• I generated newsecret.enc as the encrypted output file.
• I supplied a password using -k for key generation.


At this point, the original file content was unreadable without the password.


<img width="1006" height="142" alt="image" src="https://github.com/user-attachments/assets/54070ba3-12a2-4e10-8539-1426369c346c" />

<img width="548" height="91" alt="image" src="https://github.com/user-attachments/assets/a828ea4d-df86-45a2-b437-4d7f6851a6c7" />

Before Encryption:

<img width="547" height="121" alt="image" src="https://github.com/user-attachments/assets/c4fc4d56-944d-4819-bef3-4b20c9ca8d49" />


After Encryption:

<img width="649" height="121" alt="image" src="https://github.com/user-attachments/assets/66673111-28f8-4044-b562-a5b6933a1bcf" />


---

## Step 2: Decrypting the AES-256 Encrypted File

Next, I verified the encryption by decrypting the file back to plaintext.

# Command used:
openssl enc -aes-256-cbc -pbkdf2 -d -in newsecret.enc -out decrypted.txt -k yourpassword

What happened:
• I used -d to enable decryption mode.
• I supplied the same password used during encryption.
• OpenSSL restored the original content into decrypted.txt.

I confirmed that the decrypted file matched the original secret.txt.


<img width="884" height="115" alt="image" src="https://github.com/user-attachments/assets/461161cf-b3fc-4815-a990-701ae628a199" />

Before Decryption:

<img width="584" height="73" alt="image" src="https://github.com/user-attachments/assets/7e181a06-7c10-4f56-b42a-70681a8b26ca" />


After Decryption:

<img width="541" height="82" alt="image" src="https://github.com/user-attachments/assets/58a5addf-0c90-4165-9e1a-7c19262bc3f1" />

---

## Step 3: Encrypting with a Random 256 Bit Key

To improve security, I moved away from passwords and generated a random key. This removes the risk of password exposure.

a. I generated a 256 bit key

# Command:
openssl rand -out aes.key 32

b. I then encrypted the file using the key

# Command:
openssl enc -aes-256-cbc -pbkdf2 -salt -in newsecret.txt -out newsecret.enc -pass file:./aes.key

c. For decryption, I used the same key file

# Command:
openssl enc -aes-256-cbc -pbkdf2 -d -in newsecret.enc -out decrypted.txt -pass file:./aes.key

Why this is more secure:

• The key is random and 32 bytes long.
• There is no human readable password to guess or leak.
• Access to the key file is required for decryption.

This method significantly improves confidentiality when handling sensitive data.

# NOTE: To view generated key command output, use the "xxd aes.key" command.

<img width="693" height="137" alt="image" src="https://github.com/user-attachments/assets/b1a1804d-49e7-42fb-a6a5-e7388459c3b7" />


To view encrypted key output,use the commands below:

<img width="814" height="205" alt="image" src="https://github.com/user-attachments/assets/2817768c-44c4-4677-97fa-14bd80c4ac1d" />


To view decrypted key output,use the commands below:

<img width="1011" height="213" alt="image" src="https://github.com/user-attachments/assets/6eae1231-8536-4df2-a37f-b4d9a125eddb" />

---

## Outcome:

Through this project, I demonstrated practical symmetric encryption using AES-256 on Kali Linux. I validated encryption, decryption, and key based security. This exercise reinforced how symmetric cryptography protects data at rest when implemented correctly.









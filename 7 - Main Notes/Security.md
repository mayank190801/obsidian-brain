
2024-07-17 10:07
Status: 
Tags:

# Security

### What is Security and Privacy?
- Distributed systems face unique challenges related to security and privacy due to their distributed nature, which makes them more vulnerable to attacks and data breaches

##### A. Authentication and Authorization
- Authentication is the process of verifying the identity of users, services, or nodes before allowing them access to the system.
- Authorization determines what actions or resources the authenticated entity is allowed to access.
##### B. Data Encryption
-  converting data into an encoded format that can only be decrypted and read by someone with the correct decryption key.
- Techniques like symmetric and asymmetric encryption, as well as protocols such as TLS/SSL, can be used to secure data in distributed systems.
##### C. Secure Communication
- Implementing secure communication protocols, such as TLS/SSL, IPSec, or application-level encryption, can help protect the integrity and confidentiality of data exchanged between nodes.
##### D. Intrusion Detection and Prevention
- designed to monitor network traffic, detect malicious activities or policy violations, and take appropriate actions to mitigate potential threats

### What is Authentication?
- Authentication is a crucial first step in securing a software system, ensuring that access is granted only to the right individuals, much like how the right people are allowed into a club or a private event.

**Types of Authentication**:
1. **Single-Factor Authentication (SFA)**: 
2. **Two-Factor Authentication (2FA)**: 
3. **Multi-Factor Authentication (MFA)**:

### What is Authorization?
- Authorization in software systems is like getting a specific wristband at a festival that allows you access to certain areas. It's about granting or denying permissions to do something after your identity is verified

 ##### Roles and Permissions
-  **Roles**: These are like different types of wristbands or badges. For example, an 'Admin' might have access to everything, while a 'User' has limited access.
- **Permissions**: Specific actions you're allowed to perform, like viewing, editing, or deleting information. If you're at a festival, it's like being allowed to enter backstage areas, VIP sections, or just the general area.
##### Examples - 
- File System Permissions
- Database Roles
- Web Application Privileges

### OAuth vs. JWT for Authentication

### JWT
- Full form - Json Web Tokens 
- **JWT** is a token format used in authorization and information exchange. It’s a JSON object encoded as a string, which is digitally signed, and optionally encrypted.
- A JWT typically consists of three parts: Header, Payload, and Signature.
- Stateless; it contains all the necessary information within the token.

What is Encoding
- In computers, encoding is the process of putting a sequence of characters (letters, numbers, punctuation, and certain symbols) into a specialized format for efficient transmission or storage.

![[Screenshot 2024-06-18 at 8.24.24 PM.png]]

![[Screenshot 2024-06-18 at 8.25.29 PM.png]]

Pros 
- Self contained, portable, dont require server side storage 
Cons
- As payload in not encrypted, hence it should not contain highly sensitive data 
- vulnerable to theft 
- poor performance due to large payload 

### OAuth
https://www.youtube.com/watch?v=t4-416mg6iU
- Authorization between services (but whyyy?)
- **OAuth** is an open standard for access delegation, commonly used as a way for users to grant websites or applications access to their information on other websites but without giving them the passwords.
- When third parties wants some data from your Google, Facebook account and you don't want to share the passwords 
- It is not an authentication protocol but a secure delegation mechanism
- Example -  A user logs into a third-party app using their Google account. OAuth allows the app to access some of the user’s Google account data, as authorized, without the need to share Google account credentials with the third-party app.It uses access tokens for authorization.
- Typically relies on server-side storage to keep track of the issued tokens

Security 
- **OAuth**: Security depends on the specific implementation but generally relies on SSL/TLS for security during token exchange.
- **JWT**: The token itself is secured by its digital signature.

### What is Encryption?
- Encryption transforms readable data (plaintext) into a scrambled, unreadable format (ciphertext). To turn it back into readable form, you need the correct decryption key.
- Important to keep the keys safe (complex task)
- Slow downs systems 
##### **Types of Encryption**:
1. **Symmetric Encryption**: Uses the same key for encrypting and decrypting data. Think of it as a lock and key system where the same key locks and unlocks the box.
2. **Asymmetric Encryption**: Uses two different keys – a public key for encryption and a private key for decryption. It's like having a public mailbox where anyone can drop a message (public key), but only you have the key to open it (private key).
##### Uses
- Data security
- Privacy
- Integrity of data









# **References**
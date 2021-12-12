#### X.509 Certificates
###### What is X.509 Certificates
**X.509** is a standard format for **public key certificates**, digital documents that securely associate cryptographic key pairs with identities such as websites, individuals, or organizations.

Common applications:
1. SSL/TLS and HTTPS for authenticated and encrypted web browsing
2. Code signing
3. Document signing

Certificate format includes:
1. Version of X.509 certificate
2. Signature algorithm
3. period of validity
4. Signature

![[Pasted image 20211212163921.png]]

###### Reasons to revoke a certificate before it expires
1. User's private key is compromised
2. User is no longer certified by this CA
3. CA's certificate is compromised
# Public Key Certificate System Demonstration
## Assignment Brief
**Public key certificate system**: Design a public key certificate system that involves one root CA, two sub-CAs and three clients:
- Implement functionalities for the root CA to generate its own private/public key pair.
- Develop functions for issuing certificates for clients, including necessary attributes such as client ID, public key, and validity period.
- Implement client registration functionality, allowing clients to provide their identity and public key.
- Develop a mechanism for clients to submit certificate requests to the CA. The request should be encrypted.
- Develop methods for validating certificates using the corresponding public keys and CA signatures.
- Implement mechanisms for certificate revocation in case of compromise or expiration.

## Preparation
- Repository  [link](https://github.com/simplehasan/public-key-infrastructure.git)
```bash
# Make the repo visibility to public

# 1. Clone the repo
git clone https://github.com/simplehasan/public-key-infrastructure.git

# 2. Go to code directory
cd public-key-infrastructure

# 3. Install requirements
pip3 install -r requirements.txt

# 4. Run the program
python3 app.py
```

---
> **Aaditya**
## 1. Root CA Initilization (menu 1)

🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/root_ca.py#L65)
- [ ] Input Root CA common name
- [ ] Display plaintext keypair (e), (d)
- [ ] Display PEM format of Keypair (public, private)
## 2. Root CA self signed certificate (menu 2 and 3)
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/root_ca.py#L119)
- [ ] Generate self-signed certificate for Root CA (menu 2)
- [ ] Display Certificate detail (menu 3)
## 3. Revoke Root CA certificate (menu 4)
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/root_ca.py#L193)
- [ ] Revoke root CA certificate
- [ ] Display the new certificate
- [ ] Display CRL certificate
> back to main menu, go to menu 2 (Sub CA)
## 4. Sub CA Initialization
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L64)
- [ ] Generate key pair (menu 1) - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L15)
- [ ] Display key pair in plain text - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L214)
- [ ] Display key pair in PEM format (inside key folder)
## 5. Sub CA Register Profile Data (Menu 2)
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L87)
- [ ] Input profile data - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L726)
- [ ] Display profile data in the folder (.txt and .sig file)
## 6. Sub CA Profile Data validation (Root CA Menu)
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L582)
- [ ] Open Root CA menu in new terminal
- [ ] Verify Sub CA profile Data (menu 5)
> Explanation : The Sub CA wont be able to generate CSR until Root CA verifies Sub CA’s profile, and create csr folder for Sub CA to submit their CSR. Root CA send back Sub CA profile with UUID (txt and sig file)
- [ ] Display Sub CA update profile folder
- [ ] Display Sub CA csr folder (commonName_csr)
## 6. Sub CA CSR generation and Encryption (Menu 3)
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L133)
- [ ] Generate CSR for Sub CA, input the target CSR signer (root) - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L103) 
- [ ] Display CSR file in the Sub CA csr folder
- [ ] Encrypt and send CSR file to Root CA (Menu 4) - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L203) and this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L139)
- [ ] Display encrypted CSR and AES Key - refer to this code
> Explanation: CSR will be encrypted using AES key (symmetric encryption) and the AES key will be [encrypted](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L269) using target CA (root) public key. The IV will be decoded into Base64. read
- [ ] Go to Root CA for CSR decrypt process

---
> **Tengku**
## 7. Sub CA Decryption and Certificate Issuance (Root CA menu)
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/root_ca.py#L225)
- [ ] Open Root CA menu, go to menu 6 to decrypt Sub CA CSR
- [ ] Input Sub CA common name
- [ ] Display encrypted CSR, compare with original CSR from Sub CA folder
- [ ] Issue certificate for Sub CA (menu 7) and input Sub CA’s common name - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/root_ca.py#L268)
- [ ] Display the certificate detail in terminal and folder, compare with this [online certificate decoder](https://www.sslshopper.com/certificate-decoder.html)
> Explanation: Root CA will verify the Sub CA csr first using Sub CA’s provided public key, and if it’s verified, Root CA will issue certificate for Sub CA
- [ ] Validate Sub CA certificate (menu 8), input sub CA common name - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L582)
- [ ] Show the validation status in terminal
> Open new terminal for client
## 8. Client Initialization
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/client.py#L65)
- [ ] Go to Client menu and initialize client key pair, input client’s common name (menu 1)
- [ ] Display client’s key pair in terminal and client’s folder
## 9. Register Client’s Profile
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/client.py#L72)
- [ ] Register Client’s Profile (menu 2)
- [ ] Fill the client’s data and display the result in folder -  refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/client.py#L55)
- [ ] Go to Sub CA terminal to validate the Client’s registration data
## 10. Process Client Registration (Sub CA menu)
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L285)
- [ ] Process client’s registration (menu 5), input client’s common name -  refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L502)
- [ ] Input Sub CA’s common name to sign the profile details including UUID
- [ ] Display the result in terminal and folder (client_profile, client_csr) - same as Sub CA method
> Go to client’s terminal
## 11. Client’s CSR generation and Encryption (Client Menu)
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/client.py#L122)
- [ ] Generate Client’s CSR (menu 3)
- [ ] Input target CA common name, e.g. subca1
- [ ] Input client’s common name e.g. client1
- [ ] Display generated CSR in terminal and folder, compare with this [online decoder](https://certlogik.com/decoder/)
- [ ] Encrypt client’s CSR and send to corresponding Sub CA (menu 4) - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/client.py#L191)
- [ ] Display the encrypted CSR in the folder
> Go to Sub CA’s terminal
## 12. Client’s CSR Decryption and Certificat Issuance (Sub CA Menu)
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L292)
- [ ] Decrypt and Sign Client’s CSR , input client’s common name (menu 6) - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L356)
- [ ] Display the decrypted CSR in terminal and folder
- [ ] Input certificate recipient’s common name (e.g. client1)
> Explanation: Sub CA will validate the client’s CSR first before sign issue certificate
- [ ] Display client’s certificate in terminal and folder, compare with this [online certificate decoder]()
> We can also match the certificate with the private key here: [Certificate Key Matcher](https://www.sslshopper.com/certificate-key-matcher.html)
- [ ] Validate Client’s certificate (menu 7), provide certificate issuer and certificate holder common name, display the validation result in terminal - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L448) and this code from [crypto_utils](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L582)

***[Note: All steps above can be repeated for each Sub CA and client]***

---
> **Abdullah**
## 13. Client Revocation Request
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/client.py#L287)
- [ ] Go to client’s terminal and open revocation request (menu 6)
- [ ] Provide the revocation reason
> Explanation: revocation request will create a json file containing client’s data (reason, cert serial number,  and cert itself) and client’s signature (to ensure the request is original from the client)
> Display request json file in folder
- [ ] Open Sub CA terminal to process the revocation request
## 14. Process Client Revocation request
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L522)
- [ ] Process client revocation request (menu 9)
- [ ] Display the result in terminal and folder (sub ca crl, client certficate)
- [ ] Verify client’s certificate (before client generate new certificate) using menu 7, provide certificate owner (e.g. client1) and certificate issuer (e.g. subca1) -  refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L448)
- [ ] Display the verification result in terminal
- [ ] Re-generate client’s key pair, details, and certificate using steps above

## 15. Sub CA Revocation Request
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L462)
- [ ] Go to Sub CA terminal and open Sub CA revocation request (menu 8)
- [ ] Provide the revocation reason
> Explanation: revocation request will create a json file containing Sub CA’s data (reason, cert serial number,  and cert itself) and SubCA signature (to ensure the request is original from the client)
> Display request json file in folder
- [ ] Open Root CA terminal to process the revocation request

## 16. Process Sub CA revocation request (Root Menu)
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/root_ca.py#L397)
- [ ] Process Sub CA revocation request (menu 9), confirm
- [ ] Provide the Sub CA common name (e.g. subca1)
- [ ] Display the result in terminal and RootCA’s crl folder
- [ ] Verify Sub CA’s certificate (menu 8) and display the result - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L582)
- [ ] Re-generate Sub CA keypair, details, and certificate using steps above

## 17. Root CA revocation Process
🧑‍💻 [source code](https://github.com/simplehasan/public-key-infrastructure/blob/main/root_ca.py#L193)
- [ ] Revoke own Root CA certifiate (menu 4)
- [ ] Display the result in terminal
- [ ] Try to verify SubCA’s certificate (menu 8) and show the result

## 18. Test
- [ ] Initialize another SubCA (generate key pair, register, and generate CSR)
- [ ] Client generate CSR to root CA (menu 3), it should be error
- [ ] Client generate CSR to another Sub CA (e.g. subca2) and another Sub CA (e.g. subca1) try to issue certificate for client (menu 6 - Sub CA) - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L303)
- [ ] Corresponding Sub CA issue certificate for client (menu 6 - Sub CA) , it should be failed because need certificate from root - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/sub_ca.py#L366)
- [ ] Root CA issue Sub CA certificate
- [ ] Repeate, corresponding Sub CA issue certificate for client (menu 6 - Sub CA) - success, and verify client’s certificate
- [ ] Client verify certificate from another CA (not the issuer CA), it should be error - refer to this [code](https://github.com/simplehasan/public-key-infrastructure/blob/main/crypto_utils.py#L631)
> ***Please make the repo visibility to private again 👀 !!!***

**THANK YOU 🙂**
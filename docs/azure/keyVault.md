# Azure Key Vault

`Azure Key Vault` is a product that stores secrets. Anything, almost, that an application needs to function that needs protection, provides access to sensitive data, or cannot be stored in plain text at any time or anyplace can be stored in Azure Key Vault. Items that can be encrypted and stored in a vault are:

1. Tokens
2. Certificates (.pfx)
3. Passwords
4. Encryption keys 
 
To access any item stored in a Key Vault, you must first be authenticated.

Azure Key Vault supports the following authentication capabilities, which have been
previously discussed:
1. `Service principals`
2. `Managed identities`


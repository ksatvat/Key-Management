# Key Management


## Key Management: Empty Encryption Key

### Abstract
Empty encryption keys can compromise security in a way that cannot be easily remedied.
### Explanation
It is never a good idea to use an empty encryption key. Not only does using an empty encryption key significantly reduce the protection afforded by a good encryption algorithm, but it also makes fixing the problem extremely difficult. After the offending code is in production, the empty encryption key cannot be changed without patching the software. If an account protected by the empty encryption key is compromised, the owners of the system must choose between security and availability.

Example: The following code initializes an encryption key variable to an empty string.

``
from Crypto.Ciphers import AES
cipher = AES.new("", AES.MODE_CFB, iv)
msg = iv + cipher.encrypt(b'Attack at dawn')
``


Not only will anyone who has access to the code be able to determine that it uses an empty encryption key, but anyone with even basic cracking techniques is much more likely to successfully decrypt any encrypted data. After the program ships, a software patch is required to change the empty encryption key. An employee with access to this information can use it to break into the system. Even if attackers only had access to the application's executable, they could extract evidence of the use of an empty encryption key.




## Key Management: Empty HMAC Key

### Abstract
Empty HMAC keys could compromise system security in a way that cannot be easily remedied.
### Explanation
It is never a good idea to use an empty HMAC key. The cryptographic strength of HMAC depends on the size of the secret key, which is used for the calculation and verification of the message authentication values. Using an empty key undermines the cryptographic strength of the HMAC function.

Example 1: The following code uses an empty key to compute the HMAC:

``
import hmac
mac = hmac.new("", plaintext).hexdigest()
``

The code in Example 1 may run successfully, but anyone who has access to it will be able to figure out that it uses an empty HMAC key. After the program ships, there is likely no way to change the empty HMAC key unless the program is patched. A devious employee with access to this information could use it to compromise the HMAC function. Also, the code in Example 1 is vulnerable to forgery and key recovery attacks.



## Key Management: Empty PBE Password

### Abstract
Generating and using a cryptographic key based on an empty password may compromise system security in a way that cannot be easily remedied.
### Explanation
It is never a good idea to pass an empty value as the password argument to a cryptographic password-based key derivation function. In this scenario, the resulting derived key will be based solely on the provided salt (rendering it significantly weaker), and fixing the problem is extremely difficult. After the offending code is in production, the empty password often cannot be changed without patching the software. If an account protected by a derived key based on an empty password is compromised, the owners of the system may be forced to choose between security and availability.

Example 1: The following code passes the empty string as the password argument to a cryptographic password-based key derivation function:

``
from hashlib import pbkdf2_hmac
dk = pbkdf2_hmac('sha256', '', salt, 100000)
``


Not only will anyone who has access to the code be able to determine that it generates one or more cryptographic keys based on an empty password argument, but anyone with even basic cracking techniques is much more likely to successfully gain access to any resources protected by the offending keys. If an attacker also has access to the salt value used to generate any of the keys based on an empty password, cracking those keys becomes trivial. After the program ships, there is likely no way to change the empty password unless the program is patched. An employee with access to this information can use it to break into the system. Even if attackers only had access to the application's executable, they could extract evidence of the use of an empty password.

## Key Management: Hardcoded Encryption Key
## Abstract
Hardcoded encryption keys could compromise system security in a way that cannot be easily remedied.
## Explanation
It is never a good idea to hardcode an encryption key. Not only does hardcoding an encryption key allow all of the project's developers to view the encryption key, it also makes fixing the problem extremely difficult. After the code is in production, a software patch is required to change the encryption key. If the account protected by the encryption key is compromised, the owners of the system must choose between security and availability.
Example: The following code uses a hardcoded encryption key to encrypt information:

``
from Crypto.Ciphers import AES
encryption_key = b'_hardcoded__key_'
cipher = AES.new(encryption_key, AES.MODE_CFB, iv)
msg = iv + cipher.encrypt(b'Attack at dawn')
``


This code will run successfully, but anyone who has access to it will have access to the encryption key. After the program ships, there is likely no way to change the hardcoded encryption key _hardcoded__key_ unless the program is patched. A devious employee with access to this information can use it to compromise data encrypted by the system.



## Key Management: Hardcoded HMAC Key

### Abstract
Hardcoded HMAC keys could compromise system security in a way that cannot be easily remedied.
### Explanation
It is never a good idea to hardcode an HMAC key. The cryptographic strength of HMAC depends on the confidentiality of the secret key, which is used for the calculation and verification of the message authentication values. Hardcoding an HMAC key allows anyone with access to the source to view it, and undermines the cryptographic strength of the function.

Example 1: The following code uses a hardcoded key to compute the HMAC:

``
import hmac
mac = hmac.new("secret", plaintext).hexdigest()
``


This code will run successfully, but anyone who has access to it will have access to the HMAC key. After the program ships, there is likely no way to change the hardcoded HMAC key "secret" unless the program is patched. A devious employee with access to this information could use it to compromise the HMAC function.





## Key Management: Hardcoded PBE Password

### Abstract
Using a key generated by a password-based key derivation function that was passed a hardcoded value for its password argument may compromise system security in a way that cannot be easily remedied.
### Explanation
It is never a good idea to pass a hardcoded value as the password argument to a cryptographic password-based key derivation function. In this scenario, the resulting derived key will be based mostly on the provided salt (rendering it significantly weaker), and fixing the problem is extremely difficult. After the offending code is in production, the hardcoded password often cannot be changed without patching the software. If an account protected by a derived key based on a hardcoded password is compromised, the owners of the system may be forced to choose between security and availability.

Example 1: The following code passes a hardcoded value as the password argument to a cryptographic password-based key derivation function:

``
from hashlib import pbkdf2_hmac
dk = pbkdf2_hmac('sha256', 'password', salt, 100000)
``


Not only will anyone who has access to the code be able to determine that it generates one or more cryptographic keys based on a hardcoded password argument, but anyone with even basic cracking techniques is much more likely to successfully gain access to any resources protected by the offending keys. If an attacker also has access to the salt value used to generate any of the keys based on a hardcoded password, cracking those keys becomes trivial. After the program ships, there is likely no way to change the hardcoded password unless the program is patched. An employee with access to this information can use it to break into the system. Even if attackers only had access to the application's executable, they could extract evidence of the use of a hardcoded password.



## Key Management: Null Encryption Key

### Abstract
Null encryption keys can compromise security in a way that cannot be easily remedied.
### Explanation
Assigning None to encryption key variables is a bad idea because it can allow attackers to expose sensitive and encrypted information. Not only does using a null encryption key significantly reduce the protection afforded by a good encryption algorithm, but it also makes fixing the problem extremely difficult. After the offending code is in production, a software patch is required to change the null encryption key. If an account protected by the null encryption key is compromised, the owners of the system must choose between security and availability.

Example: The following code initializes an encryption key variable to null.

``
from Crypto.Ciphers import AES
cipher = AES.new(None, AES.MODE_CFB, iv)
msg = iv + cipher.encrypt(b'Attack at dawn')
``


Anyone who has access to the code would be able to determine that it uses a null encryption key, and anyone employing even basic cracking techniques is much more likely to successfully decrypt any encrypted data. After the program ships, a software patch is required to change the null encryption key. An employee with access to this information can use it to break into the system. Even if attackers only had access to the application's executable, they could extract evidence of the use of a null encryption key.

# Python-Guidelines


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
...
mac = hmac.new("", plaintext).hexdigest()
...
``

The code in Example 1 may run successfully, but anyone who has access to it will be able to figure out that it uses an empty HMAC key. After the program ships, there is likely no way to change the empty HMAC key unless the program is patched. A devious employee with access to this information could use it to compromise the HMAC function. Also, the code in Example 1 is vulnerable to forgery and key recovery attacks.

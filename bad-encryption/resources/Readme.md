# Exploit Overview

This vulnerability arises from the improper handling of cookies and the use of an insecure hashing algorithm (MD5). The issue lies in the fact that sensitive operations, such as authentication, rely on the contents of a cookie named `I_am_admin`. The value of this cookie is hashed using MD5, which is a cryptographically weak algorithm. By manipulating this cookie, an attacker can gain unauthorized access to administrative privileges.

# How the Vulnerability Was Found

While inspecting the cookies stored in the browser, a field named `I_am_admin` was identified, containing an MD5 hash value. The hash `68934a3e9455fa72420237eb05902327` was decrypted using [CrackStation](https://crackstation.net/), revealing the value `false`. By deducing that this cookie determines administrative access, the value was modified. The string `true` was hashed using MD5 (`b326b5062b2f0e69046810717534cb09`) and replaced in the cookie. Upon reloading the website, administrative access was granted, and the flag `df2eb4ba34ed059a1e3e89ff4dfc13445f104a1a52295214def1c4fb1693a5c3` was revealed.

# Mitigation and Protection

To address this vulnerability and prevent similar exploits in the future:

1. **Avoid Trusting Cookies for Sensitive Operations**: Do not rely on client-side data, such as cookies, for critical authentication or authorization processes. Always validate such data on the server side.

2. **Use Secure Hashing Algorithms**: Replace MD5 with a more secure algorithm like bcrypt, Argon2, or PBKDF2. These algorithms are designed to resist brute-force attacks and provide better security.

3. **Implement Strong Authentication Mechanisms**: Use session tokens or server-side validation mechanisms to manage user authentication securely.

By following these best practices, the risk of similar vulnerabilities can be significantly reduced.

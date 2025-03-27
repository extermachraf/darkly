# README: Directory Traversal Vulnerability Exploit

## Overview

This document describes a directory traversal vulnerability. The vulnerability allows an attacker to access sensitive files on the server by manipulating the `page` parameter in the URL. This type of attack exploits improper input validation, enabling unauthorized access to files outside the intended directory.

## Exploit Details

The vulnerability was identified in the `GET` method of the web application. By navigating through the website, it was observed that the `page` parameter was used to load specific resources. Testing with values such as `/` and `../../` revealed that the application responded with humorous or trolling messages, indicating a lack of proper input sanitization.

Further testing with the following payload:

```
http://ip-server/?page=../../../../../../../../../../../etc/passwd
```

resulted in the successful retrieval of the `/etc/passwd` file, confirming the presence of a directory traversal vulnerability. The flag obtained from this exploit was:

```
b12c4b2cb8094750ae121a676269aa9e2872d07c06e429d25a63196ec1c8c1d0
```

## How the Vulnerability Was Found

1. Observed the `page` parameter in the URL during navigation.
2. Tested with simple traversal patterns like `/` and `../../`.
3. Incrementally increased the traversal depth to access sensitive files.
4. Successfully retrieved the `/etc/passwd` file using the crafted payload.

## Mitigation and Protection

To prevent directory traversal vulnerabilities, the following measures should be implemented:

1. **Input Validation**:

   - Validate and sanitize user inputs to ensure only expected values are accepted.
   - Use a whitelist approach to restrict allowed inputs.

2. **Path Normalization**:

   - Normalize file paths to prevent traversal sequences like `../` from being processed.

3. **Access Controls**:

   - Restrict access to sensitive files and directories using proper file permissions.
   - Ensure the web server runs with the least privileges required.

4. **Error Handling**:

   - Avoid exposing detailed error messages that could aid attackers in crafting exploits.

5. **Use Secure Libraries**:
   - Leverage secure frameworks and libraries that handle file paths safely.

By implementing these measures, the risk of directory traversal attacks can be significantly reduced.

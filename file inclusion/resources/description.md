# Open Redirect Vulnerability via URL Manipulation in Social Media Links

## Summary

An open redirect vulnerability was identified in the social media redirection links of the application. By manipulating the URL parameters, an attacker can redirect users to arbitrary malicious websites, potentially leading to phishing attacks or other security threats.

## Vulnerable Code:

```html
<ul class="icons">
  <li>
    <a
      href="index.php?page=redirect&amp;site=facebook"
      class="icon fa-facebook"
    ></a>
  </li>
  <li>
    <a
      href="index.php?page=redirect&amp;site=twitter"
      class="icon fa-twitter"
    ></a>
  </li>
  <li>
    <a
      href="index.php?page=redirect&amp;site=instagram"
      class="icon fa-instagram"
    ></a>
  </li>
</ul>
```

The URL structure suggests that the application uses query parameters like site to determine the destination for the user. However, the values of these parameters are not being properly sanitized or validated. This allows for exploitation by an attacker

you can manipulate the _site_ in the url for example

```url
index.php?page=redirect&site=http://malicious-website.com

```

##### This open redirect can be used to :

- Perform phishing attacks by directing users to malicious websites disguised as legitimate ones.
- Trick users into providing sensitive information.
- Launch social engineering attacks by redirecting users to pages that prompt them to download malicious software.
- Trigger Cross-Site Scripting (XSS) if the destination URL contains unsafe JavaScript code.

## Recommendations for Mitigation:

- Sanitize Input: Validate the site parameter against a whitelist of known social media URLs (e.g., facebook.com, twitter.com, instagram.com).
- Use Absolute URLs: Instead of dynamically generating redirection URLs using query parameters, hard-code the destination URLs for external sites.

[you can find more details about Unvalidated Redirects and Forwards Cheat Sheet in this link](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html)

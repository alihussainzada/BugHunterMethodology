# Laravel

## Methodology

- XSS or CRLF discovery on `*.domain.tld` to overwrite the CSRF token
- XSS can be handled easily, but it’s possible so test for XSS
- XSS can be occurred in `<a>` and `<iframe>` or `<form>` tags
- `.env` file store sensitive information, but it’s not in public directory (`../.env`)
- Look for IDOR and logic based vulnerabilities
- Laravel uses traditional web server, so fuzz for the files and directories
    - it differs from WordPress, it uses public folders as `document_root`
- GET Request to the `_ignition/heath-check` and search for `can_execute_commands`
- Look if debug mode is enabled or not, verb tamper on different pages
- Use `arrays` instead of `string`, it may result in information disclosure

```python
laravel.test/validateEmail?email[]=
```

- Run an automate scanner like burp Active Scan or Acunetix
- In Laravel ≤ 8.x the X-Forwarded-Host header is allowed an attacker to generate a malicious password-reset Email
# Django

Django is a python-based free and open-source wen framework that follows the model-template-views architectural pattern. it is maintained by the Django Software Foundation, an independent organization established in the US as a 501 non-profit.

## Methodology

- XSS or CRLF discovery on `*.domain.tld` to overwrite the `csrftoken`
- XSS can be handled easily, but it’s possible so test for XSS
- XSS can be occurred in `<a>` and `<form>` or `<iframe>` tags (when the input is reflected there)
- Look for `IDOR`, `SSTI` (old version) and logic based vulnerabilities
- Fuzz to discover endpoint not files or directories
    - If it uses a reverse proxy, there might be an additional path to pointing somewhere else
- Debug mode page discovery
    - Change the host header to something else
    - Sending Request to the 404 page and search for
    - Verb tampering on all pages
    - Send POST request to the `admin/login/?next=/admin/` and searching for 500 Status-Code
- Run an automate scanner like Burp Active Scanner or Acunetix
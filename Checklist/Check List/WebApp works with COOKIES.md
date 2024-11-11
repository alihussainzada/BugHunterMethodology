# WebApp works with COOKIES?

Try CSRF or CORS:

## CORS:

- always add `Origin: domain.tld` in every page

## CSRF:

- If cookie is SameSite, an XSS is needed on any subdomains
- if the cookie is LAX, still possible. However, the state-changing request should be done by GET method.
- if app works with cookie and JSON format more likely to be vulnerable
    - make the request simple (cuz if it is JSON a preflight is sent and not be allowed)

Here are 3 condition:

1. The Request is state-changing (something changes …)
2. The site works with Cookie (none and lax)
3. The request is SIMPLE
    1. HEAD, POST, GET
    2. URL-encoded, text-plain, multipart
    3. some basic headers
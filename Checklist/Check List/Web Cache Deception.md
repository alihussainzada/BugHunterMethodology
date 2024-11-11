# Web Cache Deception

Web Cache Deception arises when the cache server (which can either be a load balancer, revers proxy, and CDN) caches sensitive and private files

- If there is a web page that returns sensitive information (CSRF-TOKEN) try to test WCD

### Conditions:

1. Cache proxy should be configured to cache files based on the extension of the file (.css) and not on the content-type.
2. So, the response should have text/html `content-type`
3. Sensitive data should be cached, not being dynamic! Means the header must be `HIT`
4. It should not show 404 not found instead it must load the data
5. The response should not have `Cache-Control`, `no-cache`, `max-age`, `private` and `no-store`

### How to test:

1. Find an endpoint revealing sensitive info, find out that the web app uses any cache mechanism 
2. append or try “Test cases" , open the URL in a incognito tab or `CURL` command
- **Test Cases:**
    - [ ]  example.com/profile.php/nothing.css
    - [ ]  example.com/profile.php.css
    - [ ]  example.com/profile.php/../nothing.css
    - [ ]  example.com/profile.php/%2e%2e/test.js
    - [ ]  Use lesser known extensions such as .`avif` (Search on google, cloudflare has a good list)
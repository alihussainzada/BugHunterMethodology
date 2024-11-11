# Cross Site Request Forgery

## Methodology

The methodology is to find **state-changing requests**, then try to bypass the security manually

- Important rule: ALWAYS make an exploit code and run it to show the POC
- Fuzz to find hidden path and parameters, they mostly are not protected against CSRF
- Pay attention to the **SameSite** flag of the cookie (Lax or Strict)
    - If **SameSite** is not None, you need an XSS in any subdomains
    - If **SameSite** is **Lax**, you can still exploit the CSRF with a top level navigation exploit (GET only)
- **JSON request** with **cookies** are more likely vulnerable to CSRF, why?
    - The endpoints might accept other content types
    - JSON requests with token are safe
- Does mobile endpoints work with **Authentication Cookies?**
- CSRF Bypasses
    - Change the content type
    
    ```
    application/json -> application/x-www-form-urlencoded
    ```
    
    - Sometime be creative (do the following requests trigger the pre-flight?)
    
    ```
    application/json -> application/text/plain; application/json
    application/json -> application/x-www-form-urlencoded; application/json
    ```
    
    - Send empty value or remove the CSRF token
    
    ```
    data=value&CSRF_TOKEN=token -> data=value&CSRF_TOKEN=
    data=value&CSRF_TOKEN=token -> data=value
    ```
    
    - Change the token with a valid one (your token)
    
    ```
    data=value&CSRF_TOKEN=token -> data=value&CSRF_TOKEN=your_token
    ```
    
    - Verb tamper the request, works? try previous bypasses
    
    ```
    POST / HTTPS/1.1
    username=user&CSRF_TOKEN=value
    
    GET /?username=user&CSRF_TOKEN=value HTTP/1.1
    ```
    
    - Put the header’s CSRF token in body (not vice versa, why?), works? try previous bypasses
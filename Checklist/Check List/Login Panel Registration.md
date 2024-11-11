# Login Panel/Registration

## Login:

- [ ]  Blind XSS, in username and password
- [ ]  Check `.js` file on the page, such as `login.js`
- [ ]  Check the parameters used on the endpoint
    - Might be listed in the `source`
- [ ]  Checking the Mobile Endpoint
    - Does it have the same protection as webapp?
    - How does it treat Unicode characters?
- [ ]  Google Dorks, and try much more
    - `site:example.com inurl:register inurl:&`
    - `site:example.com inurl:signup inurl:&`
    - `site:example.com inurl:join inurl:&`
- [ ]  Brute Force UserName:Password (rate limit)
- [ ]  SQL injection e.g. `‘ or '1'=1#` or `‘ or ‘1’=’1—`
- [ ]  Hidden parameter discover
- [ ]  Directory fuzz

## Registration

- XSS (Blind)
    - for email: <svg/onload=alert(origin)>”@gmail.com
- Duplicate Registration
    - Try to generate using an existing username
        - ali@gmail.com ⇒ Ali@gmail.com `or` with the different password.
        - uppsecase
        - +1@
        - add special char `%00`, `%09` and `%20`
        - victim@attacker.com@gmail.com
        - victim@gmail.com@attacker.com
- check password length is limited or not
    - try to add limitless amount of characters lead to DDOS
- Email Takeover
    - add a new Email, before confirming, check if the new confirmation email is sent to the first registered email. If it send code to your number try it too, (old code new number)
- pre-account takeover
- email enumeration
    - Chech you can figure out registered users inside the app
- leaking PII information
    - Sign up an existing users, the errror may leak more info (PII)
- Path overwrite
    - name your username as `index.php` to occupy the app path
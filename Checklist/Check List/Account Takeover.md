# Account Takeover

Here we go again:

- [ ]  change Email send a confirmation link
- [ ]  Pre-account Takeover
- [ ]  Improper rate limiting
- [ ]  Open redirect

### How to test them:

- Change Email
    1. Change your email to you second email and send the confirmation link to victim
    2. victim clicks, and your email connects to victim’s account
- Open Redirect
    - If the app works with Oauth as well, this attack is possible. Just change the `redirect_uri` value to yours
-
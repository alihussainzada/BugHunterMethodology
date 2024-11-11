# MFA/2FA Bypasses

It is just another layer of security mechnism to verify usere identity, So when a Hacker has access to victim’s credintials he/she can not log in to victims account

## Methodology:

- [ ]  Resoponse Manipulation
- [ ]  2FA code leakage in response
- [ ]  2FA re-usability / from another account
- [ ]  Lack of brute force (no rate limiting)
- [ ]  Direct Request/Forceful browsing
- [ ]  CSRF & ClickJacking on 2FA disable Feature
- [ ]  Bypassing 2FA by sending blank code
- [ ]  Lack of rate limit re-sending the code via SMS
- [ ]  Previous sessions ended
- [ ]  Change the password, use the reset password.
- [ ]  copy paste cookie

## How to Test them:

- Resoponse Manipulation
    - Enter correct OTP, get the response of correct otp paste it when you entered the invalid respons
- 2FA code leakage in response
    - Request for 2FA and incept the request, Analyze the reponse and see if the code is leaked or not
- 2FA re-usability
    - Request a 2FA code and Use it, Now try to used it again, if it works consider it as a bug
    - Use the code, after a day or more
- Lack of brute force
    - Capture the request and send it to intruder, run the brute force attack
    
- Direct Request/Forceful browsing
    - Request Straight to the page which reaches after 2FA or any other authentication page
    - If there is no success, change the refer header to the 2FA page URL. This may fool application to pretend as if the request came after satisfying 2FA Condition
- CSRF & ClickJacking on 2FA disable Feature
    - Create 2 accounts, enable 2FA for one of them, capture the disable request run that on second request.
- Bypassing 2FA by sending blank code
    - Capture the asking OTP code request, remove the code or give it a null value and forward the request
- Lack of rate limit re-sending the code via SMS
    - You won't be able to bypass the 2FA but you will be able to waste the company's money.
- Previous sessions ended
    - When the 2FA is enabled, previous sessions created should be ended. This is because when a client has his account compromised he could want to protect it by activating the 2FA, but if the previous sessions aren't ended, this won't protect him.
- Change the password, use the reset password.
    - enable the 2FA, go to reset pass and request the reset pass and login you may bypass.
- copy paste cookie
    - authenticate yourself, if the 2FA is still poped up and you got cookie/token, copy the 2FA enabled account and paste it to another user.
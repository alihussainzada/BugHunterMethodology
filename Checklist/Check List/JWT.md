# JWT

- Application just decodes not verify, meaning change role to another user or admin
- Change the alg to none.
- the alg is HS256, and it means signature is symmetric try to bruteforce it
- 
- [ ]  Support for the none algorithm
- Try these
    
    ```
    none
    None
    NONE
    nOnE
    ```
    
- [ ]  Lack of valid signature
- Try this
    
    ```
    Change the signeture algorithm (e.g. HS256) and remove the signature section (the 3rd part)
    because the RS256 uses ASYMETRIC and SYMMETRIC, but HS256 uses JUST SYMMETRIC to verfify.
    but the RS public key might be availble publicky, So chagne to HS256 and use the public key of RS256 
    ```
    
- [ ]  Disclose of a correct signature
- Try this
    
    ```
    Try to change a payload and send such token to an API endpoint (remove the 3rd part of it)
    ```
    
- [ ]  Weak an HMAC secret key
- Try it
    
    ```
    
    ```
    
- [ ]  Brute force
- The Tools
    
    ```
    
    ```
    
- [ ]  Signature not been checked
- Try it out
    
    ```
    if the programmer forgets to check it, so you can remove it change it and so on.
    ```
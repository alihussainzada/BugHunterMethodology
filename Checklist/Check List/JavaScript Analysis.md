# JavaScript Analysis

I divided the process into 2 parts.

What do we look for?

- The links to increase the attack surface (hidden endpoints)
- Sensitive information (Password, API keys, Emails)
- Dangerous code (DOM, Eval ..)

## Manually Analysis

- We can use chrome browser in order to perform this task (tomnomnom method)
- Spider the app, add extract the sitemap from Burp Suite

## Automated Analysis

- Collect all js extension from wayback, katana, gospider (they may be dead, filter them alive)
- Run Secret Finder tool against all of them (the command is bellow)
- The SecretFinder command
    
    ```
    cat all-js-tosecret | while read url ; do python3 SecretFinder.py -i $url -o cli >> secret.txt; done
    # Run link finder against all url, not just js files
    ```
    
- Run LinkFinder to find Links (command is the same)
-
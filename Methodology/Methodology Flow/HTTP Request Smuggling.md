# HTTP Request Smuggling

Methodology

- Use HTTP Request smuggling in burp suite to discover vulnerability
- Use Smuggler to discover vulnerability
- Exploit The Flaw manually, Some techniques may be useful (Exploits)
    - Do application recon (Fuzz and etc) to discover a redirection path, try adding host header
    - Find redirection or any section that can save data, leak the information from front server
    - Check if the target uses cache implementation, try cache deception
    - Try to exploit in order to DDoS
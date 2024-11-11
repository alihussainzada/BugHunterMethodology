# Did you find an Origin IP? GREAT!

- Do Host Header Fuzzing
    - keep dead subs in order to fuzz
    - find origin IP, in Chat Box print your URL
    - trigger port scanning (nmap - Pn -F)
    - fuzz for -H (ffuf -w subs -u http://IP:Port/ -H “host: FUZZ” -fc 403 -c
    - if you find something(it responds), again fuzz for directory, if it does not respond to it in all IPs
    - send a curl request in order to find whether it responds or not
    - Use Boom word list
- Use your tools
    - Virtual-host-scanner from jobert abma
    - https://github.com/wdahlenburg/VhostFinder used
    
- Do nmap
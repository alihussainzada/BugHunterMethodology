# Email Spoofing on DOMAIN

## Email Spoofing

Attacker can send Email on behalf of Company when the bellow conditions meet:

1. Lack of an SPF or DMARK
2. SPF record never specifies -all or ~all
3. DMARK policy is set to p=none or is nonexistent 

### **For check:**

- Use the [https://github.com/BishopFox/spoofcheck](https://github.com/BishopFox/spoofcheck) to check SPF/ DMARK
- Or use, the site : [click](https://mxtoolbox.com) (DMARK lookup, SPF Record lookup)

### For exploit:

- For exploit navigate to this site : [click](http://emkei.cz)
- No SPF, and NO DMARC is found so vulnerable sometimes if there is DMARC is found but still vulnerable
- Install Hunter extension in order to find any email regarding to the sites or doing it on any domain :)
# WebApp Recon

In the recon process, we aim to map the application as most as possible. In order to achieve this, various techniques shroud be used:

- Google Dorks
- GitHub, Bit bucket and etc searches
- Determine the framework or CMS
- Virtual host discovery
- Using Archives (WayBackMachine, OTX, etc)
- Crawl web application
- Resource discovery
- Fuzzing on various properties
- Goals of this section
    1. To extract URLs and Js files
    2. To extract file names
    3. To extract Parameter
    4. To extract endpoints
    5. To discover hidden parameters, files and endpoints

## Google Dorks

To search in third parties

```bash
site:http://ideone.com | site:http://codebeautify.org | site:http://codeshare.io | site:http://codepen.io | site:http://repl.it | site:http:// | site:http://ideone.com | site:http://ideone.com | 
```

To search for indexes with `inurl`, `ext`, `link`, `site`, `intitel`

```bash
site:domain.tld inurl:&
site:domain.tld ext:(php|aspx|txt|jsp|html|xml|bak)
site:domain.tld inurl:(unsubscribe|register|feedback|signup|join|contact|user|profile|api|developer|affiliate|mobile|upload|pgrade|password) inurl:&
site:domain.tld ext:xml | ext:conf | ext:cnf | ext:reg | ext:inf | ext:rdp | ext:cfg | ext:ora | ext:ini
site:domain.tld ext:doc | ext:docx | ext:odt | ext:pdf | ext:rtf | ext:sxw | ext:psw | ext:ppt | ext:pptx | ext:pps | ext:csv 
site:domain.tld ext:sql | ext:dbf | ext:mdb | ext:log
site:domain.tld ext:bkf | ext:bkp | ext:bak | ext:old | ext:backup
site:domain.tld inurl:login | inurl:login | inurl:signin | intitle:Login | intitle:signin | inurl:auth 
site:domain.tld ext:action | ext:struts | ext:do
site:domain.tld filetype:wsdl | filetype:WSDL | exy:svc | inurl:wsdl | Filetype:?wsdl | intitle:_vti_bin/sites.asmx?wsdl | inurl:_vti_bin/sites.asmx?wsdl 
site:domain.tld filetype:config
site:*.domain.tld
site:*.*domain.tld
### Finding buckets of site:
site:.s3.amazonaws.com "domain.tld"
site:amazonaws.com "domain.com"
amazonaws s3 domain.com
amazonaws bucket domain.com
amazonaws domian.com
s3 domian.con

link:domain.tld
site:stackoverflow.com "domain.tld"
```

- I have collected these

```
site:*.target.* intext:@gmail.com -> useful from twitter
```

Use these tree sites:

[Google Dorks for Bug Bounty](https://taksec.github.io/google-dorks-bug-bounty/)

1. [https://pentest-tools.com/information-gathering/google-hacking](https://pentest-tools.com/information-gathering/google-hacking)
2. [https://dorksearch.com/](https://dorksearch.com/)
3. [https://dorkgenius.com/](https://dorkgenius.com/)

## Determine the framework or CMS

The wappalayzer is a good tool, the add-on or CLI

## Virtual host discovery

```bash
host: [FUZZ]
host: [FUZZ].domain.tld
host: [ALL_SUBDOMAIN]
```

## Extract

**some sites useful sites**

- [https://archieve.org](https://archieve.org) - a great source to travel in time
- [https://commoncrawl.org](https://commoncrawl.org) - great source of sites which have already crawled
- Hakrawler - a good crawler written in go
- GoSpider - a good crawler - supports many third parties (is recommended)
- GAU - a tool (passive, but supports actives mode)
- LinkFinder - a tool to discover endpoints and their parameters in JS files
- burpsuite
    
    Manually browsing the website, generate a site map
    
    Using spidering feature in the burp suite
    

The flow is like:

Find All Urls (gospider) ⇒ Find hidden links from js files (LinkFinder) ⇒ httpx

for Mass and Manual Test

## Fuzzing to discover

the aim to discover following properties

- File names
- parameters name
- endpoints

see the methodology!
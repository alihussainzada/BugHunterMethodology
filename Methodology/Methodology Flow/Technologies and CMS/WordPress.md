# WordPress

WordPress is a free and open-source content management system written in PHP and paired with a MySQL or MariaDB database. Features including a plugin architecture and template system, referred to within WordPress as Themes. 

## Methodology

- Recommend
    - Try to register with `@company.tld` email in `/wp-register.php`
    - Extract important files in WordPress (buckup fuzz)
    - File and directory files such as `.env`
    - Plugin and Theme enumeration → look for the vulnerabilities
    - Run an automate scanner like Burp Active Scan or Acunetix
- `license.txt` contains useful information such as the version WordPress installed.
- `wp-activate.php` is useful for the email activation process when setting up a new WordPress site.
- `xmlrpc.php` should be checked ( POST method )
- `wp-content/uploads` for directory listing and should be checked
- `wp-config.php` file contains top creds database stuff should be looked for backups

### Get WordPress Version

- meta tags name=”generator” ‘`content=WordPress’`

```bash
curl https://taget.com/ | grep 'content="WordPress'
```

- CSS link show the version and `js` files
- `wp-cron.php` for `DoS`
- `wp-json/oembed/1.0/proxy?url=COLOBURETOR` ( when 401 is found, it did not work )
- Yashar does not do (we can do)
    - WordPress user enumeration → Brute force
        - `/wp-json/wp/v2/users`
        - `/?author=1`
    - Brute force user accounts

### Fuzzing the plugins

Fuzzing plugins are helpful and they can help us to look for the found vulnerabilities in the plugins and also help us to manually work on the templates and search for the 0days

New plugins daily come to the WordPress websites and if we want to find the most plugins in target we should keep updating or wordlist.

To getting the latest version wordlist. Yashar made a script.

```python
from bs4 import BeautifulSoup
import urllib.request as hyperlink
import os

link = hyperlink.urlopen('http://plugins.svn.wordpress.org/')
wordPressSoup = BeautifulSoup(link,'lxml')
filePate = os.path.dirname(os.path.realpath(__file__))
fileNaming = (filePath + ('scrapedlist.txt'))
print('The current working directory of the files is ' + filePath + ' the scraped list has been saved to this directory as scrapedlist.txt')
with open('scrapedlist.txt','wt',encoding='utf8') as file:
	for link in wordPressSoup.find_all('a', href=True):
		lng = link.get('href')
		file.write(lnk.replace("/", "") + '\n')
		print(lnk.replace("/", "")
```

Fuzzing Themes

Like fuzzing plugins phase I wrote a script to get the latest themes slugs.

```python
from bs4 import BeautifulSoup
import urllib.request as hyperlink
import os

link = hyperlink.urlopen('http://themes.svn.wordpress.org/')
wordPressSoup = BeautifulSoup(link,'lxml')
filePate = os.path.dirname(os.path.realpath(__file__))
fileNaming = (filePath + ('scrapedlist.txt'))
print('The current working directory of the files is ' + filePath + ' the scraped list has been saved to this directory as scrapedlist.txt')
with open('scrapedlist.txt','wt',encoding='utf8') as file:
	for link in wordPressSoup.find_all('a', href=True):
		lng = link.get('href')
		file.write(lnk.replace("/", "") + '\n')
		print(lnk.replace("/", "")
```

## To fuzz:

```python
ffuf -w scraped -u http://url.tld/wp-content/plugins/FUZZ
```
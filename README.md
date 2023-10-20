# 35.181.1.193 -> vile.corp

## NMAP

### TCP

{% code overflow="wrap" %}
```bash
[Oct 13, 2023 - 09:35:49 (CEST)] exegol-CTF_PJ /workspace # nmap -sV 35.181.1.193 -sC -T4 -Pn -p-
Starting Nmap 7.93 ( https://nmap.org ) at 2023-10-13 09:35 CEST
Nmap scan report for ec2-35-181-1-193.eu-west-3.compute.amazonaws.com (35.181.1.193)
Host is up (0.13s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT      STATE SERVICE  VERSION
80/tcp    open  http     Apache httpd 2.4.56
|_http-server-header: Apache/2.4.56 (Debian)
|_http-title: Did not follow redirect to https://ec2-35-181-1-193.eu-west-3.compute.amazonaws.com/
443/tcp   open  ssl/http Apache httpd 2.4.56
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  http/1.1
| ssl-cert: Subject: commonName=frontoffice.vile.corp/organizationName=Vile/stateOrProvinceName=France/countryName=FR
| Not valid before: 2022-07-25T15:46:28
|_Not valid after:  2023-07-25T15:46:28
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  Basic realm=Restricted Content
|_http-server-header: Apache/2.4.56 (Debian)
|_http-title: 401 Unauthorized
50022/tcp open  ssh      OpenSSH 8.4p1 Debian 5+deb11u2 (protocol 2.0)
| ssh-hostkey: 
|   3072 8a093cf40bcf24877e426cd009c393c4 (RSA)
|   256 10858047d58a789f6a92b4e094625e49 (ECDSA)
|_  256 64a123e1e7f2809f94e245dd9b9602ba (ED25519)
Service Info: Hosts: localhost, 172.17.0.2; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 990.17 seconds
```
{% endcode %}

### UDP

{% code overflow="wrap" %}
```bash
/[Oct 13, 2023 - 09:53:25 (CEST)] exegol-CTF_PJ /workspace # nmap 35.181.1.193 -T4 -sU -Pn     
Starting Nmap 7.93 ( https://nmap.org ) at 2023-10-13 09:54 CEST
Nmap scan report for ec2-35-181-1-193.eu-west-3.compute.amazonaws.com (35.181.1.193)
Host is up.
All 1000 scanned ports on ec2-35-181-1-193.eu-west-3.compute.amazonaws.com (35.181.1.193) are in ignored states.
Not shown: 1000 open|filtered udp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 108.52 seconds
```
{% endcode %}

## PORT 80

Le port 80 redirige vers le port HTTPS 443

## PORT 443

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption><p>index of IP Address</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>Source Code</p></figcaption></figure>

We have the source code of the web page and we can see the link to the image referre to "frontoffice.vile.corp". We got ourself a host (vile.corp) and a vhost (frontoffice).

We add them in /etc/hosts

### Fuzzing

{% code overflow="wrap" %}
```bash
[Oct 13, 2023 - 10:18:48 (CEST)] exegol-CTF_PJ /workspace # gobuster dir -u https://vile.corp/ -k -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 20 -U tom.gendry -P Hu3-i3yief -r --timeout=20s -a "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36" 
===============================================================
Gobuster v3.5
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://vile.corp/
[+] Method:                  GET
[+] Threads:                 20
[+] Wordlist:                /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36
[+] Auth User:               tom.gendry
[+] Follow Redirect:         true
[+] Timeout:                 20s
===============================================================
2023/10/13 10:21:11 Starting gobuster in directory enumeration mode
===============================================================
/uploads              (Status: 200) [Size: 1685]
/javascript           (Status: 403) [Size: 275]
/server-status        (Status: 403) [Size: 275]
Progress: 220360 / 220561 (99.91%)
===============================================================
2023/10/13 10:30:26 Finished
===============================================================
```
{% endcode %}

{% code overflow="wrap" %}
```bash
[Oct 13, 2023 - 10:30:44 (CEST)] exegol-CTF_PJ /workspace # gobuster dir -u https://vile.corp/ -k -w /usr/share/wordlists/seclists/Discovery/Web-Content/big.txt -t 20 -U tom.gendry -P Hu3-i3yief -r --timeout=20s -a "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36" 
===============================================================
Gobuster v3.5
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://vile.corp/
[+] Method:                  GET
[+] Threads:                 20
[+] Wordlist:                /usr/share/wordlists/seclists/Discovery/Web-Content/big.txt
[+] Negative Status codes:   404
[+] User Agent:              Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36
[+] Auth User:               tom.gendry
[+] Follow Redirect:         true
[+] Timeout:                 20s
===============================================================
2023/10/13 10:31:00 Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 275]
/.htpasswd            (Status: 403) [Size: 275]
/_dev                 (Status: 200) [Size: 2701]
/javascript           (Status: 403) [Size: 275]
/server-status        (Status: 403) [Size: 275]
/uploads              (Status: 200) [Size: 1685]
Progress: 20476 / 20477 (100.00%)
===============================================================
2023/10/13 10:32:08 Finished
===============================================================
```
{% endcode %}

#### /uploads

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

**FLAG**

```
CogiTF{22f7376bdac07c4b1273ae98c604d8b9}
```

lm and cv folders are the same, they upload after filename obfuscation, the two possible upload file on the form on Frontoffice.vile.corp

Img folder is use to store image of frontoffice website

pdfs folder is use to store jobs pdfs&#x20;



### Nuclei

{% code overflow="wrap" %}
```bash
[Oct 13, 2023 - 17:49:24 (CEST)] exegol-CTF_PJ nuclei # ./nuclei -H "Authorization: Basic dG9tLmdlbmRyeTpIdTMtaTN5aWVmCg==" -u https://vile.corp

                     __     _
   ____  __  _______/ /__  (_)
  / __ \/ / / / ___/ / _ \/ /
 / / / / /_/ / /__/ /  __/ /
/_/ /_/\__,_/\___/_/\___/_/   v2.9.15

                projectdiscovery.io

[INF] Current nuclei version: v2.9.15 (latest)
[INF] Current nuclei-templates version: v9.6.5 (latest)
[INF] New templates added in latest release: 75
[INF] Templates loaded for current scan: 6967
[INF] Targets loaded for current scan: 1
[INF] Templates clustered: 1218 (Reduced 1156 Requests)
[api-intercom] [http] [info] https://api.intercom.io/users
[INF] Using Interactsh Server: oast.pro
[api-npm] [http] [info] https://registry.npmjs.org/-/whoami
[basic-auth-detect] [http] [info] https://vile.corp
[http-missing-security-headers:permissions-policy] [http] [info] https://vile.corp
[http-missing-security-headers:x-frame-options] [http] [info] https://vile.corp
[http-missing-security-headers:x-permitted-cross-domain-policies] [http] [info] https://vile.corp
[http-missing-security-headers:cross-origin-embedder-policy] [http] [info] https://vile.corp
[http-missing-security-headers:cross-origin-opener-policy] [http] [info] https://vile.corp
[http-missing-security-headers:cross-origin-resource-policy] [http] [info] https://vile.corp
[http-missing-security-headers:strict-transport-security] [http] [info] https://vile.corp
[http-missing-security-headers:content-security-policy] [http] [info] https://vile.corp
[http-missing-security-headers:x-content-type-options] [http] [info] https://vile.corp
[http-missing-security-headers:referrer-policy] [http] [info] https://vile.corp
[http-missing-security-headers:clear-site-data] [http] [info] https://vile.corp
[waf-detect:apachegeneric] [http] [info] https://vile.corp/
[ssl-issuer] [ssl] [info] vile.corp:443 [Vile]
[expired-ssl] [ssl] [low] vile.corp:443 [2023-07-25 15:46:28 +0000 UTC]
[mismatched-ssl-certificate] [ssl] [low] vile.corp:443 [CN: frontoffice.vile.corp]
[revoked-ssl-certificate] [ssl] [low] vile.corp:443
[self-signed-ssl] [ssl] [low] vile.corp:443
[deprecated-tls] [ssl] [info] vile.corp:443 [tls10]
[deprecated-tls] [ssl] [info] vile.corp:443 [tls11]
[tls-version] [ssl] [info] vile.corp:443 [tls10]
[weak-cipher-suites:tls-1.0] [ssl] [low] vile.corp:443 [[tls10 TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA]]
[tls-version] [ssl] [info] vile.corp:443 [tls11]
[weak-cipher-suites:tls-1.1] [ssl] [low] vile.corp:443 [[tls11 TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA]]
[tls-version] [ssl] [info] vile.corp:443 [tls12]
[tls-version] [ssl] [info] vile.corp:443 [tls13]
```
{% endcode %}

## VHOST

We know that frontoffice is a valid vhost for the vile.corp website, we look at its STATUS CODE which the curl command returns to us:

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

So we see that the return code is 421 and we can know enumerate the other vhost:

{% code overflow="wrap" %}
```bash
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -H "Host: FUZZ.vile.corp" -H "Authorization: Basic dG9tLmdlbmRyeTpIdTMtaTN5aWVmCg==" -u https://vile.corp -mc 421
```
{% endcode %}

We found the following vhost:

* backoffice
* frontoffice
* secret

In the secret VHOST, we can found the flag CogiTF{534da5310d1af4d817f25facb4a90002}

## WAF

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>


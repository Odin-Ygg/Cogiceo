# \_dev

It's seem to be the same as https://frontoffice.vile.corp but in an oldest version

## FUZZING

{% code overflow="wrap" %}
```bash
[Oct 13, 2023 - 11:04:47 (CEST)] exegol-CTF_PJ /workspace # feroxbuster -u https://vile.corp/_dev -H "Authorization: Basic dG9tLmdlbmRyeTpIdTMtaTN5aWVm" -x pdf,js,html,php,txt,json,docx -k


 ___  ___  __   __     __      __         __   ___
|__  |__  |__) |__) | /  `    /  \ \_/ | |  \ |__
|    |___ |  \ |  \ | \__,    \__/ / \ | |__/ |___
by Ben "epi" Risher 🤓                 ver: 2.9.3
───────────────────────────┬──────────────────────
 🎯  Target Url            │ https://vile.corp/_dev
 🚀  Threads               │ 50
 📖  Wordlist              │ /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
 👌  Status Codes          │ All Status Codes!
 💥  Timeout (secs)        │ 7
 🦡  User-Agent            │ feroxbuster/2.9.3
 🤯  Header                │ Authorization:  Basic dG9tLmdlbmRyeTpIdTMtaTN5aWVm
 🔎  Extract Links         │ true
 💲  Extensions            │ [pdf, js, html, php, txt, json, docx]
 🏁  HTTP methods          │ [GET]
 🔓  Insecure              │ true
 🔃  Recursion Depth       │ 4
 🎉  New Version Available │ https://github.com/epi052/feroxbuster/releases/latest
───────────────────────────┴──────────────────────
 🏁  Press [ENTER] to use the Scan Management Menu™
──────────────────────────────────────────────────
403      GET        9l       28w      275c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
404      GET        9l       31w      272c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
301      GET        9l       28w      307c https://vile.corp/_dev => https://vile.corp/_dev/
301      GET        9l       28w      314c https://vile.corp/_dev/static => https://vile.corp/_dev/static/
200      GET       70l      189w     3113c https://vile.corp/_dev/nous-rejoindre.html
200      GET       65l      122w     1235c https://vile.corp/_dev/static/css/index.css
200      GET       50l      222w     2701c https://vile.corp/_dev/index.html
200      GET      162l     1087w    77091c https://vile.corp/_dev/static/assets/images/hacker_hoodie.png
200      GET        2l     1294w    89501c https://vile.corp/_dev/static/js/jquery-3.6.0.min.js
200      GET       68l      116w     1392c https://vile.corp/_dev/static/css/base.css
200      GET      225l     1123w    88071c https://vile.corp/_dev/static/assets/images/vile.png
200      GET       94l      212w     3891c https://vile.corp/_dev/jobs.html
200      GET        5l       83w    59378c https://vile.corp/_dev/static/css/fontawesome.css
200      GET       76l      187w     3216c https://vile.corp/_dev/team.html
200      GET        7l     2211w   193529c https://vile.corp/_dev/static/css/bootstrap.min.css
200      GET       50l       91w      809c https://vile.corp/_dev/static/css/profile.css
200      GET       75l      250w     3583c https://vile.corp/_dev/profile.html
200      GET      192l     1426w    90265c https://vile.corp/_dev/static/js/jquery.dataTables.min.js
200      GET        1l      759w    18369c https://vile.corp/_dev/static/css/jquery.dataTables.min.css
200      GET        9l       19w      158c https://vile.corp/_dev/static/css/jobs.css
301      GET        9l       28w      318c https://vile.corp/_dev/static/css => https://vile.corp/_dev/static/css/
301      GET        9l       28w      317c https://vile.corp/_dev/static/js => https://vile.corp/_dev/static/js/
301      GET        9l       28w      321c https://vile.corp/_dev/static/assets => https://vile.corp/_dev/static/assets/
[####################] - 1m   1200304/1200304 0s      found:21      errors:148962 
[####################] - 1m    240000/240000  3936/s  https://vile.corp/_dev/ 
[####################] - 59s   240000/240000  4043/s  https://vile.corp/_dev/static/ 
[####################] - 56s   240000/240000  4271/s  https://vile.corp/_dev/static/js/ 
[####################] - 56s   240000/240000  4274/s  https://vile.corp/_dev/static/css/ 
[####################] - 54s   240000/240000  4417/s  https://vile.corp/_dev/static/assets/ 
```
{% endcode %}

{% code overflow="wrap" %}
```bash
[Oct 13, 2023 - 10:08:41 (CEST)] exegol-CTF_PJ vile.corp # gobuster dir -u https://vile.corp/_dev -k -t 20 -U tom.gendry -P Hu3-i3yief -r --timeout=20s -a "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36" -u https://vile.corp/_dev -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-files.txt 
===============================================================
Gobuster v3.5
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://vile.corp/_dev
[+] Method:                  GET
[+] Threads:                 20
[+] Wordlist:                /usr/share/wordlists/seclists/Discovery/Web-Content/raft-large-files.txt
[+] Negative Status codes:   404
[+] User Agent:              Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36
[+] Auth User:               tom.gendry
[+] Follow Redirect:         true
[+] Timeout:                 20s
===============================================================
2023/10/13 10:54:56 Starting gobuster in directory enumeration mode
===============================================================
/index.html           (Status: 200) [Size: 2701]
/.htaccess            (Status: 403) [Size: 275]
/.                    (Status: 200) [Size: 2701]
/.html                (Status: 403) [Size: 275]
/profile.html         (Status: 200) [Size: 3583]
/.php                 (Status: 403) [Size: 275]
/.htpasswd            (Status: 403) [Size: 275]
/jobs.html            (Status: 200) [Size: 3891]
/.htm                 (Status: 403) [Size: 275]
/.git                 (Status: 403) [Size: 275]
/.htpasswds           (Status: 403) [Size: 275]
/team.html            (Status: 200) [Size: 3216]
/.gitignore           (Status: 200) [Size: 3078]
/.htgroup             (Status: 403) [Size: 275]
/wp-forum.phps        (Status: 403) [Size: 275]
/.htaccess.bak        (Status: 403) [Size: 275]
/.htuser              (Status: 403) [Size: 275]
/.htc                 (Status: 403) [Size: 275]
/.ht                  (Status: 403) [Size: 275]
/.htaccess.old        (Status: 403) [Size: 275]
/.htacess             (Status: 403) [Size: 275]
Progress: 25247 / 37051 (68.14%)[ERROR] 2023/10/13 10:56:00 [!] parse "https://vile.corp/_dev/directory\t\te.g.": net/url: invalid control character in URL
Progress: 36894 / 37051 (99.58%)
===============================================================
2023/10/13 10:56:25 Finished
===============================================================
```
{% endcode %}

## Nuclei

{% code overflow="wrap" %}
```bash
[Oct 13, 2023 - 17:53:33 (CEST)] exegol-CTF_PJ nuclei # ./nuclei -H "Authorization: Basic dG9tLmdlbmRyeTpIdTMtaTN5aWVmCg==" -u https://vile.corp/_dev

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
[api-npm] [http] [info] https://registry.npmjs.org/-/whoami
[api-intercom] [http] [info] https://api.intercom.io/users
[INF] Using Interactsh Server: oast.me
[basic-auth-detect] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:referrer-policy] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:cross-origin-opener-policy] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:strict-transport-security] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:x-frame-options] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:x-permitted-cross-domain-policies] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:clear-site-data] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:cross-origin-embedder-policy] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:cross-origin-resource-policy] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:content-security-policy] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:permissions-policy] [http] [info] https://vile.corp/_dev
[http-missing-security-headers:x-content-type-options] [http] [info] https://vile.corp/_dev
[waf-detect:apachegeneric] [http] [info] https://vile.corp/_dev/
[ssl-issuer] [ssl] [info] vile.corp:443 [Vile]
[expired-ssl] [ssl] [low] vile.corp:443 [2023-07-25 15:46:28 +0000 UTC]
[mismatched-ssl-certificate] [ssl] [low] vile.corp:443 [CN: frontoffice.vile.corp]
[revoked-ssl-certificate] [ssl] [low] vile.corp:443
[self-signed-ssl] [ssl] [low] vile.corp:443
[deprecated-tls] [ssl] [info] vile.corp:443 [tls10]
[deprecated-tls] [ssl] [info] vile.corp:443 [tls11]
[tls-version] [ssl] [info] vile.corp:443 [tls10]
[tls-version] [ssl] [info] vile.corp:443 [tls11]
[tls-version] [ssl] [info] vile.corp:443 [tls12]
[tls-version] [ssl] [info] vile.corp:443 [tls13]
[weak-cipher-suites:tls-1.0] [ssl] [low] vile.corp:443 [[tls10 TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA]]
[weak-cipher-suites:tls-1.1] [ssl] [low] vile.corp:443 [[tls11 TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA]]
```
{% endcode %}

## .git

We fuzz the git directory

### FUZZING

First Step: Create a Wordlist for a .git repository

{% code overflow="wrap" %}
```bash
.git/
.git/HEAD
.git/config
.git/description
.git/info/
.git/info/exclude
.git/info/refs
.git/info/packed-refs
.git/objects/
.git/objects/info/
.git/objects/pack/
.git/refs/
.git/refs/heads/
.git/refs/tags/
.git/refs/remotes/
.git/logs/
.git/logs/HEAD
.git/logs/refs/
.git/logs/refs/heads/
.git/logs/refs/remotes/
.git/hooks/
.git/hooks/applypatch-msg.sample
.git/hooks/commit-msg.sample
.git/hooks/fsmonitor-watchman.sample
.git/hooks/post-update.sample
.git/hooks/pre-applypatch.sample
.git/hooks/pre-commit.sample
.git/hooks/pre-merge-commit.sample
.git/hooks/pre-push.sample
.git/hooks/pre-rebase.sample
.git/hooks/pre-receive.sample
.git/hooks/prepare-commit-msg.sample
.git/hooks/update.sample
.git/branches/
.git/index
.git/packed-refs
.git/COMMIT_EDITMSG
.git/FETCH_HEAD
.git/ORIG_HEAD
.git/MERGE_RR
.git/MERGE_HEAD
.git/MERGE_MODE
.git/CHERRY_PICK_HEAD
.git/rebase-apply/
.git/rebase-merge/
.git/rebase-apply/next
.git/rebase-apply/last
.git/rebase-apply/rebasing
.git/rebase-apply/patch
.git/rebase-apply/head-name
.git/rebase-apply/onto
.git/rebase-apply/orig-head
.git/rebase-apply/msg-clean
.git/rebase-apply/author-script
.git/rebase-apply/final-commit
.git/rebase-apply/msgnum
.git/rebase-apply/stopped-sha
.git/rebase-apply/quit
.git/rebase-apply/amend
.git/rebase-apply/patch-merge-index
.git/rebase-apply/apply-opt
.git/rebase-merge/
.git/rebase-merge/interactive
.git/rebase-merge/head-name
.git/rebase-merge/msgnum
.git/rebase-merge/end
.git/rebase-merge/msg-clean
.git/rebase-merge/onto
.git/rebase-merge/orig-head
.git/rebase-merge/done
.git/rebase-merge/git-rebase-todo.backup
.git/rebase-merge/git-rebase-todo
.git/rebase-merge/stopped-sha
.git/rebase-merge/quit
.git/rebase-merge/amend
.git/rebase-merge/patch-merge-index
.git/SQUASH_MSG
.git/BISECT_START
.git/BISECT_GOOD
.git/BISECT_BAD
.git/BISECT_LOG
.git/BISECT_EXPECTED_REV
.git/BISECT_ANCESTORS_OK
.git/BISECT_SKIP
.git/BISECT_PLAN
.git/BISECT_DONE
.git/BISECT_RUN
.git/MERGE_MSG
.git/sequencer/
.git/sequencer/todo
.git/sequencer/onto
.git/sequencer/head
.git/sequencer/abort-safety
.git/shallow
.git/unpacked-objects-timestamp
.git/gc.pid
.git/modules/
.git/worktrees/
.git/worktrees/HEAD
.git/worktrees/refs/
.git/worktrees/objects/
.git/worktrees/info/
.git/worktrees/logs/
.git/worktrees/logs/HEAD
.git/worktrees/logs/refs/
.git/worktrees/logs/refs/heads/
.git/worktrees/logs/refs/remotes/
.git/worktrees/hooks/
.git/worktrees/hooks/applypatch-msg.sample
.git/worktrees/hooks/commit-msg.sample
.git/worktrees/hooks/fsmonitor-watchman.sample
.git/worktrees/hooks/post-update.sample
.git/worktrees/hooks/pre-applypatch.sample
.git/worktrees/hooks/pre-commit.sample
.git/worktrees/hooks/pre-merge-commit.sample
.git/worktrees/hooks/pre-push.sample
.git/worktrees/hooks/pre-rebase.sample
.git/worktrees/hooks/pre-receive.sample
.git/worktrees/hooks/prepare-commit-msg.sample
.git/worktrees/hooks/update.sample
.git/annex/
.git/FETCH_HEAD~
.git/ORIG_HEAD~
.git/COMMIT_EDITMSG~
.git/COMMIT_EDITMSG.bak
.git/COMMIT_EDITMSG.tmp
.git/config~
.git/config.bak
.git/config.old
.git/config.tmp
.git/description~
.git/description.bak
.git/HEAD~
.git/HEAD.bak
.git/index~
.git/index.bak
.git/index.tmp
.git/packed-refs~
.git/packed-refs.bak
.git/packed-refs.old
.git/info/exclude~
.git/info/exclude.bak
.git/objects/info/packs~
.git/objects/info/packs.bak
.git/refs/original/
.git/refs/bisect/
.git/refs/wip/
.git/refs/notes/
.git/modules/info/
.git/modules/refs/
.git/modules/objects/
.git/MERGE_MSG.bak
.git/ORIG_HEAD.bak
.git/FETCH_HEAD.bak
.git/refs/wip/
.git/rebase-merge.orig/
.git/rebase-apply.orig/
.git/logs/refs/stash
.git/refs/stash

```
{% endcode %}

Step 2: Fuzzing

{% code overflow="wrap" %}
```bash
[Oct 13, 2023 - 19:23:40 (CEST)] exegol-CTF_PJ /workspace # gobuster dir -k -t 10 -U tom.gendry -P Hu3-i3yief -r --timeout=60s --delay=100ms -a "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36" -u https://vile.corp/_dev/ -w git.wl

===============================================================
Gobuster v3.5
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://vile.corp/_dev/
[+] Method:                  GET
[+] Threads:                 10
[+] Delay:                   100ms
[+] Wordlist:                git.wl
[+] Negative Status codes:   404
[+] User Agent:              Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.82 Safari/537.36
[+] Auth User:               tom.gendry
[+] Follow Redirect:         true
[+] Timeout:                 1m0s
===============================================================
2023/10/13 19:27:43 Starting gobuster in directory enumeration mode
===============================================================
/.git/info/           (Status: 403) [Size: 275]
/.git/HEAD            (Status: 200) [Size: 23]
/.git/objects/        (Status: 403) [Size: 275]
/.git/                (Status: 403) [Size: 275]
/.git/info/exclude    (Status: 200) [Size: 240]
/.git/config          (Status: 200) [Size: 226]
/.git/description     (Status: 200) [Size: 73]
/.git/refs/           (Status: 403) [Size: 275]
/.git/refs/heads/     (Status: 403) [Size: 275]
/.git/logs/HEAD       (Status: 200) [Size: 1400]
/.git/logs/refs/      (Status: 403) [Size: 275]
/.git/hooks/          (Status: 403) [Size: 275]
/.git/logs/refs/heads/ (Status: 403) [Size: 275]
/.git/logs/           (Status: 403) [Size: 275]
/.git/hooks/applypatch-msg.sample (Status: 200) [Size: 478]
/.git/hooks/commit-msg.sample (Status: 200) [Size: 896]
/.git/hooks/fsmonitor-watchman.sample (Status: 200) [Size: 3327]
/.git/hooks/post-update.sample (Status: 200) [Size: 189]
/.git/hooks/pre-applypatch.sample (Status: 200) [Size: 424]
/.git/hooks/pre-commit.sample (Status: 200) [Size: 1638]
/.git/hooks/pre-rebase.sample (Status: 200) [Size: 4898]
/.git/hooks/pre-receive.sample (Status: 200) [Size: 544]
/.git/hooks/pre-push.sample (Status: 200) [Size: 1348]
/.git/hooks/prepare-commit-msg.sample (Status: 200) [Size: 1492]
/.git/hooks/update.sample (Status: 200) [Size: 3610]
/.git/index           (Status: 200) [Size: 4271]
/.git/COMMIT_EDITMSG  (Status: 200) [Size: 89]
Progress: 159 / 160 (99.38%)
===============================================================
2023/10/13 19:27:45 Finished
===============================================================
[Oct 13, 2023 - 19:27:45 (CEST)] exegol-CTF_PJ /workspace # 

```
{% endcode %}

### DISCOVERY

In the URL [https://vile.corp/\_dev/.git/config](https://vile.corp/\_dev/.git/config), we found:

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

{% code overflow="wrap" %}
```bash
git -c http.sslVerify=false clone 'https://lucas.reeves%40vile.corp:Vilecorp123!@vile.corp/_dev/.git'
[Oct 13, 2023 - 11:37:33 (CEST)] exegol-CTF_PJ _dev # git -c http.sslVerify=false clone 'https://lucas.reeves%40vile.corp:Vilecorp123!@vile.corp/_dev/.git'

Cloning into '_dev'...
fatal: Authentication failed for 'https://vile.corp/_dev/.git/'
```
{% endcode %}

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

The credentials doesn't seem to be usable to connect to the git

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

#### .gitignore

{% code overflow="wrap" %}
```bash
# Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# PyInstaller
#  Usually these files are written by a python script from a template
#  before PyInstaller builds the exe, so as to inject date/other infos into it.
*.manifest
*.spec

# Installer logs
pip-log.txt
pip-delete-this-directory.txt

# Unit test / coverage reports
htmlcov/
.tox/
.nox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*.cover
*.py,cover
.hypothesis/
.pytest_cache/
cover/

# Translations
*.mo
*.pot

# Django stuff:
*.log
local_settings.py
db.sqlite3
db.sqlite3-journal

# Flask stuff:
instance/
.webassets-cache

# Scrapy stuff:
.scrapy

# Sphinx documentation
docs/_build/

# PyBuilder
.pybuilder/
target/

# Jupyter Notebook
.ipynb_checkpoints

# IPython
profile_default/
ipython_config.py

# pyenv
#   For a library or package, you might want to ignore these files since the code is
#   intended to run in multiple environments; otherwise, check them in:
# .python-version

# pipenv
#   According to pypa/pipenv#598, it is recommended to include Pipfile.lock in version control.
#   However, in case of collaboration, if having platform-specific dependencies or dependencies
#   having no cross-platform support, pipenv may install dependencies that don't work, or not
#   install all needed dependencies.
#Pipfile.lock

# poetry
#   Similar to Pipfile.lock, it is generally recommended to include poetry.lock in version control.
#   This is especially recommended for binary packages to ensure reproducibility, and is more
#   commonly ignored for libraries.
#   https://python-poetry.org/docs/basic-usage/#commit-your-poetrylock-file-to-version-control
#poetry.lock

# pdm
#   Similar to Pipfile.lock, it is generally recommended to include pdm.lock in version control.
#pdm.lock
#   pdm stores project-wide configurations in .pdm.toml, but it is recommended to not include it
#   in version control.
#   https://pdm.fming.dev/#use-with-ide
.pdm.toml

# PEP 582; used by e.g. github.com/David-OConnor/pyflow and github.com/pdm-project/pdm
__pypackages__/

# Celery stuff
celerybeat-schedule
celerybeat.pid

# SageMath parsed files
*.sage.py

# Environments
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# Spyder project settings
.spyderproject
.spyproject

# Rope project settings
.ropeproject

# mkdocs documentation
/site

# mypy
.mypy_cache/
.dmypy.json
dmypy.json

# Pyre type checker
.pyre/

# pytype static type analyzer
.pytype/

# Cython debug symbols
cython_debug/

# PyCharm
#  JetBrains specific template is maintained in a separate JetBrains.gitignore that can
#  be found at https://github.com/github/gitignore/blob/main/Global/JetBrains.gitignore
#  and can be added to the global gitignore or merged into this file.  For a more nuclear
#  option (not recommended) you can uncomment the following to ignore the entire idea folder.
#.idea/

```
{% endcode %}

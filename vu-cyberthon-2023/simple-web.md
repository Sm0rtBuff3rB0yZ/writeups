# Simple Web

## Challenge 

![alt text](images/simple-web.png?raw=true)

## Solution

We were given an html file `Task-www-index.html` that we can cat to obtain:
```
s4tb0y@s4tb0y ~/C/c/web-crypto> cat Task-www-index.html 
<html>
    <head>
        <meta http-equiv="refresh" WWW-Authenticate="--[----->+<]>---.-[--->+<]>+++.---[->+++<]>.+++.+++++++++++++.++.------------.+++++++.-." sop="WWW-Authenticate in esoteric programming language" content="1;url=https://www.cyberthon.lt/">
    </head>
    <body>
        <h1>Redirecting in 1 seconds...</h1>
    </body>
</html>⏎                  
```
We quickly find out its brainfuck language, we use an online tool to decode it and obtain the flag:

![alt text](images/web-simple2.png?raw=true)

`VU{cyberthon}`

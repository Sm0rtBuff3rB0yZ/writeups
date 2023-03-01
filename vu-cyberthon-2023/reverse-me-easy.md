# Reverse Me (easy)

## Challenge

Reverse the given binary to retrieve username and password in order to obtain the flag. `VU{username:password}`

## Solution

We were given a binary `Task-ReverseME`, we open it inside Ghidra and quickly find the value for username and password in main function:

![alt text](images/re-easy.png?raw=true)

We convert hex to dec and run the binary:
```
local_18 = 0x3f1; // -> 1009 (username) 
local_14 = 0x62b; // -> 1579 (password)
```
```
s4tb0y@s4tb0y ~/C/c/R/re_easy> ./Task-ReverseME
Enter login:1009
Enter password:1579

Congrats! The correct CTF answer is a password.
```

Thereore the flag is:

`VU{1009:1579}`

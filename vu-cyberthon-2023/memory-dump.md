# Memory Dump

## Challenge:

The challenge tells us that an user forgot his password and all we have is a memory dump, we need to find the forgotten password.

## Solution

We are given a zip file `Task-RAM.zip` containing the dump file `DESKTOP-URF93F5.raw`

We are going to use volatility3 for this task.

We first thought about dumping the hashes so we run the command below:
```
s4tb0y@s4tb0y ~/C/c/forensic> python3 volatility3/vol.py -f DESKTOP-URF93F5.raw hashdump

Volatility 3 Framework 2.4.1
Progress:  100.00		PDB scanning finished                        
User	rid	lmhash	nthash

Administrator	500	aad3b435b51404eeaad3b435b51404ee	31d6cfe0d16ae931b73c59d7e0c089c0
Guest	501	aad3b435b51404eeaad3b435b51404ee	31d6cfe0d16ae931b73c59d7e0c089c0
DefaultAccount	503	aad3b435b51404eeaad3b435b51404ee	31d6cfe0d16ae931b73c59d7e0c089c0
Admin	1001	aad3b435b51404eeaad3b435b51404ee	551d4771fff4866af49649dedad047f3
cloudbase-init	1002	aad3b435b51404eeaad3b435b51404ee	49ce64bf89ed6f0b6a985d313e914a36
no	1004	aad3b435b51404eeaad3b435b51404ee	c52295bb06a5d4de6c00c40abc898206
USER62B	1005	aad3b435b51404eeaad3b435b51404ee	fc525c9683e8fe067095ba2ddc971889
```

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
It's NTLM hashes, we can decode them with an online tool and retrieve:

![alt text](images/memory-dump.png?raw=true)

We try the decoded passwords but none of them work. <br>
Therefore we keep digging for hints about passwords on the memory dump.<br>
We start a filescan piped with a grep and discover a weird file named password.txt.
```
s4tb0y@s4tb0y ~/C/c/forensic> python3 volatility3/vol.py -f DESKTOP-URF93F5.raw windows.filescan | grep pass
0xe0014d2842c0.0\Windows\INF\umpass.PNF	216
0xe0014fe7d790	\Windows\SoftwareDistribution\Download\a57ac8f7c1a8e79edee4aa42282f94de\amd64_microsoft-windows-p..urepassword-library_31bf3856ad364e35_10.0.10240.17184_none_1903176943b783c4.manifest	216
0xe0015023aad0	\Users\Admin\AppData\Local\Packages\Microsoft.MicrosoftEdge_8wekyb3d8bbwe\AC\#!001\MicrosoftEdge\Cache\4FIHPBC1\password-cracking[1].jpg	216
0xe001507baf20	\Users\Admin\AppData\Roaming\Microsoft\Windows\Recent\password.lnk	216
0xe00150b14ca0	\Users\Admin\Desktop\password.txt	216
```
We extract it again with a volatility command:
```
s4tb0y@s4tb0y ~/C/c/forensic> python3 volatility3/vol.py -f DESKTOP-URF93F5.raw dumpfiles --virtaddr 0xe00150b14ca0
Volatility 3 Framework 2.4.1
Progress:  100.00		PDB scanning finished                        
Cache	FileObject	FileName	Result

DataSectionObject	0xe00150b14ca0	password.txt	file.0xe00150b14ca0.0xe0014eb53be0.DataSectionObject.password.txt.dat
```
We cat the downloaded file and obtain the flag:
```
s4tb0y@s4tb0y ~/C/c/forensic> cat file.0xe00150b14ca0.0xe0014eb53be0.DataSectionObject.password.txt.dat
VU2023CYBER⏎    
```
`VU{VU2023CYBER}`

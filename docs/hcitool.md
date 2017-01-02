Identified Onyx device using hcitool.


```
[jhe@oxcart raw]$ sudo hcitool lescan
LE Scan ...
1C:88:79:E0:04:26 Onyx-003W
1C:88:79:E0:04:26 Onyx-003W
^C
```

Inquired about Onyx using hcitool.

```
[jhe@oxcart raw]$ sudo hcitool leinfo 1C:88:79:E0:04:26
Requesting information ...
	Handle: 64 (0x0040)
	LMP Version: 4.0 (0x6) LMP Subversion: 0x2031
	Manufacturer: Cambridge Silicon Radio (10)
	Features: 0x01 0x00 0x00 0x00 0x00 0x00 0x00 0x00
```
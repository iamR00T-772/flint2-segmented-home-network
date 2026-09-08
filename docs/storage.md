# SMB / Samba Storage

A Silicon Power A62L 5 TB USB 3.0 external HDD is attached to the Flint 2.

The disk uses a single EXT4 filesystem partition and is exposed through authenticated SMB/Samba.

Security decisions include:
- anonymous access disabled
- Samba WAN access disabled
- SIEM network excluded
- access limited only to VLAN 10

A future media-server project was intentionally kept separate from the router to avoid unnecessary workload and complexity.

Note: The GL.iNET incorrectly displays the Silicon Power 5 TB drive as 36.39 TB. This drive is absolutely not as big as it is displayed, and this is confirmed on local devices that access it. Its true size, after formatting, is 4.96 TB.

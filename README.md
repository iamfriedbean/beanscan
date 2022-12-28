For binary releases, jump to https://github.com/iamfriedbean/beanscan/releases


# Beanscan External Attack Surface Scanner 

Traditional forms of security testing such as penetration testing are carried out in a very tight schedule usually in a pre-determined window often due to budget constraints. For this reason, scope of testing can be limited and does not scale widely to large digital footprint.  It is therefore crucial to have a tool that can discover and target large assets from day one – Beanscan does just that.​

Beanscan provides a discovery and audit workflow/automation using carefully selected open source community tools unified together for wide scale external surface attack scanning. It can be used to aid in the initial phases of external attack surface management or first step to a more in-depth or targeted penetration type testing and red team engagement

![image](https://user-images.githubusercontent.com/121557872/209822099-673ac0c6-2c19-4cbd-b335-ecf8d4cf8dc0.png)

## Sample Usage
`$beanscan -target example.com -discovery`  Run passive discovery only

`$beanscan -target example.com -discovery -asn 1234`  Run asset discovery with ASN 

`$beanscan -target example.com -webscan -nuclei -dirbrute -scantls` Run web and vulnerability scan against target. Brute force directories and also check TLS.

`$beanscan -target example.com -webscan -cloud -nuclei -portscan` Run web and vulnerability scan against target. Also run cloud checks, network mapping and security audit.

`$beanscan -target example.com -surface-attack` Run passive discovery including all tests. 

`$beanscan -show-db -target example.com` Show previously collected domain records from beanscan sink database


## System/Platform Requirements

Ubuntu Linux 20.04 LTS and above


## Credits

Would like to thank developers and contributors from Open Source community including but not limited to:
ProjectDiscovery.io, Tom Hudson, Luke Stephens, Jason Haddix, James Kettle, OWASP.org and many more.  

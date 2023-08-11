For latest release, jump to https://github.com/iamfriedbean/beanscan/releases


# Beanscan External Attack Surface Scanner 

Traditional forms of security testing such as penetration testing are carried out in a very tight schedule usually in a pre-determined window often due to budget constraints. For this reason, scope of testing can be limited and does not scale widely to an external large digital footprint.  It is therefore crucial to have a tool that can discover and test large assets from day one – Beanscan does just that.​

Beanscan provides a discovery and audit workflow/automation using combination of own written tools and carefully selected open source community tools unified together for wide scale external surface attack scanning. It can be used on its own or to aid in the initial phases of external attack surface management; or first step to a more in-depth or targeted penetration type testing and red team engagement

## How to install 

Go to the latest release section and download the installation/setup file - "setup-beanscan"


1. Download the setup file
```
https://github.com/iamfriedbean/beanscan/releases
```
2. Set executable file permission

 ```
 $chmod u+x setup-beanscan
```

3. Run the setup file

```
$ ./setup-beanscan
```

4. Follow the instruction
5. Once installed, just run the app (you may need to close and re-open your console terminal to apply environment configuration)     

```
$beanscan -h
```

*****
### Updating
To fetch the latest update, just run:
```
$update-beanscan
```   

*****

## System/Platform Requirements

- Ubuntu Linux 20.04 LTS and above.
- BASH required
- Internet Connection
- SUDO rights (required for Ubuntu package update and headless crawling)
  


## Sample Usage
Run passive discovery only
```
$beanscan -target example.com -discovery
```

Run asset discovery with ASN 
```
$beanscan -target example.com -discovery -asn 1234
```

Run web and vulnerability scan against target. Brute force directories and also check TLS.
```
$beanscan -target example.com -webscan -cve -dirbrute -scantls
```

Run web and vulnerability scan against target. Also run cloud checks, network mapping and security audit.
```
$beanscan -target example.com -webscan -cloud -cve -portscan
```

Run web and vulnerability scan against target. Also run cloud checks, network mapping and security audit, TLS scans, no headless crawling and WAF friendly mode.   
      
By default, beanscan uses several WAF bypassing techniques. The WAF friendly mode is an additional option to try and avoid getting blocked by sophisticated WAF.
Note that this can take a long time to complete.

```
$beanscan -target example.com -webscan -cloud -cve -portscan -scantls -no-headless -waf-friendly
```

Use of TOR network for evasion

```
$beanscan -target example.com -webscan -cloud -cve -portscan -scantls -use-tor
```



Show previously collected domain records from beanscan sink database
```
$beanscan -show-db -target example.com
```
Scans multiple or list of domains
```
$cat domains.txt | xargs -I {} beanscan --target {} -webscan -cve -portscan -dirbrute -scantls
```

Refer to the help section for other command options and features: 

```
/ /__  ___  ____   ____ ____ ____ ____   ____  
 / / _ \/ _ \/ _  \ / __ \ __// __// _  \ / __ \ 
/ /__/ /  __/ (_) |/ / / /_\ / /__/ (_) |/ / / / 
_/____/\___/\___/_/_/ /_/___/\___/\___/_/_/ /_/ C.E. v1.04
Spill the beans || @iamfriedbean || Community Edition
=====================================================

Powered by open source. Beanscan is an attack surface discovery and vulnerability scanner focusing
on web application.

Usage:
   beanscan [options]
   beanscan -target [string] [options]

ASSET(s) DISCOVERY:                                                             
   -discovery   Asset discovery only. Other options not listed here will be ignored.            
      Optional:                                                                 
         -dnsbrute          Subdomain bruteforcing using built-in wordlist.             
         -asn [number]      Include Autonomous System Number (ASN) in asset discovery.
         -webshot           Enable Web Screenshot Utility.             

WEB VULNERABILITY SCANNING:                                                     
   -webscan   Dynamic Application Security testing - DAST for Web (Black Box). Includes TECH detection, WAF, CORS,OAST & other OWASP Top-10 related tests.
      Optional:                                                                 
         -no-headless       Do not use headless crawling. 
            
   -cors      Cross Origin Resource Sharing misconfiguration. Already included as part of -webscan.
   -desync    HTTP request smuggling/desync attacks. Already included as part of -webscan.
   -dfxss     In depth cross site scripting and parameter analysis. Already included as part of -webscan.
   -nosqli    Scans for injection in NOSQL databases such as MongoDB. Already included as part of -webscan.
   -oastcrazy Sends callback to out-of-bound security test (OAST) server. Already included as part of -webscan.

   -dirbrute  Generates custom wordlist and perform directory bruteforce recursively.
                            
MISCELLANEOUS:                                                     
   -webshot   Enable Web Screenshot Utility.          
   -cloud     Cloud enumeration for AWS, GCP and Azure.
   -portscan  Network discovery and security auditing. (top 1K tcp/udp ports).
   -cve       Vulnerability scanner for CVEs, misconfigurations and exposures.
   -scantls   Server's SSL/TLS configuration and implementation.
   -waf-friendly  Useful for sites behind a WAF/CDN. This is very slow and will severely increase the scan-time.
                  Other scans such as DAST is not supported.(experimental)

DATABASE SINK:
   -sink-db   Use previously collected domain records from beanscan sink database rather than running asset discovery.
   -show-db   Show previously collected domain records from beanscan sink database. Other options will be ignored.

INTEGRATIONS:
   -bit-asm   Fetch domains from Tenable-Bitdiscovery ASM and update sink database. Other options will be ignored.

ANONYMITY/EVASION:
   -use-tor   Use of the Onion Router(tor) network (experimental).

HOUSEKEEPING:
   -keep-tmplogs   Keep all temporary files and logs.

USAGE EXAMPLES:                                                     
   beanscan -target example.com -discovery
      Run passive discovery only
   beanscan -target example.com -discovery -asn 1234
      Run asset discovery with ASN 
   beanscan -target example.com -webscan -cve -dirbrute -scantls
      Run web and vulnerability scan against target. Brute force directories and also check TLS.
   beanscan -target example.com -webscan -cloud -cve -portscan
      Run web and vulnerability scan against target. Also run cloud checks, network mapping and security audit.
   beanscan -show-db -target example.com
      Show previously collected domain records from beanscan sink database
```


### Additional configuration
**Optional**  

The configuration file can be found at ~/.config/beanscan/config.env   
Here, you can configure optional headers, OOB server and API keys:

```
make sure the to follow the format. Should be enclosed with : "\"CustomHeader\""
WEB_HEADER = "\"X-This is Beanscan\""


# set your oast server here
OOB_SERVER = xxxxxxxxxxxxx.oastify.com

# Bitdiscovery ASM API key
BITKEY = bitdiscovery API key

# Open AI
GPT_KEY = "Open AI GPT API Key"
```


*****

**OastCrazy**  
The -oastcrazy option requires OOB (call back) server to work. You can use BURP Collaborator or Interactsh client.
Copy the payload link and add it to your configuration


`$interactsh-client`   

`[WRN] Use with caution. You are responsible for your actions`  
`[WRN] Developers assume no liability and are not responsible for any misuse or damage.`  
`[INF] Listing 1 payload for OOB Testing`  
`[INF] cenhe2s2jh0dorbpeiugq4ktqrhbhsrgx.oast.fun`  


Edit the beanscan configuration file: ~/.config/beanscan/config.env  
Update the OOB_SERVER entry:  

`# set your oast server here`  
`OOB_SERVER = cenhe2s2jh0dorbpeiugq4ktqrhbhsrgx.oast.fun`

## Open AI GPT
Beanscan can make use of Open AI GPT (tested using GPT-3.5) to evaluate risk and impact of found vulnerabilities.

## Results/Reports

Beanscan creates directories (from current directory) based on the target seed domain. This is where it stores the results.  So assumed you used `-target example.com` from your home directory , it will create the following:   

`$ example.com/results-summary.html`  file which contains summary of results    
`$ example.com/logs/`  directory which contains log files    
`$ example.com/logs/html`  directory which contains HTML reports (where applicable)       



## Credits

Would like to thank the Open Source community for non stop research and continuously developing great tools. Special thanks to
ProjectDiscovery.io, @tomnomnom, @hakluke, @jhaddix, Portswigger, Pentesterlab, Intigriti, Sensepost, OWASP.org, SANS.org, AssetNote, Seclist and many more.  

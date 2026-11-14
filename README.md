# networkwalks-B084-week2-kalilinux-tools-GHDB-Maltego-theHarvest-zenmap-final-report
This report consolidates the practical activities evidenced in the supplied README-style screenshots. The work covers four related areas: web and DNS reconnaissance using Kali Linux tools; awareness of the Exploit Database Google Hacking Database (GHDB) and search-engine exposure; a Maltego domain-investigation workflow; and network discovery and port scanning using Nmap/Zenmap. The report follows the organization of the supplied sample report and records the observed outputs without treating reconnaissance leads as confirmed vulnerabilities.

The screenshots identify networkwalks.com as the domain used in the footprinting and Maltego examples. The Nmap screenshot separately shows a localhost scan and a network scan target field. The observed host addresses are reproduced exactly as displayed; the subnet/host-list discrepancy is called out for verification.

• Collect publicly available domain, DNS and web-technology information.
• Understand how indexed pages and exposed-device references may appear in GHDB-related research.
• Use Maltego to create a domain entity and review the output of an email-address transform.
• Use Nmap/Zenmap to identify live hosts and observe TCP port states.
• Document evidence, potential risks, limitations and practical security recommendations.
Tools and Technologies Used
Tool / Technology

Purpose

Kali Linux

Environment used for reconnaissance commands.

WhatWeb

Identifies technologies exposed by a website.

WHOIS

Retrieves public domain-registration and name-server information.

nslookup

Queries DNS and resolves a domain to an IP address.

curl -I

Requests HTTP response headers.

wafw00f

Checks for indicators of a Web Application Firewall.

DNSRecon

Performs DNS reconnaissance and attempts record enumeration.

Exploit Database / GHDB

Reference for search patterns that may reveal publicly indexed pages.

Maltego Desktop 4.14.0

Graph-based domain investigation and transform workflow.

Nmap / Zenmap

Network discovery, port scanning and topology visualization.

macOS

Operating system shown in the Nmap installation README.

 Web and DNS Footprinting
The supplied Network Reconnaissance README documents six Kali Linux commands against networkwalks.com:

Tool

Command shown

Purpose

WhatWeb

whatweb https://networkwalks.com

Fingerprint website technologies and server-side components.

WHOIS

whois networkwalks.com

Review public registration and name-server information.

DNS lookup

nslookup networkwalks.com 8.8.8.8

Resolve the domain using Google DNS.

HTTP headers

curl -I https://networkwalks.com

Inspect the HTTP response status and headers.

WAF check

wafw00f https://networkwalks.com

Check for a detected Web Application Firewall.

DNSRecon

dnsrecon -d networkwalks.com

Attempt DNS record enumeration.

Observed notes from the screenshot: networkwalks.com resolved to 192.232.216.135 when queried through 8.8.8.8; WHOIS returned domain-registration and name-server information; WhatWeb and the HTTP-header request returned web-server/technology and response metadata; the WAF check reported ModSecurity (SpiderLabs); and DNSRecon output included timeout/lifetime-related errors, meaning the captured enumeration was not fully successful.
GHDB and Public-Exposure Awareness
The GHDB screenshots show the Exploit Database site and a GHDB listing of search patterns, followed by a search-results example associated with webcamXP and browser views of webcamXP and a Mobotix camera interface. These screenshots demonstrate that device-related pages or interfaces may be indexed or discoverable through search engines. They do not establish device ownership, authorization, whether a feed is intentionally public, or whether a vulnerability exists. No attempt to log in, control, record or redistribute camera content is represented as part of this report.
Maltego Domain Investigation
1. Installed and launched Maltego Desktop version 4.14.0, as shown in the supplied guide.
2. Signed in to a Maltego account; personal login details are intentionally not reproduced.
3. Created a new graph and added a Domain entity for networkwalks.com.
4. Reviewed or edited the Domain entity details before running a transform.
5. Selected the “Email addresses from Domain” transform workflow.
6. Reviewed the transform output; the screenshot shows info@networkwalks.com as an example result.
Transform results are leads that may depend on the account, data sources, availability and credits. The example email address should be independently verified before use and should not be treated as proof of a current, active or authorized contact.
Nmap / Zenmap Network Scanning
The supplied Nmap README describes installation on macOS using the nmap-7.993.dmg installer and nmap-7.993.mpkg package, followed by launching Nmap/Zenmap from Applications. The screenshots document two quick-scan examples:

Scan

Target

Command

Localhost quick scan

127.0.0.1

nmap -T4 -F 127.0.0.1

Network quick scan

192.168.1.0/24

nmap -T4 -F 192.168.1.0/24

The localhost scan table shows the following TCP port observations:

Port

Protocol

State

Service

5000

tcp

open

upnp

49154

tcp

filtered

unknown

49155

tcp

filtered

unknown

49156

tcp

open

unknown

49157

tcp

open

unknown

The visible network host list is 10.21.65.144, 10.21.65.160, 10.21.65.247 and localhost. The host-details panel for 10.21.65.144 reports host state up, 1 open port, 2 filtered ports, 97 closed ports and 100 TCP ports scanned.

Important evidence note: the Nmap screenshot target field displays 192.168.1.0/24, while the visible discovered host list uses 10.21.65.x addresses. These are reproduced as shown and are not reconciled here. Verify the actual network interface, subnet and scan target before repeating the scan or submitting this as a single-subnet result.

 Risk Analysis / Impact
Finding

Evidence

Potential impact

Indicative level

Technology/version information visible

WhatWeb and HTTP headers returned technology and response metadata.

May help an external party fingerprint the web stack and select further research paths.

Low–Medium

Public DNS and registration data

WHOIS and nslookup returned registration/name-server information and an IP address.

Can contribute to infrastructure profiling; public DNS data is not itself a vulnerability.

Low

WAF identification

wafw00f reported ModSecurity (SpiderLabs).

Reveals a defensive technology detail; does not prove the WAF is effective or ineffective.

Low

Incomplete DNS enumeration

DNSRecon reported timeout/lifetime-related errors.

Incomplete visibility may leave records unreviewed; repeat only within authorized scope and with suitable connectivity.

Informational

Search-indexed camera-related pages

GHDB/search screenshots show webcamXP/Mobotix-related pages or interfaces.

Potential privacy and exposure concern if a device is unintentionally accessible; screenshots do not prove unauthorized access or a vulnerability.

Medium (requires validation)

Email address discovered by transform

Maltego output shows info@networkwalks.com as an example.

May enable unwanted contact or phishing if misused; verify relevance and handle responsibly.

Low

Live hosts and open/filtered ports

Nmap shows multiple host addresses and port states.

Unexpected devices or exposed services may increase attack surface; ownership and business need must be confirmed.

Medium (requires validation)

Risk levels are preliminary observations based only on the supplied screenshots. They are not confirmed vulnerabilities or a formal severity assessment. No exploitation, authentication attempts, access-control testing or vulnerability validation is evidenced in the supplied materials.

Recommendations
7. Review publicly exposed web-technology and HTTP-header information; disclose only what is operationally necessary.
8. Keep the CMS, plugins, web server and supporting software updated, and review relevant security advisories.
9. Review DNS records and domain-registration information periodically; remove obsolete records and restrict unnecessary service exposure.
10. Keep the WAF maintained, monitored and correctly configured; validate its effectiveness through authorized testing.
11. Investigate camera interfaces and device pages identified in public search results. Confirm ownership, remove unintended public access, require strong authentication and avoid exposing administrative interfaces to the internet.
12. Treat Maltego-discovered email addresses as unverified leads; validate them through approved organizational channels and do not use them for unsolicited or deceptive activity.
13. Maintain an inventory of authorized network assets and approved subnets; investigate unknown hosts and unexpected open ports.
14. Verify the Nmap target subnet against the active network configuration before scanning and document the exact scope, date and scan options.
15. Repeat DNS enumeration only where authorized and investigate timeout causes without increasing scan intensity unnecessarily.
16. Retain only the minimum evidence required, redact credentials and personal information, and share findings privately with the system owner.

The practical work demonstrates a reconnaissance-to-discovery workflow. Kali Linux tools were used to collect web, DNS, registration and WAF-related information for networkwalks.com. GHDB research illustrated how search-engine indexing can surface references to device interfaces, while the Maltego workflow showed how a domain entity and transform can produce additional investigation leads. Nmap/Zenmap provided examples of localhost port states and network host discovery. The exercises reinforce that reconnaissance results must be interpreted carefully: indexed pages, technology fingerprints, email results and open ports are not automatically vulnerabilities. Any further validation must remain within written authorization and a clearly defined scope.

Evidence Appendix
Evidence 1 — Network reconnaissance README: WhatWeb, WHOIS, DNS lookup, HTTP headers, WAF check and DNSRecon observations.





Evidence 2 — GHDB research and camera-interface exposure awareness: Exploit Database/GHDB listing, search-result example and browser interface screenshots. Sensitive imagery/details should remain redacted.





Evidence 3 — Maltego quick-start workflow: installation, sign-in screen (credentials concealed), domain graph, transform selection and example output.





Evidence 4 — Nmap and Zenmap: macOS installation steps, localhost and network scan examples, port-state table, host list and host details.


# Future Interns | Cyber Security Task 1

## Vulnerability Assessment Report for a Live Website (Read-Only Scope)

**Candidate:** QUSAY ALHEMIRY  
**Internship:** Future Interns - Cyber Security (November 2026)  
**Assessment date:** 03 November 2026  
**Target:** [Altoro Mutual demonstration application](https://demo.testfire.net/?mode=demo) (`demo.testfire.net`)  
**Deliverable:** [6-page Vulnerability Assessment Report](Vulnerability_Assessment_Report.pdf)

## Project overview
A limited, educational vulnerability assessment of a public demonstration web application. The purpose is to identify common configuration weaknesses, assess potential business impact, and recommend practical remediation measures. This is **not** a commissioned penetration test, an assertion of successful exploitation, or a full security certification.

## Website and scope
- Public pages inspected: the landing page and About Us (`/index.jsp?content=inside_about.htm`).
- Allowed web analysis: manual browsing, HTTP response-header review, browser cookie flags, and passive OWASP ZAP alert review.
- Excluded: authentication bypass, exploit attempts, brute force, active ZAP attacks, DoS, and testing of private or authenticated functions.
- Separate network exposure check: a limited **active TCP connect** test for ports 80 and 443 only. It is **not** a passive scan and was not used to claim any exploitable vulnerability.

## Tools
| Tool | Use |
| --- | --- |
| Chrome DevTools | Response headers and session cookie attributes |
| OWASP ZAP 2.17.0 | Safe Mode, Manual Explore, passive alerts |
| Nmap 7.993 / Zenmap | Limited TCP port status check (`nmap -sT -p 80,443 demo.testfire.net`) |
| Canva | Professional report design and export to PDF |

## Summary of observations
| ID | Observation | Risk label | Evidence |
| --- | --- | --- | --- |
| F-01 | Missing Content Security Policy | Medium (ZAP) | E02, E03, E04 |
| F-02 | Missing anti-clickjacking protection | Medium (ZAP) | E02, E03, E05 |
| F-03 | Server banner exposes implementation information | Low (ZAP) | E03, E06 |
| F-04 | Missing Strict-Transport-Security header | Low (ZAP) | E02, E03, E07 |

Supporting observations: `JSESSIONID` had `HttpOnly` and `Secure` set; explicit `SameSite` was not shown. A ZAP cache-control advisory was informational. A limited port check showed `80/tcp` and `443/tcp` as open. None of those observations alone establishes compromise or an exploitable weakness.

## Repository contents
```text
FUTURE_CS_01/
├── README.md
├── Vulnerability_Assessment_Report.pdf
└── Evidence/
    ├── E01_Altoro_Demo_Homepage.png
    ├── E02_Chrome_Response_Headers_About.png
    ├── E03_ZAP_Raw_HTTP_Response.png
    ├── E04_ZAP_CSP_Alert.png
    ├── E05_ZAP_Anti_Clickjacking_Alert.png
    ├── E06_ZAP_Server_Information_Disclosure.png
    ├── E07_ZAP_HSTS_Header_Alert.png
    ├── E08_ZAP_Cache_Control_Informational.png
    ├── E09_Nmap_80_443_Results.png
    └── E10_Cookie_Flags_Redacted.png
```

## Evidence-handling notes
Screenshots are drawn from the assessment session. Some screenshots are cropped for legibility. The session-cookie value has been permanently redacted from the evidence image. Avoid uploading raw tokens, passwords, secrets or private data to a public repository.

## Important limitations
- Only a small selection of public HTTP responses was reviewed.
- ZAP risk/confidence labels describe tool findings, not confirmed exploitability.
- Port 80/443 exposure alone is normal for many web servers and is not a vulnerability by itself.
- This is a training exercise on an HCL-hosted demonstration application, not an official audit commissioned by HCL.

## References
- [Future Interns Task 1](https://futureinterns.com/cyber-security-task-1-2026/)
- [OWASP ZAP](https://www.zaproxy.org/)
- [Nmap](https://nmap.org/)

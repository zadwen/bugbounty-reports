# Vulnerability Report: Publicly Exposed Sensitive Directories & Backups

## Executive Summary
During an independent security assessment, a critical information disclosure vulnerability was identified on a Vodafone endpoint. Due to a server misconfiguration, sensitive directories containing database dumps, command histories, and backend source files were publicly accessible without authentication. 

* **Target URL:** `https://vfo11.vodafone.om`
* **Vulnerability Type:** Information Exposure Through Sent Data (CWE-200) / Server Misconfiguration
* **Platform:** HackerOne
* **Status:** Resolved / Confirmed & Patched by Vendor

---

## Technical Analysis & Steps to Reproduce

### 1. Discovery & Reconnaissance
An analysis of the target endpoint revealed an exposed backup descriptor mapping. Executing a standard terminal request targeted the following directory listing configuration:

```bash
curl [https://vfo11.vodafone.om/xml/backup_descriptor](https://vfo11.vodafone.om/xml/backup_descriptor)
```
2. Information Leakage Analysis
The server responded with an index of active web roots exposing sensitive system administrative and architectural infrastructure assets:

backup.sql – Database structure and data dump containing potential user credentials and private information.

.bash_history – Command-line history of internal administrators, revealing internal system paths and software execution flags.

.php source files – Exposed backend application logic, increasing the surface area for code review and further vulnerability discovery.

Proof of Concept (PoC)]
Below is the validated terminal proof capturing the directory exposure from the misconfigured endpoint:

Risk & Impact Assessment
Leaving administrative backups and configuration environments publicly exposed introduces compounding security risks:

Credential Harvesting: Intercepting plain-text credentials or database strings from .sql or .bash_history contents allows immediate horizontal movement.

Source Code Auditing: Direct access to raw PHP scripts allows malicious actors to map out proprietary server-side logic and find severe architectural vulnerabilities (e.g., RCE or SQLi).

Phishing and Target Reconnaissance: Internal infrastructure paths leakage allows attackers to craft precise social engineering or targeted infrastructure attacks.

Communication Timeline & Resolution
The vulnerability was responsibly disclosed via the HackerOne platform. The security and engineering teams cooperated efficiently to address the asset leakage.

July 2, 2025: Vulnerability report submitted via HackerOne.

July 3, 2025: Report reviewed by HackerOne Triage and moved to internal assessment.

July 4, 2025: Severity assessed, and findings successfully triaged to the Vodafone Engineering team.

July 7, 2025: Vodafone internal staff confirmed the vulnerability, validated the server fix, and successfully restricted public access to the exposed directories. Report closed as Informative with reputation points awarded.

Verification of Remediation
The following screenshot illustrates the final triage workflow and communication logging on the HackerOne dashboard confirming the remediation deployment:

Key Professional Takeaways
This engagement demonstrates real-world experience identifying and documenting structural server misconfigurations on enterprise-grade scopes. It highlights the absolute necessity of enforcing stringent access control lists (ACLs), disabling automated web root directory indexation, and keeping production environments sanitized of administrative backup assets.
